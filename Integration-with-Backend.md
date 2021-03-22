# How SurveyJS Libraries Interact with the Server and Integrate with a Backend


SurveyJS offers four products:  
* SurveyJS Creator
* SurveyJS Library 
* SurveyJS Analytics Pack 
* SurveyJS PDF Export

Each is a JavaScript-written client library that works in a web browser and is server agnostic. We position these libraries as building blocks - _components_ - that help developers create a **_frontend_** part of their own survey management application. Developers can integrate our libraries with absolutely any server-side web framework/platform chosen for backend development.


## Client-Server Interaction

A simplified diagram of how SurveyJS client libraries interact with an application's server part looks as follows.

<!-- ![Client-Server Interaction](https://github.com/surveyjs/survey-documentation/blob/main/images/client-server-interaction.png?raw=true) -->
<img src="https://github.com/surveyjs/survey-documentation/blob/main/images/client-server-interaction.png?raw=true" alt="Client-Server Interaction" width="100%"/>

### JSONs to Communicate

As you can see, SurveyJS libraries communicate with the server by sending and receiving just two types of JSON objects:  
* `survey definition`  
A JSON that represents a survey model describing an individual survey's structure. The survey model contains questions which are typically organized in pages and lined up due to the necessary survey logic.  

* `survey response`  
A JSON that contains answers of an individual respondent to questions of a survey.

These JSONs are the only requirement for SurveyJS libraries to work on the client.  

### Storing JSON Data is a Backend Development Concern

If talking about on-premises application development, it is worth to admit that responsibility for an application's server part implementation lies with application developers. In particular, a developer should design a proper REST API for survey data exchange between server and client. And a developer should also create and maintain a server storage for survey data - `survey definitions` (questions) and `survey responses` (answers).  


## Application Layers and Components


### Client Side

 * **SurveyJS Creator**  
 A UI tool that allows survey managers/designers to visually create, customize and test surveys with ease right in a browser.  
 Works with:  
   * a `survey definition` (in JSON format)

   Customizable through public API.  
   Learn more: [Site](https://surveyjs.io/Overview/Survey-Creator), [Docs](https://surveyjs.io/Documentation/Survey-Creator), [Examples](https://surveyjs.io/Examples/Survey-Creator/)

 * **SurveyJS Library**  
 A core client library that allows developers to run a survey in a respondent's browser. The library's main tasks are to show a survey to a respondent and to collect respondent answers (a response). Developers can use the library's public API to programmatically customize any survey element as their application needs dictate.  
   Receives: 
   * a `survey definition` (in JSON format)

   Returns: 
   * a `survey response` (in JSON format)
   
   Provides a huge public API for customization.    
   Learn more: [Site](https://surveyjs.io/Overview/Library), [Docs](https://surveyjs.io/Documentation/Library), [Examples](https://surveyjs.io/Examples/Library/)

 * **SurveyJS Analytics Pack**  
 A client library to visualize and analyze a survey's results (all collected responses).  
 Receives:
   * a `survey definition` (in JSON format)
   * a list of `survey responses` (in JSON format)

   Provides public API for customization.  
   Learn more: [Site](https://surveyjs.io/Overview/Analytics), [Docs](https://surveyjs.io/Documentation/Analytics), [Examples](https://surveyjs.io/Examples/Analytics)

* **SurveyJS PDF Export**  
A client library to export survey responses to PDF files.  
 Receives:
   * a `survey definition` (in JSON format)
   * a `survey response` (in JSON format)

   Provides public API for customization.  
   Learn more: [Site](https://surveyjs.io/Overview/Survey-Pdf-Export), [Docs](https://surveyjs.io/Documentation/Pdf-Export), [Examples](https://surveyjs.io/Examples/Pdf-Export)

### Server Side
Implementation of an application's back-end part is a custom development task which is out of the SurveyJS libraries' application scope. Provide your own backend implementation based upon your business needs.

 * **REST API**  
 A survey service application should allow its client part to communicate with a server via the REST API. To transfer survey data, REST APIs should accept JSON in requests and send JSON in responses. Design proper API endpoints and access them from the client when supplying SurveyJS libraries with server data or sending their data back to the server.

 * **API Security**  

   * User Authentication and Authorization  
   Authentication:  
   Determine the identity of an application's end user sending a request.  
   Authorization:  
   Determine the resources an identified user is authorized to access. Prevent users from accessing API operations outside their predefined roles. 
   
   * Data Validation and Sanitization  
   Validate your API calls and sanitize user input to prevent cross-site request forgery ([CSRF](https://en.wikipedia.org/wiki/Cross-site_request_forgery)) attacks and code injections, such as cross site scripting ([XSS](https://en.wikipedia.org/wiki/Cross-site_scripting)) and SQL injection ([SQLi](https://en.wikipedia.org/wiki/SQL_injection)).
    
 * **Survey Data Store**  
 A survey management application should implement a database to store survey data (`survey definition` and `survey response` objects, typically in JSON format).
 Depending upon your scenario, you can build an on-premises data storage or host data in a cloud.


## How to Learn More

As we are concentrating on JavaScript client library development, we do not offer any production-ready server-side (back-end) solutions. 

For now, we actually provide our [My Surveys](https://surveyjs.io/Service/MySurveys) cloud [service](https://surveyjs.io/Overview/Service), however we use it more as a showcase of what can be done with the help of our client libraries.
If you want to implement a similar service on your own and look for more details about such an implementation, you can download, investigate and run locally one of our boilerplate samples listed here:
https://surveyjs.io/Examples/Service

These boilerplates are basic examples of a typical survey management application that mimics our My Surveys cloud service. These examples target different server platforms and are developed to help you get started with integration of SurveyJS libraries. 
