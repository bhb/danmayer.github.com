### Evaluating API development tools

I have been evaluating and looking over various API tools lately. In part as I develop more APIs myself for personal projects. Mostly because I have learned that all projects these days will have some sort of API backend and multiple front ends: web, mobile apps, native desktop, internal reporting tools, etc, etc. Basically, if you can generate any sort of interesting data eventually people will want it in other formats. Because of this anything that has data I am starting to think about API first. Many other developers are starting to focus more on internal and external APIs as well, which is why there is a variety of great tooling popping up related to it.

I had been playing a bit with some API tools such as [Apiary](http://apiary.io/), and [Fdoc](https://github.com/square/fdoc) a bit on my side projects. At work, various discussions about the future of our APIs began to heat up. [Adam Keys](http://therealadam.com/), [Cloves Carneiro](https://twitter.com/ccjr), and [Tim Schmelmer](http://www.timschmelmer.com/) were leading the charge in having better tooling around our APIs. The discussions lead to some features we wanted to support, which caused me to start to take a much closer look at some of the API tools available.

### Features we wanted

The most common features we wanted after discussing our APIs and some of the tools available.

* Support for multiple languages. (preferably all the ones we use in the company)
* Support for automatically generating client code from an [IDL definition](http://en.wikipedia.org/wiki/Interface_description_language)
* Support for generating service-side generation of API documentation, based on the IDL definition of the APIs
* Support for cURL / browser based service interaction, to analyze requests / responses in a "human-readable" format

There were other things we wanted, but this was the most common and most desired list of features. I will also say that since we are considering this for use in our day job, I wanted solutions that would work all self-hosted / behind the firewall. Which makes some of the hosted solutions like [Apiary](http://apiary.io/) less interesting although large parts of their solution is open sourced, like [API Blueprint](http://apiblueprint.org/). 

Basically, with the growing number of APIs we wanted something similar to [Google APIs Discovery Service](https://developers.google.com/discovery/). Google's tools are great, but not really an option as they haven't open sourced the document generation, service discovery server, or much language side tooling. What has been open sourced is a [client code generator](https://code.google.com/p/google-apis-client-generator/), which doesn't have as much language support as we would like (Java, Java/GWT, .NET, and PHP). Also, open sourced was the [google-apis-explorer](https://code.google.com/p/google-apis-explorer/) which while cool doesn't quite cover full documentation. Which would work for you if you build out APIs that match their schema, but their supported languages are limited and don't include my primary language Ruby. 

### Why not just a Rails JSON api

Basically the state of APIs is already like this today. The response formats are slightly different. The documentation is lacking and inconsistent. The clients sometimes are small configurations on rest-client, and sometimes built out a large custom client gems. This makes the tests, caching, usability, a whole new ballgame with each API. So we are looking to get more benefits than just moving from various custom presenters and JSON formatters to a consistent usage of something like [Jbuilder](https://github.com/rails/jbuilder). Similarly the if we are looking for larger improvements, the list of options below can be excluded:

* [RABL](https://github.com/nesquena/rabl)


For those that might just be interested in the best way of building custom JSON responses of mapping Ruby objects to JSON, the change log has a good post on [crafting JSON output](http://thechangelog.com/a-few-tools-to-build-a-json-api-in-a-ruby-web-app/), which shows some examples, although it is a little dated.


### Why not Thrift, Protocol Buffers, or Avro

We want a curl / human readable API. We want to be able to easily write a generic client if we need to. That knocks out both Thrift and Protocol Buffers. 

While Avro supports JSON as a format and has better platform support in terms of mobile, 

http://tech.flurry.com/2012/07/12/apache-avro-at-flurry/

it still isn't really human curl-able. maybe example 

    curl  curl -v -H "Accept: application/json" -H "Content-type: application/json" -X POST -d '{"adSpaceName":"splash_screen","location":{"lat":12.231212,"lon":23.3435},}' http://localhost:8080

"Dynamic typing: Avro does not require that code be generated. Data is always accompanied by a schema that permits full processing of that data without code generation, static datatypes, etc. This facilitates construction of generic data-processing systems and languages."
http://avro.apache.org/docs/current/
 
Avro doesn't seem to have great Ruby support http://www.igvita.com/2010/02/16/data-serialization-rpc-with-avro-ruby/


### Api Tooling Options

* [Rocket Pants](https://github.com/Sutto/rocket_pants): opinionated rails api framework.
  * __pros:__
  * Highly integrated into rails and activerecord (AR error support, AR object mapping support. 
)
  * Most standard rails coding style
  * build in support for easy caching
  * Easy Ruby client generation via [ApiSmith](https://github.com/Sutto/api_smith) integration
  * __cons:__
  * Doesn't include pretty documentation generation support
  * Also a pro but heavily tied to rails.
  * Custom format doesn't yet support [JSON Schema](http://json-schema.org/)
  * Client generation is Ruby only
  
* [FDoc](https://github.com/square/fdoc): Documentation format and verification, built by [Square](https://squareup.com/)
  * __pros:__
  * Works with Rails or Sinatra
  * Integrated testing and verification support
  * Supports [JSON schema](http://json-schema.org/) standard
  * Includes documentation page generation support
  * Company [sponsored support via Square](http://corner.squareup.com/2012/06/fdoc.html)
  * __cons:__
  * The documentation pages leave a lot to be desired. Not interactive, not very skimable.
  * No client generation support
* [Heroics](https://github.com/heroku/heroics): Ruby Client generation from JSON Schema
  * [Generating a Go client](http://www.paasmag.com/2014/01/09/auto-generating-a-go-api-client-for-heroku/)

* [Barrister](http://barrister.bitmechanic.com/)

http://jsonapi.org/

* [RAML](http://raml.org/): A YAML description language for rest-line JSON apis, built by [Mulesoft](http://www.mulesoft.com/)
* __pros:__
*  Very polished tooling & extremely good documentation, seems to have community support via [RAML workgroup](http://raml.org/about.html)
*  Sharable [API notebooks](https://api-notebook.anypoint.mulesoft.com/?ref=apihub) to share example usage and scripts, might be an interesting way to share configuring and usage.
*  Interactive Documentation
*  Nearly all components open sourced
*  __cons:__
*  Early code gen tools, Ruby not supported
*  Documentation of the API lives entirely outside of standard code flows and tools
*  While a open format, it is kind of a odd non-standard format

https://github.com/seomoz/interpol

https://github.com/mashery/iodocs   examples http://dev.mashery.com/iodocs


### Working with swagger and Ruby

swagger helps build api documentation, and clients.

http://developers.helloreverb.com/swagger/

### Pros

* The documentation generated is extremely usable
* automatically builds clients
* Keeping the API spec with the code increases the chances it will stay in sync
* Open source we could contribute and fix any issues we have

### Cons

* Littering code with hard to read 'comments' that is really just injecting another language into the comments of your code seems gross.
* A self describing and following api seems more discoverable.
* While the api doc JSON is human readable it
* Code is littered with long and verbose comments
* Errors while generating documentation or clients are pretty unhelpful.
* Learning curve a bit higher than expected

### Tips

* build it one endpoint and model at a time
* make sure you can test locally as the generate docs, deploy, generate code cycle can be slow
* make only one change at a time between testing both doc and client source code generation
* frequently it is best to view the final JSON output to help diagnose what looks wrong somewhere. [JSONView extension](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc?hl=en) for chrome is extremely helpful when reading the JSON docs.

### CMDS

install: https://github.com/wordnik/swagger-core
add it to path

look at this example
https://github.com/wordnik/swagger-core/tree/master/samples/ruby-source2swagger

use this gem
https://github.com/solso/source2swagger

follow this example and steal it's rake file task
https://github.com/mstine/sinatra-swagger-example

cp swagger-ui dist folder to public docs

add these routes

run `bundle exec rake swagger` and view /api-docs

hit /docs

alter index.html to default to your docs

update lots of comments... notes on errors, models, return types...

Try to generate a client...

run https://github.com/wordnik/swagger-codegen
`./bin/runscala.sh com.wordnik.swagger.codegen.BasicRubyGenerator http://churn.picoappz.com/api-docs "key"`

### additional reading

* [Swagger Api-docs](https://github.com/wordnik/swagger-core/wiki/Api-Declaration)
* [Swagger parameter docs](https://github.com/wordnik/swagger-core/wiki/parameters)
* [Heroko's JSON schema support for platform API](https://blog.heroku.com/archives/2014/1/8/json_schema_for_heroku_platform_api). Mentions JSON schema support for swagger, but doesn't seem to be fully support swagger format.
* Salesforce Swagger usage:
  * [Start visualizing your Force.com RESTful services.](https://force-com-rest-swagger.herokuapp.com/)
  * [Salesforce swagger api slideshow](http://www.slideshare.net/developerforce/df13-exposing-salesforce-rest-service-using-swagger-1)
  * [Unio](https://github.com/ttezel/unio): one rest client to rule them all. Javascript and Python implementations. Describe a service in JSON, dynamically build a client for it.
  
### Examples

http://churn.picoappz.com/docs/index.html#!/churn

data
http://churn.picoappz.com/api-docs
http://churn.picoappz.com/api-docs/churn

when struggling compare to their examples
http://petstore.swagger.wordnik.com/api/api-docs/pet

### Modifying Swagger-Code-Gen 

If you change the scala files just rerun. If you change the mustache files you must rerun `/sbt assembly` to cache the new template changes. 


### Other Ruby api integrations worth looking at