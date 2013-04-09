#CoffeeScript & Backbone Applications

##General Style

* All CoffeeScript code (variable names, class names…) is written in camelcase
* Object and function names start lowercase. The only exception are constructor functions (like class definitions) that you can call with the `new` operator, e.g. `new ShapeView()`
* Globals shalt only be used with personal permission of Douglas Crockford <douglas@crockford.com>
* An appliaction uses a single namespace that contains *all* application code
* There are always two lines of white space between two methods
* Each tab is expanded to two spaces

## Naming Conventions
* View names are postfixed with `View`, e.g. `ShapeView`. The file name is lowercase singular, with `_view` postfix, e.g. `shape_view.coffee`. Both singular and plural are possible, depending on the use case. Views that render subviews for a set of models are plural. A view that renders, for example, 10 shapes, should be named `ShapesView`, with file name `shapes.coffee`.
* Model names are singular; no postfix is required. Example: `DisplayObject`, the file name would be `display_object.coffee`
* Collections are named like their models, but pluralized. Example: `DisplayObjects`, the file name would be `display_objects.coffee`

## DOM & Views
* Backbone views and the html markup they render are independent from the “rest” of the DOM. This means that no elements outside a view are manipulated. Backbone offers a handy scoped `$` function for this purpose. Calling `@$('.some-selector')` will search for an element that matches the selector *only within the view*. This is important because it promotes modularity and reduces side effects.
* If you wish to communicate with other objects from within a view, consider using:
	* The mighty `trigger` function. This is useful to notify parent objects that a certain event has occured. Example in a backbone view: `@trigger 'attachmentselected', argument(s)`. In the parent element you can bind on the view with `@childView.on 'attachmentselected', @onAttachmentSelected`. Important: Backbone events don’t bubble.
	* If the parent element is not enough, a mediator may be a good approach.
* Event names (e.g. `onuserselected`) are lowercase



## Namespacing
* Classes share a *single* namespace, like `drapit.views.ShapeView`
* “Abstract” classes are postfixed with `Base(View|Model|Collection)`, like `MenuItemBaseView`. This indicates that the class cannnot be instantiated directly.
* If a method of an abstract class *must* be implemented by its inheritors, consider throwing an error in the BaseView. It fires if the method isn’t overwritten.
* To call a function’s parent, `super()` is used instead of e.g. `MenuItemsBaseView.prototype.initialize.call(@, arguments)`
* The namespace mainly consists of classes. Actual objects, like e.g. a reference to the application router can be put in `runtime`: `drapit.runtime.router = new drapit.routers.MainRouter()`. This allows easy access to objects that are useful for debugging.

## Extending Object Prototypes
* Extensions of object prototypes, e.g. a `trim` method for the `String` object, are placed in a seperate file, e.g. `prototype_extensions.coffee`
* Function prototypes are only extended if the desired method does not exist. This can be done with e.g. `if typeof(String::trim) != 'function' then # your implementation`. This is important to avoid unexpected bahvior.


