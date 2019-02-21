Node service template
---
A template for building a RESTful service.

To adapt this template for a new service
---
   * edit but do not rename: `README.md`, `package.json`, `api/swagger.json`, `lib/constants.js`
   * rename and edit: `config/*`, `controllers/fortunes.js`, `lib/fortune.js`, `lib/fortuneteller.js`, `test/*`

Do not rename or modify anything else. If you want to modify other files, consider updating the template as well.
   
To test this service as-is, run the following commands from a shell window
---
   1. install the dependencies: `npm install`
   1. lint the files: `npm run lint`
   1. run the tests: `npm test`
   1. start the service: `npm start`
   1. retrieve random fortunes: `curl -X GET http://localhost:8080/v1/fortunes`
   1. execute the following to create a new fortune: `curl -X POST http://localhost:8080/v1/fortunes -d 'text=you%20will%20be%20fortunate'`, and take note of the `link` returned in the response for the steps that follow.
   1. use `curl -X GET $LINK` replacing `$LINK` with the link returned in the previous step
   1. re-execute the random fortune operation until `you will be fortunate` appears
   1. delete the fortune: `curl -X DELETE $LINK` replacing $LINK with the link returned by your POST
   1. attempt to fetch the fortune you added using `curl -X GET -D - $LINK` and observe the `404`. 
   
The template integrates [swagger-tools-wrapper](https://github.home.247-inc.net/platform/swagger-tools-wrapper) and allows you to render the raw swagger API document and an interactive representation of the API using the following URLs:

```
http://localhost:8080/v1/fortunes/api-docs
http://localhost:8080/v1/fortunes/docs
```
