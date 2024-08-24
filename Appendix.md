# Appendix

## Difference between System Design and Software Architecture

System Design and Software Architecture are closely related but focus on different aspects of creating a software system. Here's a breakdown of the key differences:

### System Design

* Scope: System Design deals with the overall structure and high-level components of a system. It includes defining the system's key components, how they interact, and how they meet specific requirements.
* Focus: It emphasizes the functionality, scalability, performance, and user requirements of the entire system. System Design addresses the big picture, including the overall structure, communication between components, data flow, and external interactions.
* Concerns: System Design is concerned with:
    * Defining the major components or subsystems (e.g., services, databases, user interfaces)
    * Data flow and communication between components
    * High-level design patterns
    * Scalability, fault tolerance, and load balancing
    * Technology stack decisions
    * Integration with external systems or APIs

### Software Architecture

* Scope: Software Architecture focuses on the detailed structure of individual software components, modules, or systems. It involves the technical blueprint of how these components will be implemented and interact at a code level.
* Focus: It delves into the technical aspects, such as how the code is organized, the application of design patterns, and the choice of frameworks and libraries. Software Architecture is more about the internal workings of software components.
* Concerns: Software Architecture is concerned with:
    * Code organization and structure
    * Application of design patterns (e.g., MVC, microservices, monolithic)
    * Modularization and layering of the software
    * Data modeling and database design
    * Security, maintainability, and extensibility of the codebase
    * Specific technologies, programming languages, and frameworks

### Summary

* System Design is about the high-level structure and relationships of components across the entire system.
* Software Architecture is about the detailed design and implementation within specific components or subsystems.

In practice, these two areas often overlap, especially in large systems where high-level design decisions influence detailed software architecture, and vice versa.
