# Backbone setMatch 0.0.1 #
A Backbone plugin which allows you to match models in a collection based on attributes other than their id.

## Introduction ##
Backbone setMatch is a Backbone plugin which allows you to match models in a collection based on attributes other than their id. This matching is used every time `set` is called on a collection, explicitly or internally by Backbone. This can be useful in cases where you want to create a more advanced collection which creates a neat representation data as models which is inconsistent with their representation on the server or where the server has no explicit `id` attribute.

As well as being used explicitly, the `set` method is used internally by Backbone's `add` method. `setMatch` is particularly useful when used in conjuction with the [`{merge: true}` parameter](http://backbonejs.org/#Collection-set) set.

## Usage ##
In order to use setMatch with any collection, simply define the `setMatch` property in the collection's declaration.

    var MyCollection = Backbone.Collection.extend({
        setMatch: /* setMatch parameters */
    });

The `setMatch` property is typically an object, although it may take other forms.

### setMatch : object ###
If `setMatch` is an object, there are many different parameters which may be defined, all of which are optional:

#### match (optional) ####
`match` provides an array of names of properties which must be matched, a string of a single name of a property which must be matched or a function which takes a property name and returns true if the property should be matched, and false otherwise.

If `match` is not defined, or takes an unrecognised form, all parameters must be matched. If you specify that `id` must be matched, matching will be dependent on the `id` parameter (see below).

#### id (optional) ####
`id` allows you to specify what the behaviour should be regarding the `id` property of models when it is defined for the model passed to `set`.

If this value is **'retain'**, then the value of the `id` property of the resulting model will be that of the model before `set` was called.

If this value is **'inherit'**, then the value of the `id` property of the resulting model will be that of the incoming model passed into `set`.

If this is not defined, then if the model passed to set has a `id` parameter, this will need to match that of the model in the collection or a separate model will be added.

#### active (optional) ####
`active` is a boolean that allows you to switch off setMatch. If setMatch has been defined in a collection's declaration then you will need to set the `active` property to false to disable setMatch.

### setMatch : array | string | other ###
If `setMatch` is not a plain object, it will be assumed to take the form of the `match` property above and all other properties will assume their default.