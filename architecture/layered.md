# Layered architecture

The layered architecture is the most common of the architecture patterns that are discussed in this document. 
Well-designed applications will usually be composed of logical horizontal layers, each dedicated to fulfilling a given role. The main layers are usually: 
- The presentation layer, responsible for the UI and user workflow (navigation among the UI screens), 
- The application layer, that implements the processes (steps) of the application, through the manipulation of the features that are offered by the components of the business layer.
The logic implemented in the application layer is specific to that application's use cases.
- The business layer, which implements the business logic and business objets. They reflect the main concepts of the business domain that is covered by the application and they are usually persistent, i.e. their state will be saved into a durable data store. The definitions (e.g classes) of the business objects is usually highly reusable.


