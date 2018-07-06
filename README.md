SMART on FHIR JavaScript Client Library
=======================================

## Building

To build the library, you will need Grunt and NPM. Once you
have all the dependencies in place, you can build the library
with the `grunt` command.

Here are the exact steps to build the client library
on Ubuntu 14.04:

```
sudo apt-get update
sudo apt-get -y install git npm
sudo ln -s "$(which nodejs)" /usr/bin/node
git clone https://github.com/smart-on-fhir/client-js
cd client-js
npm install
sudo npm install -g grunt-cli
grunt
```

If all goes well, the client library will be available in the
`dist` directory in multiple variants as follows:

* `fhir-client.js` - complete client library with jQuery and [fhir.js](https://github.com/FHIR/fhir.js) included (no external dependencies)
* `fhir-client-jquery.js` - client library using jQuery, jQuery and [fhir.js](https://github.com/FHIR/fhir.js) not included
* `fhir-client-angularjs.js` - client library using AngularJS, AngularJS and [fhir.js](https://github.com/FHIR/fhir.js) not included

## fhir.js API Documentation

Visit [fhir.js](https://github.com/FHIR/fhir.js) repository to read more about FHIR API documentation provided in `lib/jqFhir.js` library.

## Usage

For usage examples and further documentation, please visit http://docs.smarthealthit.org/clients/javascript/

### Passing headers to fhir.js library

The latest version of this library allows headers to globally be set and passed to [fhir.js](https://github.com/FHIR/fhir.js) library for all requests to a FHIR resource server.  The header cannot be selectively set per FHIR resource being called. See [fhir.js](https://github.com/FHIR/fhir.js#headers) documentation for more info.

There are two ways to achieve this.

1. Using the `input` argument of `FHIR.oauth2.ready` function at initialization

    ```
    { 'headers': {'Accept-Language': 'en-US'} }

    FHIR.oauth2.ready({ 'headers': {'Accept-Language': 'en-US'} }, callback, errback);
    ```

2. Using the new `setHeaders` function on the argument of the callback function defined `FHIR.oauth2.ready` function

    ```
    ...
    FHIR.oauth2.ready(onReadyCallback, onErrorCallback);
    ...
    function onReadyCallback(smart) {
      if (smart.hasOwnProperty('patient')) {
        // Set headers
        smart.setHeaders({'Accept-Language': 'en-UK'});
    ...
    ```

If the same header is set using both methods, the value of the header set via `setHeaders` will have a higher precedence.