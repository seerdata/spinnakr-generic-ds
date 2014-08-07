

Here is the model specification:

https://github.com/stormasm/spinnakr-generic-ds/blob/master/test01.json

So the idea is this --- the top level properties are ones that every JSON will have.

The categories property is mandatory just like all of the other top level properties BUT it can be an empty array.

If you decide to add in a category you can call it whatever you want and that "name" will go in the category array.

You can have as many categories as you like and the corresponding category name as a property.

The data structure for each category is variable meaning you can have anything in there you like.

The specification shows arbitrary types of data structures within each category.  

I show two model categories with arbitrary data structures as good examples of how to have multiple categories.

The idea being that when we process this data in Redis / Storm we will be able to have category readers.

These readers will know what the data structures in each category look like.

So given a set of customers with slightly different category requirements all we will have to do :)

Is write a new Reader and we are good to go.

I reviewed various data structures around the internet especially from YELP and came up with this concept based on what I saw.

Here is an example of a Yelp data structure with multiple categories:

https://github.com/stormasm/spinnakr-generic-ds/blob/master/examples/yelpformat.json

The example categories are [business, review, checkin, tip, user]

So you can see based on our data structure we could have five categories in the category array and then five readers to model and process that data.

One thing that would be great for you all to do is look at our two current LEGACY data structures and make sure I hit all of the mandatory properties at top level.

Legacy ACTION

https://github.com/stormasm/spinnakr-generic-ds/blob/master/examples/actionformat.json

Legacy VISIT

https://github.com/stormasm/spinnakr-generic-ds/blob/master/examples/visitformat.json

Note that one can have 'N' categories at the top level each
defined in the categories array.

Each category has its own ID enabling the possibility
in the future of persistant storage via cassandra or other document
store.

Each 'category' has within it attributes which allows for further
customization of the particular data.
