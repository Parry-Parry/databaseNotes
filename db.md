# Database Systems Notes
## Lecture 1
### Slides
#### CONTEXTUAL DATABASE

**Observations** : human activity is data\-driven, i.e., we are making decisions, proceeding with actions and reasoning based on observed data
**Observation** : we are limited in storing all data in our memory and recall them

**Idea** : Define a robust basethat can store humongous data, update and delete data, and recall/ search data efficiently

_A database holds data relevant to our current contextual activity:_
- **Web Search** : a database with web page links
- **Data Mining** : a database managing multidimensional data for discovering patterns, outliers, novel trends, prediction and classification e.g Google database e.g UCI ML Repository
- **Scientific/Medical databases** : used for drug discovery, health monitoring and viruses analytics e.g MEDLINE
- **Customer/Retail database** : used for customers profilesand preferences, products e.g Amazon Database

#### DATA MANAGEMENT SYSTEM

_The fundamental functionality is to provide software to:_
- **model data** : relational data modeling, object-oriented data modeling, first-order logic data modeling, description logics data modeling, fuzzy logic modeling...
- **access data** : query for data, insert, delete and update
- **analyze data** : complex aggregation queries, function approximation, histograms, multi-dimensional visualization, outliers detection, ...
- **store \(physically\) data** : from memory to hard disks
- **secure data** : control access to sensitive & confidential data, cipher / encode data

_maintain data consistency in the face of_
- **failures** : think of machine crashes due to software bugs, power cuts, disk crashes
- recovery from failures

_optimize data access to efficiently retrieve data_
- index and hashing data structures: fast access to data
- optimization algorithms

_A **box** with an interface for users/applications offering the discussed functionality_
- Data Modelling
- Declarative Programming Language \(SQL\) to manage & query data

**Declarative** : we tell the database what to do and not how to do a task

_Refer to page 6 of DATABASE FUNDAMENTALS & RELATIONAL MODEL for a diagram of user queries and a diagram of of a database system_

#### DATA

_Distinguish three families of data:_
- **Structured data** : well-defined data structure, e.g., tables
- **Unstructured data** : e.g., web pages, texts, sensor measurements. Less information is provided on interpreting the data 
- **Semi\-structured data** : e.g., XML or JSON documents

_datum_ : a piece of data

_meta-data_ : data on other data e.g a measurement

_Self-descriptive data_ : they interpret themselves \(medium entropy\)

_Modern DMSs manage all families of data: documents, graphs, multimedia content..._

#### CONCEPTUAL DATA MODELLING
 
**Challenge** : transforma textual description of a real problem into a set of concepts conveying exactly the same information

_Entity-Relationship Modeling_ : Does not guarantee optimality in operations and query executions

_Relational Modeling:_
- Mathematics-driven: foundation of relational algebra, set theory, functional dependency theory
- Guarantees query optimization

**Conceptual Data Model** : A mathematical model for interpreting our data

_Why mathematical model?_ : theorems from: set theory, functional dependency & normalization theory, and relational algebra

_Why interpretation:_
- need to understand the context
- Which are the entities? e.g., bank accounts; students; employees ...
- Which are the attributes \(characteristics\) of a data entity? e.g., name; address; ID ...
- Which are the relationships between entities? e.g., an employee works in a department; a student attends many courses? 

#### RELATIONAL CONCEPTUAL MODEL

Informally, any entity might relate with any other entity when they both share common attributes

_Basically foreign keys_

#### RELATIONAL MODEL

_Any entity and any relationship are modelled as a relation, which maps to a 2-dimensional table:_
- an ordered set of attributes \(columns\)
- a set of tuples \(rows\), which represents instances
- There exists a specific attribute that uniquely identifies a tuple in the relation e.g sequential numbers or logical values like an ID

**Query** : attributes of interest to be retrieved, and constrained attributes to filter out irrelevant tuples

#### RELATIONAL MODEL: FORMALISM

**Schema of a Relation** : R\(A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>\)
- Relation with name R and an ordered set of attributes: A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>
- Each attribute A<sub>i</sub> assumes values in a domain D<sub>i</sub>

A tuple t of R is an ordered set of values corresponding to attributes of R satisfying the domain constraints: 
t = \(v<sub>1</sub>, v<sub>2</sub>, ..., v<sub>n</sub>\) in D<sub>i</sub>

An instance r\(R\) is a set of tuples:
r\(R\) = \{t<sub>1</sub>, t<sub>2</sub>, ..., t<sub>m</sub>,\}: t<sub>i</sub> is a tuple of R

**NULL:** : represents an unknown, or inapplicable, or uncertain, or missing value

**Relational Database Schema** : set of relations
S = \{R<sub>1</sub>, R<sub>2</sub>, ..., R<sub>k</sub>\} UNION NULL

#### RELATIONAL MODEL: COMPANY 

_A **company** is organized into **departments**. Each department has a unique number, and a particular **employee** who manages the department_
- We keep track of the start date that employee began managing the department

- A department may have several locations
- A department controls a number of **projects**, each of which has a unique name, number and a single location

_The company stores the information about the employee\(e.g., name, salary, birth date, ...\), and the unique social security number. An employee is assigned only to one department, but may work on several projects, which are not necessarily controlled by the same department_
- We keep track of the current number of hours per week that an employee works on each project and their direct supervisor, who is another employee

- The company keeps track of the **dependent**\(e.g., child\) of each employee for insurance purposes and the corresponding relationship with the employee \(e.g., son, daughter\)

**Schema**
_Schema_ : Company

_Entities:_
- Department
- Employee
- Project
- Dependent

_Relationships:_
- An employee manages a department
- A department may have several locations
- A department controls a number of projects
- An employee is assigned only to one department
- An employee may work on several projects \(for each, store hours per week\), which are not necessarily controlled by the same department
- A department controls several projects 
- An employee is supervised by a supervisor, who is another employee
- An employee has several dependents, each one corresponding to a specific relationship with the employee

#### RELATIONAL CONSTRAINTS

Conditions that must hold on all instances, for each relation

_Distinguish three fundamental constraints:_
- **Key constraint** : unique tuple identification
- **Entity integrity constraint** : keys are never null
- **Referential integrity constraint** : interpretation of relationships

#### ENTITY INTEGRITY CONSTRAINT

**Principle: Primary Key** : cannot be NULL in anytuple of instance r\(R\)

- If PK has several attributes, NULL is not allowed in any of these attributes
- If \{student-id, course-id\} is a composite PK then:student-id cannot be NULL and course-id cannot be NULL

_Note: There might be non-key attributes which are not allowed to be NULL, e.g., Employee’s surname specified by the database designer, e.g., unique value_

#### REFERENTIAL INTEGRITY CONSTRAINT

**Roles** : referencing relation R1 and referenced relation R2

There exists an attribute Foreign Key \(FK\) in R1 that either has exactly the same value with the Primary Key \(PK\) in R2 or is NULL

If t1\[FK\] = NULL then the FK in R1 should not be a part of its own primary key \(not violating the entity integrity constraint\)

**Notation** : directed arc from R1.FK to R2.PK 

#### SO FAR...

**Superkey** : is used to uniquely identify a tuple in a relation
- **Lemma** : If K is a superkey, then any superset of K is a superkey

**Candidate Key** : the minimal superkey: i.e., K is a candidate key if there is no subset of K that is also a superkey

_A relation can have several different candidate keys; one of them is chosen to be the Primary Key \(PK\)_

**Foreign Key \(FK\)** : In a referencing relation should either be NULL\(if it is not part of the primary key\) or have a value of the primary key of the referenced relation

## Fundamentals of Database Systems
### Chapter 2 : Database System Concepts and Architecture

#### Data Models, Schemas and Instances

**DBMS** : DataBase Management System, a software package designed to define, manipulate, retrieve and manage data in a database

Current _cloud computing_ environments consist of thousands of large servers managing so\-called _big data_.

**Client Module:** 
- Designed to run on a mobile device, user workstation or PC
- Applications and user interfaces that access a database run on this module
- Handles user interaction and provides user\-friendly interfaces 

**Server Module**
- Handles data storage, access and search etc.

**Data Abstraction**
- The supression of details of data organization and storage
- The highlighting of the essential features for an improved understanding of data

**Data model** : a collection of concepts that can be used to describe the structure of a database, provides the means for data abstraction

_Structure of a database_ : data types, relationships and constraints that apply to data

**Basic operations** : Specify retrieval and updates on a database

**Dynamic aspect** : set of valid user\-defined operations, other generic operations such as delete and modiy are often oncluded in the _basic data model operations_

**Stored procedures** : Persistent stored modules to attach behaviours to relations within a database

**High\-level / conceptual data models** : provides concepts close to the way users percieve data

**low\-level / physical data models** : provides concepts that describe the details of how data is stored on the computer storage media

**Representational / implementation data models** : provides concepts which may be easily understood by end users but are not far\-removed from how data organized in computer storage

**entity** : represents a real world object or concept

**attribute** : represents a property of interest that further describes an entity

**relationship** : represents an association among entities

**Entity\-relationship model** : high\-level conceptual model 

**Record\-based data models** : represent data by using record structures

**Physical data models** : describe how data is stored as files in the computer by representing information such as record formats , record orderings and access paths

**Access path** : a search structure that makes the search for particular database records efficient, such as indexing or hashing

**index** : an access path that allows direct access to data using an index term or keyword

**self\-describing data models** : combines the description of data with the data values themselves 

_In traditional models the schema is seperate from the data e.g XML and NOSQL systems_

**Schema diagram** : displayed schema

**Schema construct** : an object in the schema

_A schema diagram displays only some aspects of a schema, it may not show data types or relationships between files_

**Database state / Snapshot** : The data in a database at a particular moment in time

**Defining a database**
- specify schema
- with just a schema this is considered the _empty state_
- when we populate the database initially this is known as the _initial state_
- at any point in time the database has a _current state_
- A DBMS is partly responsible for ensuring that every state is a _valid state_

_A database state is called an **extension** of the schema_

**Schema evolution** : Modifying the schema as application requirements change

#### Three\-Schema Architecture and Data Independence

**Important characteristics of the database approach**
- use of a catalog to store the schema as to make it self\-describing
- insulation of programs and data
- support of multiple user views

**Three\-Schema Architecture** : separates the user applications from the physical database

_In this architecture schema can be defined on three levels:_
- **Internal level** : describes the physical storage structure of the database, uses a physical data model and describes the complete details of data storage and access paths
- **Conceptual level** : describes the structure of the whole database, it hides tge details of physical storage structures and concentrates on the entities, data types, relationships, user operations and constraints. _Usually described by a representational model_
- **External / View level** : A number of external schemas or user views, each external schema describes the part of the database a particular user group is interested in. _Usually described by a representational model_

**Mapping** : the process of transforming requests and results between levels

**Data independence** : the capacity to change the schema at one level of a database system without having to change the schema at the next higher level

_We can describe two types of data independence:_
- **Logical data independence** : the capacity to change the conceptual schema without having to change the external schemas or application programs, this can be done to expand the database to change constraints or to reduce the database i.e removing a record type or data item
- **Physical dat independence** : the capacity to change the internal schema without having to change the conceptual schema. Changes to the internal schema may have to occur because physical files may have been reorganized

#### Database Languages and Interfaces

_The DBMS must provide appropriate languages and interfaces for each category of users._

**DDL** : Data Definition Language, where no strict separation of levels is maintained one language can be used to define both schemas

**SDL** : Storage Definition Language, used to specify the internal schema, the mapping between schemas can be done in either of these languages

**VDL** : View Definition Language, specifies user views and mappings to the conceptual schema, in most DBMSs the DDL is used to define both conceptual and external schemas

_In relational DBMSs, SQL is used in the role of VDL_

**DML** : Data Manipulation Language, provides means to manipulate the database such as retrieval, insertion, deletion and modification of data

_In current DBMSs these languages are not usually distinct from on another_

**High\-level DML** : can be used on its own to concisely specify complex database operations, statements can be entered from a display, terminal or within an embedded programming language

**Low\-level / Procedural DML** : _must_ be embedded in a general purpose language, typically retrieves individual records or objects and processes them seperately

**Host language** : the general purpose language used to enter DML statements

**Data sublanguage** : DML statements

**Query language** : high\-level DML used in a standalone interactive manner

#### DBMS Interfaces

**Menu-based Interfaces** : presents the user with a list of options that lead the user through the formulation of a request

**Apps for Mobile Devices** : presents mobile users with access to their data providing a limited menu of options

**Form-based interfaces** : allows users to fill out form entries to insert new data or fill out certain entries to retrieve matching data

_Form specification language_ : special languages that help programmers specify forms e.g SQL\*, Oracle Forms

**Graphical user interfaces** : typically displays a schema in diagrammatic form, the user can then specify a query by manipulating the diagram

**Natural language interfaces** : accept requests written in English or another language and attempts to understand them, if this fails a dialogue can be entered with the user to clarify a request

**Keyword\-based Database Search** : similar to web search engines, they use predefined indexes on words and use ranking functions to retriev and present documents in a decreasing degree of match

**Speech input and output** : use of speech as an input query and an answer to a question is now commonplace. Input is detected using a library of predefined words and used to set up parameters passed to a query, output is similarly converted

**Interfaces for Parametric Users** : parametric users such as bank tellers often have a small set of operations they must perform repeatedly so a special interface for each user group is designed and implemented to minimise keystrokes required for each request

**Interfaces for the DBA** : most databases contain privileged commands that can only be used by the DBA staff including commands for creating accounts, setting system parameters, authorizing accoutns, changing schema and reorganizing storage structures.

#### The Database Environment

**Operating system** : schedules disk read/write

**buffer management** : within DBMS, schedules read/write as buffer storage management has considerable performance impact

**stored data manager** : higher\-level module of DBMS that controls access to DBMS information stored on disk that is part of the database or catalog

_DDL compiler processes schema definitions and stores meta data in the DBMS catalog_

**interactive query** : interface for data interaction aimed towards casual users

**query compiler** : validates query input

**query optimizer** : rearranges queries to eliminate redundancies and allows for efficient search algorithms. It consults the system catalog for physical information about the data and generates code that performs the necessary operations

_Programs written in a host language are submitted to a precompiler_

**precompiler** : extracts DML commands from an application program and sends them to the compiler, the rest of the program is sent to the host language compiler

**Runtime data processor**
- executes privilidged commands
- exectutable query plans
- canned transactions with runtime parameters

_transaction_ : a set opf operations on the database

The runtime data processor works with the system catalog and may provide statistics, it also works with the stored data manager which in turn uses basic system services for carrying out low\-level read/write. It also handles management of buffers on the main memory

_concurrency control and backup and recovery systems are integrated_

The **client program** accesses the DBMS on a seperate computer to the system on which the database resides. The former is called the **client computer** running DBMS client software and the latter is called the **database server**. In many cases the client accesses a middle computer called the **application server** which in turn accesses the database server.

#### Database System Utilities

- **Loading** : a loading utility is used to load existing data files into the database, data is often reformated for the DBMS and some vendors offer conversion tools to move these files between DBMSs

- **Backup** : a backup utility creates a backup copy of the database usually by dumping the entire database onto tape or other mass storage medium. Incremental backups are often used that only store changes from the last backup which save space but are more complex

- **Database Storage Reorganization** : This utility can be used to reorganize a set of database files into different file organizations and create new access paths to improve performance

- **Performance Monitoring** : Such a utility monitors database usage and provides statistics to the DBA. This aids decisions such as whether or not to reorganize files or whether to add or drop indexes to improve performance

_Other utilities may be availible for sorting, handling compression, access monitoring, interfacing with the network and other functions_

#### Tools, Application Enviroments and Communications Facilities

**Data dictionary** : stores catalog information about schemas and constraints aswell as design decisions, usage standards, application program descriptions and user information, also known as an **information repository**

**Application development environments** : provide an environment for creatign database applications and include facilities that help on many facets of database systems including design, GUI development, querying and updating, and application program development

**communications software** : interfaces with the DBMS to allow users at remote locations to access the database through terminals. The integration of these systems with the DBMS is called a DB/DC system

#### Centralized and Client/Server Architecture for DBBMs

_See page 77 for a physical centralized architecture diagram_

**client/server architecture** : developed to deal with environments in which a large number of PCs, workstations and servers are connected via a network

**specialized server** : a server with a specific functionality e.g file servers, printer servers, web servers or e\-mail servers

_A client machine provides the user with the appropriate interfaces to utilize these servers._

#### Two-Tier Client/Server Architecture for DBMSs

**RDBMS** : Relational Database Management System

_In this architecture the server is often called a **query / transaction server** because it provides these two functionalities_

**ODBC** : Open DataBase Connectivity, a standard that provides an API which allows client\-side programs to call the DBMS

_This architecture is named as such because software components are split between the client and server_

#### Three\-Tier and _n_\-Tier Architectures for Web Applications

_In these architectures intermediate stages are added beween the client and database server know as **Application or Web servers**_

This server runs application programs and stores procedures or constraints that are used to to check access from the database server. It can also improve database security by checking client credentials before forwarding a request to the database server.

In _n_\-tier architectures these layers are divided more finely allowing for each system to run on approprite processors or OSs and can be handled independently.

Advances in encryption have made it safer to transfer data from server to the client but network security issues remain a major concern.

#### Classification of Database Management Systems

Big data systems are also known as key\-value storage systems or NOSQL systems and use various data models:
- document\-based
- graph\-based
- column\-based
- key\-value data models

**Object\-relational DBMS** : based on object databases

XML : eXtended Markup Language : a _tree\-structured data model_

DBMSs can be categorized:
- the number of concurrent users allowed
- the number of sites over which the database is distributed, a centralized DBMS is stored on a single computer site but does allow multiple users, a distributed DBMS can have the database and software distributed over many sites on a network, data is often replicated to prevent loss of data availibility in the event of a site failure.

**Homogeneous** : same DBMS software on all sites
**Heterogenous** : can use different software at each site

**Federated DBMS** : loosely coupled DBMSs with a degree of local autonomy

- it is difficult to propose a classification of DBMSs by cost, we have open source products like MySQL and PostgreSQL aswell as giant systems sold in modular form with components to handle distribution, replication, parallel processing, mobile capacity etc.

_These paid systems are often licensed with limits on database copies and concurrent accesses_

**General purpose DBMS** : functions across a variety of applications
**Speciality DBMS** : tailored performance to a specific application

**Object Data Model**
- Objects with the same structure and behaviour belong to a _class_
- Classes are organized into _hierarchies_
- Operations of of each class are defined in terms of predefined features called _methods_

**Big Data Systems**
- **key\-value data model** : associates a unique key with each value and provides fast access when given a key
- **document data model** : based on JSON and stores data as documents which somewhat resemble complex objects
- **graph data model** : stores objects as graph nodes and relationships among objects as directed graph edges
- **column\-based data model** : store columns of rows clustered on disk pages for fast access and allow multiple versions of the data

**The XML Model**
- standard for exchanging data ove the web
- uses hierarchical tree structure combining database concepts with concepts from document representation models
- data is represented as elements with the use of tags
- data can be nested to create compx tree structures

**network model** : represents data as record types. A 1:n relationship relates one instance of a record to many record instances called a set type

**hierarchical model** : represents data as hierarchical tree structures with each structure representing a number of related records 
### Chapter 5