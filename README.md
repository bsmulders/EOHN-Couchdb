# EOHN CouchDB demo

## Getting CouchDB to work

To start two CouchDB instances

    docker-compose up

The two instances are aproachable using these two webinterfaces:

[http://localhost:5985/_utils/index.html](http://localhost:5985/_utils/index.html) (couch1)  
[http://localhost:5986/_utils/index.html](http://localhost:5986/_utils/index.html) (couch2)

Using the webinterface on couch1, create a database named 'chat'. Then, add the following document to the [**_replicator**](http://localhost:5985/_utils/database.html?_replicator) database on couch1:

```javascript
{
   "source": "chat",
   "target": "http://couch2:5984/chat",
   "create_target": true,
   "continuous": true
}
```

This creates a database named 'chat' on couch2 and enables continious replication from couch1.

Add a document on [couch1/chat](http://localhost:5985/_utils/database.html?chat) to test the replication. This document should magically appear on [couch2/chat](http://localhost:5986/_utils/database.html?chat).

#### Hint

Internally, the servers are available on couch1:5984 en couch2:5984

The two instances can be turned on and off with:

    docker-compose [start|stop] [couch1|couch2]

To stop and tear down the project:

    docker-compose down

## Start the client

Open index.html in a browser. To have two clients running, use two browsers. If you use a single browser for multiple client they'll use the same database internally, no replication will take place. 

## Challenge

Add functionality to the application. Some suggestions:

- Replicate from the client to both couch1 and couch2 (hint: copy/paste). Test your replication by shutting down the servers one by one.

- Replicate from couch2 to couch1

- Nicknames (can be randomly generated)

- Removing messages

- Displaying timestamps

- Remove all messages

- Sync status of messages

- Multiple chat channels

- Edit messages

Switch to the "fullclient" branch if you are too lazy to do this.