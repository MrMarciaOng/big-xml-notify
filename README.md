# big-xml-notify -- A fork of npm big-xml, when big files is fully read an "close" event will be emitted.

## Motivation 

Added this notify feature for my school data processing assignment.
There are many big files to process and I need to know when the files has been fully processed. 

## Install

    npm install big-xml-notify


#Example

XML files are streamed, and parsed one record at a time, which keeps memory usage low.

You must specify which XML elements should be considered as the root of a record, using a regex. In this
example the elements Foo and Bar will be emitted as records.

```javascript
var bigXml = require('big-xml');
    
var reader = bigXml.createReader('data.xml.gz', /^(Foo|Bar)$/, { gzip: true });

reader.on('record', function(record) {
  console.log(record);
});
```

The output would take the form:

```javascript
{ tag: 'Foo',
  attrs: { Name: 'John', Status: 'Student' },
  children: [
    { tag: 'Color', text: 'blue'} 
  ]
}
```

And if you want to handle errors (by default they are thrown):

```
reader.on('error', function(err) {
  console.log(err);
});

reader.on('close', function(){

console.log("File is fully read")
})
```
