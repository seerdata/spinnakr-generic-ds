The Spinnakr generic data structure uses Yelp as a data model,
showing the different types of structures that are available
in JSON documents.

Please review test01.json as an example of how to structure data.

Note that one can have 'N' categories at the top level each
defined in the categories array.

Each category has its own ID enabling the possibility
in the future of persistant storage via cassandra or other document
store.

Each 'category' has within it attributes which allows for further
customization of the particular data.
