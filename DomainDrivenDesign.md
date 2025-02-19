# Domain Driven Design

Domain-Driven Design is an approach that helps us succeed in understanding, designing, and building software models that solve complex business problems. The key elements are Domain, Model, and Software.

A Domain is a sphere of knowledge or activity.

A Model is a system of abstractions that describes selected aspects of a Domain and can be used to solve problems related to that Domain. A Model distills knowledge and assumptions about a Domain.

What about Software? If you’re reading this document, there’s no need to explain what that is. However, you should know that Domain-Driven Design provides Developers with strategic and tactical modeling tools to aid in designing high-quality software that meets their business goals.

More importantly, Domain-Driven Design is not about technology. Instead, it’s about developing knowledge around business and using technology to provide value. Only once you’re capable of understanding the industry your company works within will you be able to participate in the software model discovery process to produce a common business language and understanding - otherwise known as the Ubiquitous Language.

## Why Domain-Driven Design Matters

Software isn’t about just code. If you think about it, code is rarely the end goal of our profession. Rather, it’s merely the medium for solving business problems. That said, why does it have to speak a different language than a business?

Domain-Driven Design emphasizes making sure a business and its software speak the same language. Once that occurs, barriers to communication are removed, and there’s no longer a need for translation or tedious syncing. Furthermore, the information doesn’t get lost. In this way, everyone - not just coders - contributes to discovering the Business Domain, and in turn, the resulting software is the only truth for the common language.

Domain-Driven Design also provides a framework for Strategic Design and Tactical Design - strategic to pinpoint the most critical areas to develop based on business value, and tactical to build a working Domain Model of battle-tested building blocks and patterns.

## The Three Pillars of Domain-Driven Design

Domain-Driven Design is an approach for delivering software, and it’s based on three pillars, outlined here.

1. **Ubiquitous Language:** Domain Experts and software Developers work together to build a common language for the business areas being developed. There’s no us versus them; it’s always us. Developing software is a business investment and not just a cost, and the effort involved in building the Ubiquitous Language helps spread deep Domain insight among all team members.
2. **Strategic Design:** Domain-Driven Design addresses the strategy behind the direction of the business and not just the technical aspects. It helps define the internal relationships and early warning feedback systems. On the technical side, Strategic Design protects each business service by encouraging service-oriented architecture best practices.
3. **Tactical Design**: Domain-Driven Design provides the tools and the building blocks for iterative software deliverables. Tactical Design tools produce software that’s not only correct, but also testable and less error prone.

### Ubiquitous Language

The Ubiquitous Language is the common business language, and it has a meaning within the limits of a specific business context. This specific context is known as a Bounded Context, which is a pattern relating to Strategic Design. These two concepts are central to Domain-Driven Design.

For now, think of a Bounded Context as a conceptual boundary around a system, while the Ubiquitous Language inside a boundary has a specific contextual meaning. Meanwhile, concepts outside of this context can have different meanings.

So, how to find, explore, and capture this precise language?

- Identify key business processes, their inputs, and their outputs.
- Create a glossary of terms and definitions.
- Capture important software concepts with some kind of documentation.
- Share and expand upon the collected knowledge with the rest of the team (Developers and Domain Experts).

Since Domain-Driven Design was born, new techniques for improving the process of building the Ubiquitous Language have emerged. The most important one, which is used regularly now, is EventStorming.

#### EventStorming

EventStorming is a workshop format for quickly exploring complex business domains.

- **It is powerful:** it allows practitioners to come up with a comprehensive model of complete business flow in hours instead of weeks.
- **It is engaging:** the whole idea is to bring people with the questions and people who know the answer in the same room and to build a model together.
- **It is efficient:** the resulting model is perfectly aligned with a Domain-Driven Design implementation style (particularly fitting an Event Sourcing approach) and allows for a quick determination of Context and Aggregate boundaries.
- **It is easy:** the notation is ultra-simple. No complex UML might cut off participants from the heart of the discussion.
- **It is fun:** I always had a great time leading the workshops, people are energized and deliver more than they expected. The right questions arise, and the atmosphere is the right one.

### Strategic Design

To provide a general overview of the strategic side of Domain-Driven Design, we’ll use an approach to Consider two different spaces: the problem space and the solution space.

In the problem space, Domain-Driven Design uses Domains and Subdomains to group and organize what companies want to solve.

**\*\*Example\*\***

In the solution space, Domain-Driven Design provides two patterns: Bounded Contexts and Context Maps. The goal is to define how to provide an implementation to all the identified Subdomains by defining their interactions and the details of those interactions. Each of the Subdomains will be solved with a Bounded Context implementation. The Context Map will show how each Bounded Context is related to the rest. Inside the Context Map, we can see what type of relation two Bounded Contexts have. The ideal approach is to have each Subdomain implemented by one Bounded Context, but that’s not always possible.

**\*\*Example \*\***

In terms of implementation, when following Domain-Driven Design, you’ll end up with distributed architectures. As you may already know, distributed architectures are more complex than monolithic ones, so why is this approach attractive, especially for big and complex companies? Is it really worth it?

Well, distributed architectures are proven to increase overall company productivity because they define boundaries for your product that can be developed by focused teams. So note that if your Domain — the problem you need to solve — isn’t complex, applying the strategical part of Domain-Driven Design can add unnecessary overhead and slow down your development speed. As such, it’s important to make sure that Domain-Driven Design is what your business really needs.

### Tactical Design

Once the strategic part is clear, it’s time to jump into the implementation. Domain-Driven Design identifies a set of Design Patterns and Architectural Styles that help us pull our Domain Model into code. These building blocks are useful when writing code as part of a specific Bounded Context. In terms of software architecture, each Bounded Context can be implemented as a single service, an Application, or a set of microservices that communicate with each other. When it comes to implementing one of these services, two main Architectural Styles fit pretty well with Domain- Driven Design: Hexagonal Architecture — also known as Ports and Adapters — and Event Sourcing with CQRS.

Command-Query Responsibility Segregation (CQRS) is one of the suggested Architectural Styles in Domain-Driven Design, together with Hexagonal Architecture and Event Sourcing. CQRS is mostly used alongside Event Sourcing; however, it can be used independent of it.

Moving from the architecture to a more detailed implementation, Domain-Driven Design focuses on a set of Design Patterns that support the Domain Model in code. Using these patterns will make it easier to write the code as the Ubiquitous Language of the Domain. Let’s take a closer look:

- **Value Objects:** Objects that describe, measure, or quantify. They’re identified by the values they contain. Examples may be an email address, a product height, a quantity of money, or a price.
- **Entities:** Objects that represent the main elements in a Domain. They’re identified by a unique ID and contain the main business logic of an Application. Examples may be a user, a product, an order, or an invoice.
- **Factories:** Objects that build other objects in the Domain Model.
- **Repositories:** Objects that fetch and store Entities.
- **Domain Services:** Objects that contain business logic that isn’t related to a specific Entity - for example, a payment service.
- **Domain Events**: Objects that represent things that happen in a Domain that are interesting for the business. Examples may be OrderPlaced, UserSignedIn, or DataExportRequested.
- **Aggregates:** Objects like Entities that contain other Entities that are required to be persisted and retrieved in the same transaction. For example, an invoice with all the invoice lines, taxes, and discounts.
- **Application Services or Command Handlers:** Objects that represent the high-level use cases of an Application and orchestrate the steps to fulfill the business requirements. Examples may include RegisterNewCustomer or DisableProduct.

## Considering Domain-Driven Design

Domain-Driven Design isn’t a silver bullet; as with everything in software, it depends on the context. As a rule of thumb, use it to simplify your Domain, but never to add more complexity.

If your Application is data-centric and your use cases mainly manipulate rows in a database and perform CRUD operations — that is, Create, Read, Update, and Delete — you don’t need Domain-Driven Design. Instead, the only thing your company needs is a fancy user interface (UI) in front of your database.

If your Application has less than 30 use cases, it might be simpler to use a framework ASP.NET Core to handle your business logic.

However, if your Application has more than 30 use cases, your system may be moving toward the dreaded “Big Ball of Mud” If you know for sure your system will grow in complexity, you should consider using Domain-Driven Design to fight that complexity.

If you know your Application is going to grow and is likely to change often, Domain-Driven Design will help in managing the complexity and when refactoring your Model over time.

If you don’t understand the Domain you’re working on because it’s new and nobody has invested in a solution before, this might mean it’s complex enough for you to start applying Domain-Driven Design. In this case, you’ll need to work closely with Domain Experts to get the Models right.

## The Tricky Parts

Applying Domain-Driven Design isn’t easy. It requires time and effort to get around the Business Domain and terminology. It also requires a lot of research, and as mentioned above, you’ll need to involve Domain Experts in the process too. Such a commitment will require an open and healthy continuous conversation to model spoken language in the software. On top of that, you’ll have to make an effort to think in the Ubiquitous Language and understand the relationships between objects before getting into the technical implementation of things.

## Wrapup

Domain-Driven Design is an approach that helps build Software Models that solve complex business problems within a specific Domain. It’s organized into two big blocks: Strategic Design and Tactical Design. Strategic Design provides tools to model the current organization of your Applications and services, how these Applications relate to each other, and which business problem they solve individually. Tactical Design provides a set of useful patterns to model the software for each Application. CQRS leverages Domain-Driven Design Tactical Patterns to optimize the Applications you develop for easy composition, high semantic value, testability, and high performance.
