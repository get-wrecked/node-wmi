# node-wmi
Library to execute wmi (Windows Management Instrumentation) commands.

## Install
```bash
npm install node-wmi
```
## Documentation
__Methods__

 * [`node-wmi#Query()`](#query)

### <a name="query"></a>Query([options, callback])
Constructor that generates an instance of the Query class.

__Arguments__
 * [`options`](#query_object) - Object representing options for the query. Options can also be applied via chain api. (*optional*)
 * [`callback(err, result)`](#query_callback) - Callback. If not supplied query will not be executed until query.exec() method has been called. (*optional*)

__Return Value__
The Query method returns an instance of the query class.

<a name="query_object"></a>__Options Properties__

 * `host` (type: string) - Hostname or IP of the client to get information from. Defaults to `localhost`.
 * `namespace` (type: string) - Namespace of the class to query. Defaults to `root\CIMV2`.
 * `class` (type:string) - Class to be queried for information. (*required*)
 * `properties`/`props` (type: [string])- List of properties of the class to query for. If not set, all properties will be returned for the given class. (*optional*)
 * `username` (type: string) - Username to use to perform query. (*optional*)
 * `password` (type: string) - Password for the above username. (*optional*)
 * `where` (types: string, [string]) - Where clause for the query. The where clause can come in multiple different types. If you pass in a string, it will be accepted as a literal text to go in the where clause. If you pass in an array of strings, they will be And'ed together. (*optional*)

__Chainable API__
Chainable api methods exists to set each property for the query. To use the chainable api, call the method of the name of the property which you would like to set with the first argument being the value of the property and an *optional* second argument being a callback function to execute the query.

<a name="query_callback"></a>__Callback__
The callback has the signature of (err, result). The callback can be supplied as the second argument to either the constructor or any of the chainable functions. The callback is the first and only parameter for the exec method.

__Examples__
```javascript
// Object usage

var wmi = require('node-wmi');
wmi.Query({
  class: 'Win32_BIOS'
}, function(err, bios) {
  console.log(bios);
});
```

```javascript
// Chainable API reference with exec method

var wmi = require('node-wmi');
wmi.Query().class('Win32_BIOS').exec(function(err, bios) {
  console.log(bios);
});
```

```javascript
// Using callback in chainable api

var wmi = require('node-wmi');
wmi.Query().class('Win32_LogicalDisk', function(err, disks) {
  console.log(disks);
});
```
