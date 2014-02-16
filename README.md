meteor-test-dir-order
=====================

Example meteor app to test load order of directories

The [Meteor documentation](http://docs.meteor.com/#structuringyourapp) states:

> The JavaScript and CSS files in an application are loaded according to these rules:
> 
> * Files in the lib directory at the root of your application are loaded first.

Given the following directory structure:
```
.
├── a
│   └── lib
├── client
│   └── lib
├── common
│   └── lib
├── lib
└── server
    └── lib
```

Expected load order is:
```
// client
lib   <-- note lib directory
a/lib
client/lib
common/lib
a
client
common

// server
lib   <--
a/lib
common/lib
server/lib
a
common
server
```

Actual load order:
```
// client
a/lib
client/lib
common/lib
lib   <---  bummer
a
client
common

// server
a/lib
common/lib
server/lib
lib   <---  :-(
a
common
server
```
