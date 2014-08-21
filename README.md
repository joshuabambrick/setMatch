# Backbone setMatch 0.0.1 #
A Backbone plugin which allows you to match models in a collection based on attributes other than their id.

## Introduction ##
Backbone setMatch is a Backbone plugin which allows you to match models in a collection based on attributes other than their id. This matching is used every time `set` is called on a collection, explicitly or internally by Backbone. This can be useful in cases where you want to create a more advanced collection which creates a neat representation data as models which is inconsistent with their representation on the server or where the server has no explicit `id` attribute.

## Usage ##
In order to use setMatch with any collection, simply define the `setMatch` property in the collection's declaration.

    var MyCollection = Backbone.Collection.extend({
        setMatch: /* setMatch parameters */
    });

The `setMatch` property can either be a boolean or an object.

If `setMatch` is `true`, models added to the collection will need to match all properties - if it is `false`, setMatch will not be used and the default behaviour occurs.

If `setMatch` is an object, there are many different parameters, all of which are optional, which may be defined:

`match` provides an array of names of properties which must be matched, a string of a single name of a property which must be matched or a function which takes a property name and returns true if the property should be matched, and false otherwise. If `match` is not defined, all parameters must be matched. If you specify that `id` must be matched, matching will be dependent on the `id` parameter (see below).

`id` allows you to specify what the behaviour should be regarding the `id` property of models when it is defined for the model passed to `set`. If this value is `retain`, then the value of the `id` property of the resulting model will be that of the model before `set` was called. If this value is 'inherit', then the value of the `id` property of the resulting model will be that of the incoming model passed into `set`. If this is not defined, then if the model passed to set has a `id` parameter, this will need to match that of the model in the collection or a separate model will be added.

`active` is a boolean that allows you to switch off setMatch. If setMatch has been defined in a collection's declaration then you will need to set the `active` property to false to disable setMatch.