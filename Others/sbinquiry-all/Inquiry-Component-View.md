
## Component Diagram
![](images/storage/inQuiry%20Component%20View.drawio%20(1)-20230523-105549.png)


## External Components
The external components that inQuiry needs to function (libraries or services)



|  **Name of the component**  |  **What does it do?**  |  **Why it is needed?**  | 
|  --- |  --- |  --- | 
| Knowlg : ePub PlayerUnused - To be removed from QuML Editor | NA | inQuiry is not using it, there is a tight dependency from Resource LibraryThis needs to be made as optional dependency in Resource Library as it is planned to be used by Knowlg. **Action Item** 1completeRemove the tight dependency of ePub Player in Resource Library [\[IQ-413]](https://project-sunbird.atlassian.net/browse/IQ-413) | 
|  Knowlg : PDF PlayerUnused - To be removed from QuML Editor | NA | inQuiry is not using it, there is a tight dependency from Resource LibraryThis needs to be made as optional dependency in Resource Library as it is planned to be used by Knowlg. **Action Item** 2completeRemove the tight dependency of PDF Player in Resource Library [\[IQ-413]](https://project-sunbird.atlassian.net/browse/IQ-413) | 
| Knowlg : Video PlayerUnused - To be removed from QuML Editor | NA | inQuiry is not using it, there is a tight dependency from Resource LibraryThis needs to be made as optional dependency in Resource Library as it is planned to be used by Knowlg. **Action Item** 3completeRemove the tight dependency of Video Player in Resource Library [\[IQ-413]](https://project-sunbird.atlassian.net/browse/IQ-413) | 
| Knowlg : Knowlg Services (API) | These services are used for:<ul><li>Creating and uploading assets such as images, videos

</li><li>Composite search of questions

</li><li>Getting Framework and Channel data 

</li><li>Getting Form Configuration (Object category definition) 

</li></ul> | inQuiry service provides the functionality of managing questions and questions sets. However the creation of question and question sets require additional services that are provided by Knowlg Services.  | 
| Knowlg : Graph Engine (aka Ontology Engine)This can be replaced as Knowlg Core (has : platform-core, ontology-engine, platform-modules)

 | Graph-engine acts as an interface between databases and service module. It encapsulates all the calls to the underling data stores (Neo4J, Cassandra, Redis, etc). | This is available as library for consumption and code need not be repeated in modules that needs to access the underlying data store.The Knowledge Platform uses the Graph engine to communicate with Neo4j. The Graph engine expects schema definitions for each object type. It validates the data object with the object definition during various CRUD operations. | 
| Knowlg : Platform Telemetry (platform-telemetry) | This is used by the inQuiry API services to send the telemetry events to Obsrv service which stores all the event data. | Telemetry events data provides insights on how the system is being used. | 
| ED : Client Services | Typescript Library used to create API calls with Sunbird Environment. Includes necessary typescript code to do search, content read, corresponding data models of the platform are available.[https://github.com/Sunbird-Ed/sunbird-client-services](https://github.com/Sunbird-Ed/sunbird-client-services) | In order to facilitate Adopters to connect with Sunbird System. Typescript based library to connect with APIs. It can facilitate the adopters with readily available data models. _inQuiry is using this client services only for making the telemetry API calls. This is reused across different building blocks. Helps with wrapper services which otherwise will have to be written by different parties._  | 
| Telemetry : Telemetry SDK _This is a dependency for Sunbird : Client Services_ 

 | An open specification for recording and measuring statistical data from real-world use of digital apps & platforms. Details [here](https://telemetry.sunbird.org/) | The objective of telemetry is to assist in product, application or service development, modification or security. It works as a framework. Telemetry enables automatic collection of data from real-world, real-time use. Details [here](https://telemetry.sunbird.org/learn/understand#why-we-need-telemetry) | 
| ED: SB-Styles | Core Styling of Sunbird Products are present in this repository. CSS implementation for containers, grids.[https://github.com/Sunbird-Ed/sb-styles](https://github.com/Sunbird-Ed/sb-styles) | Consists of Basic Styles which are commonly used across Consumption Clients. | 
| Obsrv : ServicesThe telemetry service is passing the telemetry events to Obsrv.

 | [Sunbird Obsrv](https://obsrv.sunbird.org/learn/product-and-developer-guide) is a combination of various tools which provide the capabilities such as streaming, processing and storage of telemetry data and deriving reporting insights from the data. | [Sunbird Obsrv](https://obsrv.sunbird.org/) comprises several pluggable tools and microservies that come together to enable observability features on any platform/solution. No direct API calls from front-end clients or inQuiry micro service. The telemetry service is passing the telemetry events to Obsrv through a series of data-pipelines. | 
| Knowlg : Platform DB ExtensionsNeo4J plugin

 | Synch Neo4J data to Elastic Search[https://github.com/Sunbird-Knowlg/knowledge-platform-db-extensions](https://github.com/Sunbird-Knowlg/knowledge-platform-db-extensions) | The data that is stored in Graph DB (Neo4J) needs to be made available in ElasticSearch for search functionalities.High Level flow goes like,<ul><li>Write all Neo4J transactions to log files (in a particular format)

</li><li>Logstash picks up this files and sends to Kafka

</li><li>Kafka Consumer (a flink job) reads the message and writes to Elastic Search

</li></ul> | 


## Internal Components
The internal components that inQuiry needs to function (that is owned and operated by inQuiry)



|  **Name of the component**  |  **What does it do?**  |  **Tech Stack**  |  **Why it is needed?**  | 
|  --- |  --- |  --- |  --- | 
| inQuiry : QuML Editor | Question set editor is a tool offered by inQuiry to help you kickstart your creation of Question Banks[https://inquiry.sunbird.org/learn/capabilities-1](https://inquiry.sunbird.org/learn/capabilities-1) | Angular / HTML5 / CSS | This is used for creating the question banks.Editor is available as Angular Library and Web Component. Web component for the usage in an framework agnostic fashion.Benefits of using Angular,<ul><li>TypeScript

</li><li>Declarative UI

</li><li>PWA and SPA

</li><li>Simplified MVC Pattern

</li><li>Modular Structure

</li><li>Code Consistency and Easy Testing

</li></ul> | 
| inQuiry : QuML Player | Question set player is a player provided by inQuiry to create engaging & inclusive experiences for end users consuming the question sets. | Angular / HTML5 / CSS | This is used for playing the questions from question banksWeb component for the usage in an framework agnostic fashion.Benefits of using Angular,<ul><li>TypeScript

</li><li>Declarative UI

</li><li>PWA and SPA

</li><li>Simplified MVC Pattern

</li><li>Modular Structure

</li><li>Code Consistency and Easy Testing

</li></ul> | 
| inQuiry : Resource Library | Provides reusable UI and functionality for,<ul><li>Searching questions based on taxonomy

</li><li>Adding Question to QuestionSet from Question Library

</li></ul>[https://github.com/Sunbird-inQuiry/sunbird-resource-library](https://github.com/Sunbird-inQuiry/sunbird-resource-library) | Angular / HTML5 / CSS | Reusable library for,<ul><li>Searching questions based on taxonomy

</li><li>Adding Question to QuestionSet from Question Library

</li></ul>Action Item4incompleteRemove - [https://github.com/Sunbird-inQuiry/resource-library](https://github.com/Sunbird-inQuiry/resource-library) | 
| inQuiry : inQuiry Services (API) | Question and Question set service is a micro-service which provides APIs to manage the lifecycle and workflows of creation and consumption of question & question set objects. | Play FrameworkScala | It enables the question(s) and question set(s) creation, review and publishing process.The existing monolith (Spring MVC) was migrated to micro services using Play Framework with the benefits of,<ul><li>Easy to build web applications with Java & Scala

</li><li>Proven in production

</li><li>Scale predictably

</li><li>Non-blocking I/O

</li><li>Built on Akka

</li><li>Solid & fast

</li></ul> | 
| inQuiry : QuML Specification | Question Markup Language (​QuML in short) is a specification for storage, rendering and distribution of Questions and Tests | JSON | QuML defines a standard format for representation of questions, tests and their results, supporting the exchange of this material between authoring and delivery systems, repositories and other e-learning systems. | 




## References

* [https://ed.sunbird.org/use-1/source-code/reference-apps](https://ed.sunbird.org/use-1/source-code/reference-apps)


* [https://ed.sunbird.org/use-1/independent-libraries](https://ed.sunbird.org/use-1/independent-libraries)





*****

[[category.storage-team]] 
[[category.confluence]] 
