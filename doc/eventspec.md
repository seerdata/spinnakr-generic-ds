
### Spinnakr Event Spec

We have now agreed on a plan to develop the event spec.  The event spec
is the other side of the equation of our product.  It is a way for our customers
to get answers to the data they have been sending to us.  It is a way for
us to show them what is happening in their system.  It can be thought of
as a similar system to our recommendations.

All of our data will live in Redis.  By doing this, we make the system very
simple from a development perspective.  We are already using Redis for
the input data, so why not use it for the output data for now as well.

The Redis platform will give us a nice way to migrate in the future to
what ever long term persistance system our customers want.

All of the event data will live in a Redis Hashmap

The key space will be divided up by customer account_id.

Meaning if you look at a particular DB in Redis the only thing you will
see in there is a particular customers data.

I will be responsible for determining the Redis DB for a particular customer.
When I send Justin the input JSON data, I will send along the DB number. Justin
will then use that number along with the Redis **select** statement to write the
output event data to that particular DB.

The Redis Hashmaps will have the following key name structure.

```
project:dimension:key:primarykey
```

Examples include the following for project ids {1,2}

```
1:job-skills:java:0
1:job-skills:python:1
1:job-skills:ruby:2
1:job-skills:java:3

2:job-skills:ios:4
2:job-skills:java:5
2:job-skills:go:6

1:job-skills:storm:7
2:job-skills:trident:8
```

NOTE: The primary key is unique across all of the keys in the particular DB
and enables us to have keys with the same name.  For example, at a later
point in time we may want to do the exact same key again, but it will have
a different primary key.

The primary key infrastructure will read from Redis a key called
**primary-key** which will sit in the same DB we are writing to for that
particular account id.  The **primary-key** will be read, a new key will be
written and then that key will be incremented by 1.  The primary keys
will be integers starting at 0 (zero).

The beauty of this system is that because we are using Hashmaps we can
write anything we want in the Hashmap depending on the problem.

The endpoint will have in it the /project/dimension/key so we know
what key to pull and then process and send back the appropriate JSON.

The returning JSON structure will be the Redis Hashmap converted to JSON.

#### Possible Names inside the Hashmap / JSON

```
event_type       : "comparator"
account_id       :
project_id       :
dimension        :
key              :
calculated_value :
threshold        :
created_at       :
```
