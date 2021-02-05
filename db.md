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

### Chapter 5: The Relational Database Model and Relational Database Constraints

_mathematical relation_ : a table of vlaues with its theorectical basis in set theory and predicate logic

#### Relational Model Concepts

**flat file** : model with each record following a simple linear or _flat_ structure

**domain** : set of atomic values

_atomic_ : each value in the domain is indivisible as far as the relational model is concerned 

_a data type is specified for each domain_

**degree of a relation** : number of attributes of its schema

**relational intension** : the schema

**relation extension** : the relation of the schema

_A relation is a mathematical relation on domains which is a subset of the Cartesian product_

**Cartesian product** : total number of tuples in a relation state

_Attribute names indicate different roles of a domain e.g list of all phone numbers and a home phone attribute_

#### Characteristics of Relations

**Ordering of Tuples in a Relation**
- A relation is defined as a set of tuples
- elements of a set have no order
- records are physically stored on a disc so there is always an order among records

**self\-describing data** : description of each value is included in the tuple

**Values and NULLS in Tuples**
- each value in a tuple is an atomic value
- composite and multiple attributes are not allowed
- NULL is used to represent values that are unknown or do not apply to a tuple

**NULL can mean:**
- value unknown
- value exists but is unavailible
- attribute does not apply
- exact meaning in context is found by comparisons to other values

_Do not compare two NULL values_ 

_Relations may represent:_
- facts about entities
- facts about relationships

_Interpreting relational schema as a **predicate**_
- values in each tuple are interpreted as values that satify the predicate
- an assumption called the **closed world assumption** states that the only true facts in the universe are those present within the extension of the relation\(s\)

**Relational Model Notation**
- Relational schema _R_ of degree _n_ is denoted by R\(A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>\)
- The uppercase letters _Q, R, S_ denote relation names
- The lowercase letters _q, r, s_ denote relation states
- The letters _t, u, v_ denote tuples
- The name of a relational schema e.g STUDENT generally indicates the current set of tuples in that relation \- the _current relation state_
- An attribute _A_ can be qualified with the relation name _R_ to which it belongs by using the dot notation _R.A_, all attribute names in a particular relation must be distinct
- An _n_\-tuple in a relation _r\(R\_ is denoted by t = <\v<sub>1</sub>, v<sub>2</sub>, ..., v<sub>n</sub>> where v<sub>i</sub> is the value corresponding to attribute A<sub>i</sub> 
- Both t\[A<sub>i</sub>\] and t.A<sub>i</sub> refer to the value v<sub>i</sub> in t for the attribute A<sub>i</sub>
- Both t\[A<sub>u</sub>, A<sub>w</sub>, ..., A<sub>z</sub>\] and t.\(A<sub>u</sub>, A<sub>w</sub>, ..., A<sub>z</sub>\) refer to the subtuple of values <A<sub>u</sub>, A<sub>w</sub>, ..., A<sub>z</sub>> from t corresponding to the attributes specified in the list

#### Relational Model Constraints and Relational Database Schemas

**Constraints on databases can generally be divided into three main categories:**
- **inherent model\-based constraints** : constraints that are inherent to the data model
- **schema\-based constraints** : constraints that can be directly expressed in the schemas of the data model typically by specifyingthem in the DDL
- **semantic / application\-based constraints** : constraints that cannot be directly expressed in the schemas of the data model and hence must be expressed and enforced by the application programs

#### Domain Constraints 

_Domain constraints specify that within each tuple, the value of each attribute A must be an atomic valie from the domain dom\(A\). Domains can be describe by standard data types or by a subrange of values fro ma data type or as an enumerated data type._ 

#### Key Constraints and Constraints on NULL Values 

**subsets of attributes** : property that no two tuples in any relation state _r_ of R should have the same combination of values for those attributes

**Superkey** : specifies a uniqueness contraint that no distinct tuples in any state _r_ of R can have the same value for superkey
- every realtion has at least one default superkey
- a superkey can have redundant attributes 

**key** : a key k of relation schema R is a superkey of R with the additional property that removing any attribute A form K leaves a set of attributes K' that is not a superkey of R anymore

_A key satisfies two properties:_
- Two distinct tuples in any state of the relation cannot have indentical values for all attributes in the key
- It is a minimal superkey \- that is, a superkey from which we cannot remove any attributes and still have the uniqueness constrain hold

_every key is a superkey but not vice versa_

_a key is determined form the meaning of the attributes and is time\-invariant, it must continue to hold when we insert new tuples_

A relation schema may have more than one key. In this case, each of the keys is called a candidate key. It is common to designate one of the candidate keys as a primary key used to identify tuples in the relation, others are designated unique keys.

#### Relational Databases and Relational Database Schemas 

**relational database schema** : A set of relation schemas and a set of integrity constraints 

#### Entity Integrity, Referential Integrity and Foreign Keys

**referential integrity constraint** : specified between two relations and is used to maintain the consistency among tuples in the two relations

**Foreign Keys**
- The attributes in FK have the same domain\(s\) as the primary key attributes PK of R<sub>2</sub> ; the attributes FK are said to reference or refer to the relation R<sub>2</sub>
- A value of FK in a tuple t<sub>1</sub> of the current state r<sub>1</sub>\(R<sub>1</sub>\) either occurs as a value of PK for some tuple t<sub>2</sub> in the current state r<sub>2</sub>\(R<sub>2</sub>\) or is NULL. In the former case, we have t<sub>1</sub>\[FK\] = t<sub>2</sub>\[PK\], and we say that the tuple t<sub>1</sub> references or refers to the tuple t<sub>2</sub> 

_In this definition, R<sub>1</sub> is called the referencing relation and R<sub>2</sub> is the referenced relation_

_A foreign key can refer to its own relation_

We can diagrammatically display referential integrity constraints by drawing a directed arc from each foreign key to the relation it references. For clarity, the arrowhead may point to the primary key of the referenced relation.

All integrity constraints should be specified on the relational database schema if we want the DBMS to enforce these constraints. Hence, the DDL includes provisions for specifying the various types of constraints so that the DBMS can automatically enforce them.

#### Other Types of Constraints

**semantic integrity constraints** : enforced within the application programs. It is more common to check for these types of constraints within the application programs than to use constraint specification languages because the latter are sometimes difficult and complex to use

#### Update Operations, Transactions, and Dealing with Constraint Violations

**result relation** : becomes the answer to \(or result of \) the user’s query

**Basic Operations**
- **Insert** : insert one or more new tuples
- **Delete** : deletes tuples
- **Update** : used to change the values of some attributes in existing tuples

The Insert operation provides a list of attribute values for a new tuple t that is to be inserted into a relation R . Insert can violate any of the four types of constraints. Domain constraints can be violated if an attribute value is given that does not appear in the corresponding domain or is not of the appropriate data type. Key constraints can be violated if a key value in the new tuple t already exists in another tuple in the relation r \( R \). Entity integrity can be violated if any part of the primary key of the new tuple t is NULL . Referential integrity can be violated if the value of any foreign key in t refers to a tuple that does not exist in the referenced relation.

The Delete operation can violate only referential integrity. This occurs if the tuple being deleted is referenced by foreign keys from other tuples in the database. To specify deletion, a condition on the attributes of the relation selects the tuple \(or tuples\) to be deleted.

**Options if deletion cause violation**
- **restrict** : rejects the deletion
- **cascade** : attempt to propagate the deletion by deleting tuples that reference the deleted tuple
- **set NULL** : modify the affected attributes to NULL or reference a valid tuple, cannot occur if the violation is part of a primary key

The Update \(or Modify\) operation is used to change the values of one or more attributes in a tuple \(or tuples\) of some relation R . It is necessary to specify a condition on the attributes of the relation to select the tuple \(or tuples\) to be modified.

_Updating an attribute that is neither part of a primary key nor part of a foreign key usually causes no problems, if a foreign key is modified the DBMS must make sure that the new value refers to an existing tuple in the referenced relation \(or is set to NULL\)._

#### The Transaction Concept

**Transaction** : an executing program that includes some database operations, such as reading from the database, or applying insertions, deletions, or updates to the database
- At the end of the transaction, it must leave the database in a valid or consistent state that satisfies all the constraints specified on the database schema 
- A single transaction may involve any number of retrieval operations and any number of update operations 
- These retrievals and updates will together form an atomic unit of work against the database

**online transaction processing (OLTP )** : commercial applications running against relational databases that execute transactions at rates that reach several hundred per second

## Database Systems: The Complete Book

### Chapter 1

**The Evolution of Database Systems**

_A DBMS is expected to:_
- Allow users to create new databases and specify their schemas
- Give users the ability to query the data (a “query” is database lingo for a question about the data) and modify the data, using an appropriate language
- Support the storage of very large amounts of data over a long period of time, allowing efficient access to the data for queries and database modifications
- Enable durability, the recovery of the database in the face of failures, errors of many kinds, or intentional misuse
- Control access to data from many users at once, without allowing unexpected interactions among users \(called isolation\) and without actions on the data to be performed partially but not completely \(called atomicity\)

#### Early Database Systems

**First Important Applications of DBMSs:**
- **Banking systems** : maintaining accounts and making sure that system failures do not cause money to disappear
- **Airline reservation systems** : these, like banking systems, require assurance that data will not be lost, and they must accept very large volumes of small actions by customers
- **Corporate record keeping** : employment and tax records, inventories, sales records, and a great variety of other types of information, much of it critical

_Early databases were modelled with tree\-based models and the graph\-based network model but did not support high\-level query languages_

#### Relational Database Systems

_Useless to repeat information._

#### Smaller and Smaller Systems

_DBMSs were:_
- large, expensive software systems
- run on large computers as to store a gigabyte required this

#### Bigger and Bigger Systems

**Examples of Large Databases:**
- Google holds petabytes of data gleaned from its crawl of the Web. This data is not held in a traditional DBMS, but in specialized structures optimized for search-engine queries
- Satellites send down petabytes of information for storage in specialized systems
- A picture is actually worth way more than a thousand words. You can store 1000 words in five or six thousand bytes. Storing a picture typically takes much more space. Repositories such as Flickr store millions of pictures and support search of those pictures. Even a database like Amazon’s has millions of pictures of products to serve
- And if still pictures consume space, movies consume much more. An hour of video requires at least a gigabyte. Sites such as YouTube hold hundreds of thousands, or millions, of movies and make them available easily
- Peer-to-peer file-sharing systems use large networks of conventional computers to store and distribute data of various kinds. Although each node in the network may only store a few hundred gigabytes, together the database they embody is enormous

#### Information Integration

**Information Integration** : joining the information contained in many related databases into a whole. For example, a large company has many divisions. Each division may have built its own database of products or employee records independently of other divisions

- These divisions may use different DBMS’s and different structures for information
- They may use different terms to mean the same thing or the same term to mean different things
- To make matters worse, the existence of legacy applications using each of these databases makes it almost impossible to scrap them, ever.

_As a result, it has become necessary with increasing frequency to build structures on top of existing databases._

One popular approach is the creation of data warehouses, where information from many legacy databases is copied periodically, with the appropriate translation, to a central database.

### Chapter 2 : Overview of a Database Management System

**Distinct sources of commands to a DBMS:**
- Conventional users and application programs that ask for data or modify data
- A **database administrator** : a person or persons responsible for the structure or schema of the database

#### Data\-Definition Language Commands

_The second kind of command is the simpler to process_

These schema\-altering data-definition language commands are parsed by a DDL processor and passed to the execution engine, which then goes through the index/file/record manager to alter the metadata

#### Overview of Query Processing

A user or an application program initiates some action, using the data-manipulation language. This command does not affect the schema of the database, but may affect the content of the database _if the action is  a modification command_ or will extract data from the database _if the action is a query_. DML statements are handled by two separate subsystems, as follows.

**Answering the Query**

- The query is parsed and optimized by a query compiler
- The resulting query plan, or sequence of actions the DBMS will perform to answer the query, is passed to the execution engine
- The execution engine issues a sequence of requests for small pieces of data, typically records or tuples of a relation, to a resource manager that knows about data files
- The requests for data are passed to the buffer manager
- The buffer manager’s task is to bring appropriate portions of the data from secondary storage where it is kept permanently, to the main-memory buffers

_Normally, the page or “disk block” is the unit of transfer between buffers and disk_

- The buffer manager communicates with a storage manager to get data from disk
- The storage manager might involve operating-system commands, but more typically, the DBMS issues commands directly to the disk controller

**Transaction Processing**

- Queries and other DML actions are grouped into transactions, which are units that must be executed atomically and in isolation from one another
- Any query or modification action can be a transaction by itself
- In addition, the execution of transactions must be **durable**, meaning that the effect of any completed transaction must be preserved even if the system fails in some way right after completion of the transaction

_Divisions of the transaction processor:_
- **concurrency-control manager / scheduler** : responsible for assuring atomicity and isolation of transactions
- **logging and recovery manager** : responsible for the durability of transactions

#### Storage and Buffer Management

- To perform any useful operation on data, that data must be in main memory
- It is the job of the **storage manager** to control the placement of data on disk and its movement between disk and main memory
- In a simple database system, the storage manager might be nothing more than the file system of the underlying operating system
- DBMS’s normally control storage on the disk directly, at least under some circumstances
- The storage manager keeps track of the location of files on the disk and obtains the block or blocks containing a file on request from the buffer manager
- The buffer manager is responsible for partitioning the available main memory into buffers

**Buffers** : page-sized regions into which disk blocks can be transferred

_Thus, all DBMS components that need information from the disk will interact with the buffers and the buffer manager, either directly or through the execution engine_

**Information needed by DBMS components**
- **Data** : the contents of the database itself
- **Metadata** : the database schema that describes the structure of, and constraints on, the database
- **Log Records** : information about recent changes to the database; these support durability of the database
- **Statistics** : information gathered and stored by the DBMS about data properties such as the sizes of, and values in, various relations or other components of the database
- **Indexes** : data structures that support efficient access to the data

#### Transaction Processing

**The transaction processor performs the following tasks:**
- **Logging** : In order to assure durability, every change in the database is logged separately on disk

_The log manager follows one of several policies designed to assure that no matter when a system failure or “crash” occurs, a recovery manager will be able to examine the log of changes and restore the database to some consistent state._

_The log manager initially writes the log in buffers and negotiates with the buffer manager to make sure that buffers are written to disk \(where data can survive a crash\) at appropriate times._

- **Concurrency control** : Transactions must appear to execute in isolation. But in most systems, there will in truth be many transactions executing at once

- The **scheduler \(concurrency-control manager\)** must assure that the individual actions of multiple transactions are executed in such an order that the net effect is the same as if the transactions had in fact executed in their entirety, one\-at\-a\-time

- A typical scheduler does its work by maintaining locks on certain pieces of the database

- These locks prevent two transactions from accessing the same piece of data in ways that interact badly

- **Deadlock resolution** : As transactions compete for resources through the locks that the scheduler grants, they can get into a situation where none can proceed because each needs something another transaction has

_The transaction manager has the responsibility to intervene and cancel \(“rollback” or “abort”\) one or more transactions to let the others proceed._

#### The Query Processor 

Portion of the DBMS that most affects the performance that the user sees, it can be divided into two main components.

**Query Compiler** : translates the query into an internal form called a query plan

_The query compiler consists of three major units:_
- **query parser** : builds a tree structure from the textual form of the query
- **query preprocessor** : performs semantic checks on the query and performing some tree transformations to turn the parse tree into a tree of algebraic operators representing the initial query plan
- **query optimizer** : transforms the initial query plan into the best available sequence of operations on the actual data

_The query compiler uses metadata and statistics about the data to decide which sequence of operations is likely to be the fastest_

**Execution Engine** : has the responsibility for executing each of the steps in the chosen query plan 
- The execution engine interacts with most of the other components of the DBMS, either directly or through the buffers
- It must get the data from the database into buffers in order to manipulate that data
- It needs to interact with the scheduler to avoid accessing data that is locked, and with the log manager to make sure that all database changes are properly logged

# Week 2
### Chapter 14: Basics of Functional Dependencies and Normalization for Relational Databases

There are two levels at which we can discuss the goodness of relation schemas:
- logical \(or conceptual\) level : how users interpret the relation schemas and the meaning of their attributes
- implementation \(or physical storage\) level : how the tuples in a base relation are stored and updated

_This level applies only to schemas of base relations— which will be physically stored as files— whereas at the logical level we are interested in schemas of both base relations and views \(virtual relations\)._

**bottom-up design methodology** : considers the basic relationships among individual attributes as the starting point and uses those to construct relation schemas

_This approach is not very popular in practice because it suffers from the problem of having to collect a large number of binary relationships among attributes as the starting point. For practical situations, it is next to impossible to capture binary relationships among all such pairs of attributes._

**top-down design methodology** 
- starts with a number of groupings of attributes into relations that exist together naturally, for example, on an invoice, a form, or a report
- The relations are then analyzed individually and collectively, leading to further decomposition until all desirable properties are met

Relational database design goals:
- information preservation : maintaining all concepts, including attribute types, entity types, and relationship types as well as generalization/specialization relationships
- minimum redundancy : implies minimizing redundant storage of the same information and reducing the need for multiple updates to maintain consistency across multiple copies of the same information in response to real-world events that require making an update

**functional dependency** : formal constraint among attributes that is the main tool for formally measuring the appropriateness of attribute groupings into relation schemas

#### Informal Design Guidelines for Relation Schemas

Measures to determine the quality of relation schema design:
- Making sure that the semantics of the attributes is clear in the schema
- Reducing the redundant information in tuples
- Reducing the NULL values in tuples
- Disallowing the possibility of generating spurious tuples

#### Imparting Clear Semantics to Attributes in Relations

**semantics** : a realtions meaning resulting from the interpretation of attribute values in a tuple

_The ease with which the meaning of a relation’s attributes can be explained is an informal measure of how well the relation is designed._

**Informal design guideline**

Guideline 1:
- Design a relation schema so that it is easy to explain its meaning. Do not combine attributes from multiple entity types and relationship types into a single relation
- Intuitively, if a relation schema corresponds to one entity type or one relationship type, it is straightforward to explain its meaning.
- Otherwise, if the relation corresponds to a mixture of multiple entities and relationships, semantic ambiguities will result and the relation cannot be easily explained.

#### Redundant Information in Tuples and Update Anomalies

- One goal of schema design is to minimize the storage space used by the base relations \(and hence the corresponding files\)
- Grouping attributes into relation schemas has a significant effect on storage space

Storing natural joins of base relations leads to an additional problem referred to as update anomalies . These can be classified into insertion anomalies, deletion anomalies, and modification anomalies:

- **Insertion anomalies** : Issues that arise when initialising new tuples when all details of a parent object must be entered though they are not known, e.g making an employee record consistent with a department. They also occur when trying to initialise a new object that as of yet has no children, so NULL values must be entered which may violate the primary key

- **Deletion anomalies** : The problem of deletion anomalies is related to the second insertion anomaly situation just discussed. When the last child of an object is deleted all of the information regarding that bject can be lost

- **Modification anomalies** : If one attribute of an object is modified in a child then all instances of that attribute must be updated across all children otherwise different values can occur for the same attribute

Guideline 2:
- Design the base relation schemas so that no insertion, deletion, or modification anomalies are present in the relations
- If any anomalies are present, note them clearly and make sure that the programs that update the database will operate correctly

_It is important to note that these guidelines may sometimes have to be violated in order to improve the performance of certain queries._

#### NULL Values in Tuples

- In some schema designs we may group many attributes together into a “fat” relation
- If many of the attributes do not apply to all tuples in the relation, we end up with many NULLs in those tuples
- This can waste space at the storage level and may also lead to problems with understanding the meaning of the attributes and with specifying JOIN operations at the logical level

NULLs can have multiple interpretations, such as the following:
- The attribute does not apply to this tuple. For example, Visa_status may not apply to U.S. students
- The attribute value for this tuple is unknown. For example, the Date_of_birth may be unknown for an employee
- The value is known but absent; that is, it has not been recorded yet. For example, the Home_Phone_Number for an employee may exist, but may not be available and recorded yet

Guideline 3:
- As far as possible, avoid placing attributes in a base relation whose values may frequently be NULL
- If NULLs are unavoidable, make sure that they apply in exceptional cases only and do not apply to a majority of tuples in the relation
- Using space efficiently and avoiding joins with NULL values are the two overriding criteria that determine whether to include the columns that may have NULLs in a relation or to have a separate relation for those columns

#### Generation of Spurious Tuples

**spurious tuples** : extra tuples created from a poorly designed relation using a JOIN operation that contain information that is not valid

Guideline 4:
- Design relation schemas so that they can be joined with equality conditions on attributes that are appropriately related pairs in a way that guarantees that no spurious tuples are generated
- Avoid relations that contain matching attributes that are not FK/PK combinations because joining on such attributes may produce spurious tuples

#### Summary and Discussion of Design Guidelines

Problems which can be detected without additional tools of analysis, are as follows:
- Anomalies that cause redundant work to be done during insertion into and modification of a relation, and that may cause accidental loss of information during a deletion from a relation
- Waste of storage space due to NULLs and the difficulty of performing selections, aggregation operations, and joins due to NULL values
- Generation of invalid and spurious data during joins on base relations with matched attributes that may not represent a proper FK/PK relationship

#### Functional Dependencies

The single most important concept in relational schema design theory is that of a functional dependency.

#### Definition of Functional Dependency

- A functional dependency is a constraint between two sets of attributes from the database

**Definition** : A functional dependency, denoted by X → Y , between two sets of attributes X and Y that are subsets of R specifies a constraint on the possible tuples that can form a relation state r of R. The constraint is that, for any two tuples t<sub>1</sub> and t<sub>2</sub> in r that have t<sub>1</sub>\[X\] = t<sub>2</sub>\[X\], they must also have t<sub>1</sub>\[Y\] = t<sub>2</sub>\[Y\]

- This means that the values of the Y component of a tuple in r depend on, or are determined by, the values of the X component; alternatively, the values of the X component of a tuple uniquely \(or functionally\) determine the values of the Y component
- We also say that there is a functional dependency from X to Y, or that Y is functionally dependent on X

Thus, X functionally determines Y in a relation schema R if, and only if, whenever two tuples of r\(R\) agree on their X\-value, they must necessarily agree on their Y\-value. 

Note the following:
- If a constraint on R states that there cannot be more than one tuple with a given X\-value in any relation instance r\(R\) — that is, X is a candidate key of R — this implies that X → Y for any subset of attributes Y of R \(because the key constraint implies that no two tuples in any legal state r\(R\) will have the same value of X\). If X is a candidate key of R , then X → R
- If X → Y in R, this does not say whether or not Y → X in R

Relation extensions r\(R\) that satisfy the functional dependency constraints are called legal relation states \(or legal extensions\) of R

- A functional dependency is a property of the relation schema R , not of a particular legal relation state r of R
- Therefore, an FD cannot be inferred automatically from a given relation extension r but must be defined explicitly by someone who knows the semantics of the attributes of R

- Given a populated relation, we cannot determine which FDs hold and which do not unless we know the meaning of and the relationships among the attributes. All we can say is that a certain FD may exist if it holds in that particular extension
- All we can say is that a certain FD may exist if it holds in that particular extension. We cannot guarantee its existence until we understand the meaning of the corresponding attributes
- We can, however, emphatically state that a certain FD does not hold if there are tuples that show the violation of such an FD

**diagrammatic notation**
- Each FD is displayed as a horizontal line
- The left\-hand\-side attributes of the FD are connected by vertical lines to the line representing the FD
- The right\-hand\-side attributes are connected by the lines with arrows pointing toward the attributes

#### Normal Forms Based on Primary Keys

We assume that a set of functional dependencies is given for each relation, and that each relation has a designated primary key; this information combined with the tests \(conditions\) for normal forms drives the normalization process for relational schema design

Most practical relational design projects take one of the following two approaches:
- Perform a conceptual schema design using a conceptual model such as ER or EER and map the conceptual design into a set of relations
- Design the relations based on external knowledge derived from an existing implementation of files or forms or reports

#### Normalization of Relations

- The normalization process takes a relation schema through a series of tests to certify whether it satisfies a certain normal form
- The process, which proceeds in a top\-down fashion by evaluating each relation against the criteria for normal forms and decomposing relations as necessary, can thus be considered as relational design by analysis

**normal form** : the highest normal form condition that it meets, and hence indicates the degree to which it has been normalized

Normalization of data can be considered a process of analyzing the given relation schemas based on their FDs and primary keys to achieve the desirable properties of:
- minimzing redundancy
- minimizing the insertion, deletion, and update anomalies. It can be considered as a “filtering” or “purification” process to make the design have successively better quality

The normalization procedure provides database designers with the following:
- A formal framework for analyzing relation schemas based on their keys and on the functional dependencies among their attributes
- A series of normal form tests that can be carried out on individual relation schemas so that the relational database can be normalized to any desired degree

Rather, the process of normalization through decomposition must also confirm the existence of additional properties that the relational schemas, taken together, should possess. 

These would include two properties:
- The nonadditive join or lossless join property , which guarantees that the spurious tuple generation problem does not occur with respect to the relation schemas created after decomposition
- The dependency preservation property, which ensures that each functional dependency is represented in some individual relation resulting after decomposition

_The nonadditive join property is extremely critical and must be achieved at any cost , whereas the dependency preservation property, although desirable, is sometimes sacrificed._

#### Practical Use of Normal Forms

- Most practical design projects in commercial and governmental environment acquire existing designs of databases from previous designs, from designs in legacy models, or from existing files
- They are certainly interested in assuring that the designs are good quality and sustainable over long periods of time
- Existing designs are evaluated by applying the tests for normal forms, and normalization is carried out in practice so that the resulting designs are of high quality and meet the desirable properties stated previously

_Another point worth noting is that the database designers need not normalize to the highest possible normal form and may do this for performance reasons._

**Denormalization** : storing the join of higher normal form relations as a base relation, which is in a lower normal form

#### Definitions of Keys and Attributes Participating in Keys

An attribute of relation schema R is called a prime attribute of R if it is a member of some candidate key of R . An attribute is called nonprime if it is not a prime attribute— that is, if it is not a member of any candidate key.

#### First Normal Form

- First normal form \(1NF\)is now considered to be part of the formal definition of a relation in the basic \(flat\) relational model; historically, it was defined to disallow multivalued attributes, composite attributes, and their combinations
- It states that the domain of an attribute must include only atomic values and that the value of any attribute in a tuple must be a single value from the domain of that attribute
- Hence, 1NF disallows having a set of values, a tuple of values, or a combination of both as an attribute value for a single tuple

First normal form also disallows multivalued attributes that are themselves composite. These are called nested relations because each tuple can have a relation within it.

**partial key** : within a nested relation each value of this attribute must be unique

#### Second Normal Form

Second normal form \(2NF\) is based on the concept of full functional dependency. A functional dependency X → Y is a full functional dependency if removal of any attribute A from X means that the dependency does not hold anymore.

**Definition** : A relation schema R is in 2NF if every nonprime attribute A in R is fully functionally dependent on the primary key of R

A functional dependency X → Y is a partial dependency if some attribute A ε X can be removed from X and the dependency still holds.

If a relation schema is not in 2NF, it can be second normalized or 2NF normalized into a number of 2NF relations in which nonprime attributes are associated only with the part of the primary key on which they are fully functionally dependent.

#### Third Normal Form

Third normal form \(3NF\) is based on the concept of transitive dependency . A functional dependency X → Y in a relation schema R is a transitive dependency if there exists a set of attributes Z in R that is neither a candidate key nor a subset of any key of R , 11 and both X → Z and Z → Y hold.

**Definition** : According to Codd’s original definition, a relation schema R is in 3NF if it satisfies 2NF and no nonprime attribute of R is transitively dependent on the primary key

- Intuitively, we can see that any functional dependency in which the left\-hand side is part \(a proper subset\) of the primary key, or any functional dependency in which the left-hand side is a nonkey attribute, is a problematic FD
- 2NF and 3NF normalization remove these problem FDs by decomposing the original relation into new relations
- In terms of the normalization process, it is not necessary to remove the partial dependencies before the transitive dependencies, but historically, 3NF has been defined with the assumption that a relation is tested for 2NF first before it is tested for 3NF

#### General Definition of Second Normal Form 

**Definition** : A relation schema R is in second normal form (2NF) if every nonprime attribute A in R is not partially dependent on any key of R

- The test for 2NF involves testing for functional dependencies whose left-hand side attributes are part of the primary key
- If the primary key contains a single attribute, the test need not be applied at all

#### General Definition of Third Normal Form

**Definition** : A relation schema R is in third normal form \(3NF\) if, whenever a nontrivial functional dependency X → A holds in R , either \(a\) X is a superkey of R , or \(b\) A is a prime attribute of R

#### Interpreting the General Definition of Third Normal Form

A relation schema R violates the general definition of 3NF if a functional dependency X → A holds in R that meets either of the two conditions:
- A nonprime attribute determines another nonprime attribute. Here we typically have a transitive dependency that violates 3NF
- A proper subset of a key of R functionally determines a nonprime attribute. Here we have a partial dependency that violates 2NF

**Alternative Definition** 

A relation schema R is in 3NF if every nonprime attribute of R meets both of the following conditions:
- It is fully functionally dependent on every key of R
- It is nontransitively dependent on every key of R

#### Boyce\-Codd Normal Form

- Boyce\-Codd normal form \(BCNF\) was proposed as a simpler form of 3NF, but it was found to be stricter than 3NF
- Every relation in BCNF is also in 3NF; however, a relation in 3NF is not necessarily in BCNF

We pointed out in the last subsection that although 3NF allows functional dependencies that conform to the clause \(b\) in the 3NF definition, BCNF disallows them and hence is a stricter definition of a normal form.

**Definition** : A relation schema R is in BCNF if whenever a nontrivial functional dependency X → A holds in R, then X is a superkey of R

- The formal definition of BCNF differs from the definition of 3NF in that clause \(b\) of 3NF, which allows f.d.’s having the RHS as a prime attribute, is absent from BCNF
- That makes BCNF a stronger normal form compared to 3NF
- In practice, most relation schemas that are in 3NF are also in BCNF
- Only if there exists some f.d. X → A that holds in a relation schema R with X not being a superkey and A being a prime attribute will R be in 3NF but not in BCNF

#### Decomposition of Relations not in BCNF

A simple test comes in handy to test the binary decomposition of a relation into two relations:

**NJB \(Nonadditive Join Test for Binary Decompositions\)** : A decomposition D = \{R<sub>1</sub> , R<sub>2</sub>\} of R has the lossless \(nonadditive\) join property with respect to a set of functional dependencies F on R if and only if either:
- The FD \(\( R<sub>1</sub> ∩ R<sub>2</sub>\) → \( R<sub>1</sub> − R<sub>2</sub>)) is in F<sup>+15</sup>
- The FD \(\( R 1 ∩ R 2 \) → \( R 2 − R 1 \)\) is in F<sup>+</sup>

In general, a relation R not in BCNF can be decomposed so as to meet the nonadditive join property by the following procedure. It decomposes R successively into a set of relations that are in BCNF:

Let R be the relation not in BCNF, let X ⊆ R , and let X → A be the FD that causes a violation of BCNF. R may be decomposed into two relations:
- R \-A
- XA

_If either R \–A or XA . is not in BCNF, repeat the process._

### Selected Notes from Book 2

#### Computing the Closure of Attributes

Consider the following:
- There is a set of sttributes \{A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>\}
- S is a set of FDs
- The closure of the set of attributes under the FDs in S is the set of attributes B such that every relation that satisfied all the FDs in S also satisfies:

A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub> → B

We denote the closure of a set of attributes as {<Attributes>}<sup>+</sup>

**Algorithm for the closure of a set of attributes**

- If necessary, split the FD’s of S, so each FD in S has a single attribute on the right
- Let X be a set of attributes that eventually will become the closure. Initialize X to be \{A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>\}
- Repeatedly search for some FD:

B<sub>1</sub>, B<sub>2</sub>, ..., B<sub>m</sub> → C

Such that all of B<sub>1</sub>, B<sub>2</sub>, ..., B<sub>m</sub> are in the set of attributes X but C is not.

- Add C to the set X and repeat
- Since X can only grow, and the number of attributes of any relation schema must be finite, eventually nothing more can be added to X, and this step ends

The set X, after no more attributes can be added to it, is the correct value of \{A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>\}<sup>+</sup>.

#### The Transistive Rule

The transitive rule lets us cascade two FD’s, and generalizes the observation:

- If A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub> → B<sub>1</sub>, B<sub>2</sub>, ..., B<sub>m</sub> and B<sub>1</sub>, B<sub>2</sub>, ..., B<sub>m</sub> → C<sub>1</sub>, C<sub>2</sub>, ..., C<sub>k</sub> hold in relation R, then A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub> → C<sub>1</sub>, C<sub>2</sub>, ..., C<sub>k</sub> also holds in R

Notice that {A1,A2,...,An}+ is the set of all attributes of a relation if and only if A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub> is a superkey for the relation. For only then does A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub> functionally determine all the other attributes. We can test if A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub> is a key for a relation by checking first that \{A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>\}<sup>+</sup> is all attributes, and then checking that, for no set X formed by removing one attribute from \{A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>\},is X<sup>+</sup> the set of all attributes.

#### Closing Sets of Functional Dependencies

**basis** : If we are given a set of FD’s S \(such as the FD’s that hold in a given relation\), then any set of FD’s equivalent to S is said to be a basis for S

A minimal basis for a relation is a basis B that satisfies three conditions:
- All the FD’s in B have singleton right sides
- If any FD is removed from B, the result is no longer a basis
- If for any FD in B we remove one or more attributes from the left side of F, the result is no longer a basis

#### A Complete Set of Inference Rules

- **Reflexivity** : If \{B<sub>1</sub>, B<sub>2</sub>, ..., B<sub>m</sub>\} ⊆ \{A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>\}, then A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub> → B<sub>1</sub>, B<sub>2</sub>, ..., B<sub>m</sub>. These are what we have called trivial FD’s
- **Augmentation** : If A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub> → B<sub>1</sub>, B<sub>2</sub>, ..., B<sub>m</sub>, then:

A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>C<sub>1</sub>, C<sub>2</sub>, ..., C<sub>k</sub> → B<sub>1</sub>, B<sub>2</sub>, ..., B<sub>m</sub>C<sub>1</sub>, C<sub>2</sub>, ..., C<sub>k</sub>

For any set of attributes C<sub>1</sub>, C<sub>2</sub>, ..., C<sub>k</sub>. Since some of the C’s may also be A’s or B’s or both, we should eliminate from the left side duplicate attributes and do the same for the right side.

- **Transitivity** : If A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub> → B<sub>1</sub>, B<sub>2</sub>, ..., B<sub>m</sub> and B<sub>1</sub>, B<sub>2</sub>, ..., B<sub>m</sub> → C<sub>1</sub>, C<sub>2</sub>, ..., C<sub>k</sub> then A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub> → C<sub>1</sub>, C<sub>2</sub>, ..., C<sub>k</sub>

# Week 3
## Reading
### Chapter 6: Basic SQL

**SQL** : Structured query language

* SQL is a comprehensive database language
	* It has statements for data definitions, queries, and update
	* Hence, it is both a DDL and a DML
	* In addition, it has facilities for defining views on the database, for specifying security and authorization, for defining integrity constraints, and for specifying transaction controls

#### SQL Data Definition and Data Types

* SQL uses the terms table, row, and column for the formal relational model terms relation, tuple, and attribute, respectively
* The main SQL command for data definition is the CREATE statement, which can be used to create schemas, tables \(relations\), types, and domains, as well as other constructs such as views, assertions, and triggers

#### Schema and Catalog Concepts in SQL

* An SQL schema is identified by a schema name and includes an authorization identifier to indicate the user or account who owns the schema, as well as descriptors for each element in the schema
* Schema elements include tables, types, constraints, views, domains, and other constructs \(such as authorization grants\) that describe the schema
* A schema is created via the CREATE SCHEMA statement, which can include all the schema elements’ definitions
* Alternatively, the schema can be assigned a name and authorization identifier, and the elements can be defined later

* In general, not all users are authorized to create schemas and schema elements
* The privilege to create schemas, tables, and other constructs must be explicitly granted to the relevant user accounts by the system administrator or DBA

* In addition to the concept of a schema, SQL uses the concept of a catalog
	* a named collection of schemas
* Database installations typically have a default environment and schema, so when a user connects and logs in to that database installation, the user can refer directly to tables and other constructs within that schema without having to specify a particular schema name
* A catalog always contains a special schema called INFORMATION_SCHEMA, which provides information on all the schemas in the catalog and all the element descriptors in these schemas
* Integrity constraints such as referential integrity can be defined between relations only if they exist in schemas within the same catalog. Schemas within the same catalog can also share certain elements, such as type and domain definitions

#### The CREATE TABLE Command in SQL

* The CREATE TABLE command is used to specify a new relation by giving it a name and specifying its attributes and initial constraints
	* The attributes are specified first, and each attribute is given a name
	* A data type to specify its domain of values
	* possibly attribute constraints, such as NOT NULL
* The key, entity integrity, and referential integrity constraints can be specified within the CREATE TABLE statement after the attributes are declared
	* or they can be added later using the ALTER TABLE command
* Typically, the SQL schema in which the relations are declared is implicitly specified in the environment in which the CREATE TABLE statements are executed
	* Alternatively, we can explicitly attach the schema name to the relation name, separated by a period
* The relations declared through CREATE TABLE statements are called base tables \(or base relations\)
	* this means that the table and its rows are actually created and stored as a file by the DBMS
	* Base relations are distinguished from virtual relations, created through the CREATE VIEW statement _which may not correspond to a physical file_
	* In SQL, the attributes in a base table are considered to be ordered in the sequence in which they are specified in the CREATE TABLE statement
	* However, rows \(tuples\) are not considered to be ordered within a table \(relation\)

#### Attribute Data Types and Domains in SQL

**The basic data types available for attributes include numeric, character string, bit string, Boolean, date, and time:**  
* Numeric data types include integer numbers of various sizes \(INTEGER or INT , and SMALLINT\) and floating-point \(real\) numbers of various precision \(FLOAT or REAL, and DOUBLE PRECISION\)
	* Formatted numbers can be declared by using DECIMAL \(i, j\) — or DEC \(i, j\) or NUMERIC \(i, j\)
	* Where i, the precision, is the total number of decimal digits
	* and j, the scale, is the number of digits after the decimal point
	* The default for scale is zero, and the default for precision is implementation\-defined
* Character\-string data types are either fixed length— CHAR \(n\) or CHARACTER \(n\) 
	* where n is the number of characters
	* or varying length — VARCHAR \(n\) or CHAR VARYING \(n\) or CHARACTER VARYING \(n\)
	* where n is the maximum number of characters
	* When specifying a literal string value, it is placed between single quotation marks, and it is case sensitive
	* For fixed length strings, a shorter string is padded with blank characters to the right
	* Padded blanks are generally ignored when strings are compared
	* For comparison purposes, strings are considered ordered in alphabetic \(or lexicographic\) order
	* Another variable\-length string data type called CHARACTER LARGE OBJECT or CLOB is also available to specify columns that have large text values, such as documents
* Bit\-string data types are either of fixed length n — BIT\(n\) or or varying length — BIT VARYING \(n\), where n is the maximum number of bits
	* The default for n, the length of a character string or bit string, is 1
	* Literal bit strings are placed between single quotes but preceded by a B to distinguish them from character strings; for example, B ‘10101’
	* Another variable\-length bitstring data type called BINARY LARGE OBJECT or BLOB is also available to specify columns that have large binary values, such as images
* A Boolean data type has the traditional values of TRUE or FALSE
	* In SQL, because of the presence of NULL values, a three\-valued logic is used
	* so a third possible value for a Boolean data type is UNKNOWN
* The DATE data type has ten positions, and its components are YEAR, MONTH, and DAY in the form YYYY\-MM\-DD
	* The TIME data type has at least eight positions, with the components HOUR , MINUTE , and SECOND in the form HH:MM:SS
	* A TIME WITH TIME ZONE data type includes an additional six positions for specifying the displacement from the standard universal time zone
	* Only valid dates and times should be allowed by the SQL implementation

**Some additional data types are discussed below. The list of types discussed here is not exhaustive; different implementations have added more data types to SQL:**  
* A timestamp data type \(TIMESTAMP\) includes the DATE and TIME fields, plus a minimum of six positions for decimal fractions of seconds and an optional WITH TIME ZONE qualifier
* Another data type related to DATE , TIME , and TIMESTAMP is the INTERVAL data type
	* This specifies an interval — a relative value that can be used to increment or decrement an absolute value of a date, time, or timestamp
	* Intervals are qualified to be either YEAR/MONTH intervals or DAY/TIME intervals

* It is possible to specify the data type of each attribute directly, alternatively, a domain can be declared, and the domain name can be used with the attribute specification
	* This makes it easier to change the data type for a domain that is used by numerous attributes in a schema, and improves schema readability
* In SQL, there is also a CREATE TYPE command
	* which can be used to create user defined types or UDTs
	* These can then be used either as data types for attributes, or as the basis for creating tables

#### Specifying Attribute Constraints and Attribute Defaults

* Because SQL allows NULLs as attribute values, a constraint NOT NULL may be specified if NULL is not permitted for a particular attribute
	* This is always implicitly specified for the attributes that are part of the primary key of each relation, but it can be specified for any other attributes whose values are required not to be NULL
* It is also possible to define a default value for an attribute by appending the clause DEFAULT <\value\> to an attribute definition
	* The default value is included in any new tuple if an explicit value is not provided for that attribute
	* If no default clause is specified, the default default value is NULL for attributes that do not have the NOT NULL constraint
* Another type of constraint can restrict attribute or domain values using the CHECK clause following an attribute or domain definition
	* The CHECK clause can also be used in conjunction with the CREATE DOMAIN statement

#### Specifying Key and Referential Integrity Constraints

* Because keys and referential integrity constraints are very important, there are special clauses within the CREATE TABLE statement to specify them
* The PRIMARY KEY clause specifies one or more attributes that make up the primary key of a relation
	* If a primary key has a single attribute, the clause can follow the attribute directly
* The UNIQUE clause specifies alternate \(unique\) keys, also known as candidate keys
	* The UNIQUE clause can also be specified directly for a unique key if it is a single attribute
* Referential integrity is specified via the FOREIGN KEY clause
	* a referential integrity constraint can be violated when tuples are inserted or deleted, or when a foreign key or primary key attribute value is updated
	* The default action that SQL takes for an integrity violation is to reject the update operation that will cause a violation, which is known as the RESTRICT option
	* However, the schema designer can specify an alternative action to be taken by attaching a referential triggered action clause to any foreign key constraint
	* The options include SET NULL , CASCADE , and SET DEFAULT . An option must be qualified with either ON DELETE or ON UPDATE
* In general, the action taken by the DBMS for SET NULL or SET DEFAULT is the same for both ON DELETE and ON UPDATE :
	* The value of the affected referencing attributes is changed to NULL for SET NULL and to the specified default value of the referencing attribute for SET DEFAULT
	* The action for CASCADE ON DELETE is to delete all the referencing tuples, whereas the action for CASCADE ON UPDATE is to change the value of the referencing foreign key attribute\(s\) to the updated \(new\) primary key value for all the referencing tuples

#### Giving Names to Constraints

* A constraint may be given a constraint name, following the keyword CONSTRAINT
	* The names of all constraints within a particular schema must be unique
	* A constraint name is used to identify a particular constraint in case the constraint must be dropped later and replaced with another constraint
	* Giving names to constraints is optional. It is also possible to temporarily defer a constraint until the end of a transaction

#### Specifying Constraints on Tuples Using CHECK

* In addition to key and referential integrity constraints, which are specified by special keywords, other table constraints can be specified through additional CHECK clauses at the end of a CREATE TABLE statement
	* These can be called row\-based constraints because they apply to each row individually and are checked whenever a row is inserted or modified
	* The CHECK clause can also be used to specify more general constraints using the CREATE ASSERTION statement of SQL

#### Basic Retrieval Queries in SQL

* SQL has one basic statement for retrieving information from a database: the SELECT statement
	* The SELECT statement is not the same as the SELECT operation of relational algebra
* SQL allows a table \(relation\) to have two or more tuples that are identical in all their attribute values
	* Hence, in general, an SQL table is not a set of tuples, because a set does not allow two identical members; rather, it is a multiset \(sometimes called a bag\) of tuples
* Some SQL relations are constrained to be sets because a key constraint has been declared or because the DISTINCT option has been used with the SELECT statement

#### The SELECT\-FROM\-WHERE Structure of Basic SQL Queries

* The basic form of the SELECT statement, sometimes called a mapping or a select\-from\-where block, is formed of the three clauses SELECT, FROM, and WHERE
	* attribute list : is a list of attribute names whose values are to be retrieved by the query
	* table list : is a list of the relation names required to process the query
	* condition : is a conditional \(Boolean\) expression that identifies the tuples to be retrieved by the query
* A query that involves only selection and join conditions plus projection attributes is known as a select\-project\-join query

#### Ambiguous Attribute Names, Aliasing, Renaming, and Tuple Variables

* In SQL, the same name can be used for two \(or more\) attributes as long as the attributes are in different tables
	* If this is the case, and a multitable query refers to two or more attributes with the same name, we must qualify the attribute name with the relation name to prevent ambiguity
	* This is done by prefixing the relation name to the attribute name and separating the two by a period
* We can use alias\-naming or renaming mechanism in any SQL query to specify tuple variables for every table in the WHERE clause, whether or not the same relation needs to be referenced more than once

#### Unspecified WHERE Clause and Use of the Asterisk

* A missing WHERE clause indicates no condition on tuple selection; hence, all tuples of the relation specified in the FROM clause qualify and are selected for the query result
* If more than one relation is specified in the FROM clause and there is no WHERE clause, then the CROSS PRODUCT — all possible tuple combinations — of these relations is selected
	* It is extremely important to specify every selection and join condition in the WHERE clause; if any such condition is overlooked, incorrect and very large relations may result
* To retrieve all the attribute values of the selected tuples, we do not have to list the attribute names explicitly in SQL; we just specify an asterisk \(\*\), which stands for all the attributes

#### Tables as Sets in SQL

**SQL does not automatically eliminate duplicate tuples in the results of queries, for the following reasons:**  
* Duplicate elimination is an expensive operation. One way to implement it is to sort the tuples first and then eliminate duplicates
* The user may want to see duplicate tuples in the result of a query
* When an aggregate function is applied to tuples, in most cases we do not want to eliminate duplicates

* An SQL table with a key is restricted to being a set, since the key value must be distinct in each tuple
	* If we do want to eliminate duplicate tuples from the result of an SQL query, we use the keyword DISTINCT in the SELECT clause, meaning that only distinct tuples should remain in the result
	* In general, a query with SELECT DISTINCT eliminates duplicates, whereas a query with SELECT ALL does not
	* Specifying SELECT with neither ALL nor DISTINCT is equivalent to SELECT ALL

* SQL has directly incorporated some of the set operations from mathematical set theory, which are also part of relational algebra
	* There are set union \(UNION\), set difference \(EXCEPT\), and set intersection \(INTERSECT\) operations
	* The relations resulting from these set operations are sets of tuples; that is, duplicate tuples are eliminated from the result
	* These set operations apply only to typecompatible relations, so we must make sure that the two relations on which we apply the operation have the same attributes and that the attributes appear in the same order in both relations
* SQL also has corresponding multiset operations, which are followed by the keyword ALL \(UNION ALL, EXCEPT ALL, INTERSECT ALL\)
	* Their results are multisets \(duplicates are not eliminated\)

#### Substring Pattern Matching and Arithmetic Operators

* One feature of SQL allows comparison conditions on only parts of a character string, using the LIKE comparison operator
	* This can be used for string pattern matching
	* Partial strings are specified using two reserved characters: % replaces an arbitrary number of zero or more characters, and the underscore \(\_\) replaces a single character
* If an underscore or % is needed as a literal character in the string, the character should be preceded by an escape character, which is specified after the string using the keyword ESCAPE 
* Also, we need a rule to specify apostrophes or single quotation marks \(‘ ’\) if they are to be included in a string because they are used to begin and end strings
	* If an apostrophe \(’\) is needed, it is represented as two consecutive apostrophes \(”\) so that it will not be interpreted as ending the string

* Another feature allows the use of arithmetic in queries
	* The standard arithmetic operators for addition \(\+\), subtraction \(\−\), multiplication \(\*\), and division \(/\) can be applied to numeric values or attributes with numeric domains
	* For string data types, the concatenate operator \|\| can be used in a query to append two string values
	* For date, time, timestamp, and interval data types, operators include incrementing \(\+\) or decrementing \(−\) a date, time, or timestamp by an interval
	* In addition, an interval value is the result of the difference between two date, time, or timestamp values
* Another comparison operator, which can be used for convenience, is BETWEEN specifying a range of values

#### Ordering of Query Results

* SQL allows the user to order the tuples in the result of a query by the values of one or more of the attributes that appear in the query result, by using the ORDER BY clause
	* The default order is in ascending order of values
	* We can specify the keyword DESC if we want to see the result in a descending order of values
	* The keyword ASC can be used to specify ascending order explicitly 

#### Discussion and Summary of Basic SQL Retrieval Queries

* A simple retrieval query in SQL can consist of up to four clauses, but only the first two — SELECT and FROM — are mandatory
	* The SELECT clause lists the attributes to be retrieved, and the FROM clause specifies all relations \(tables\) needed in the simple query
	* The WHERE clause identifies the conditions for selecting the tuples from these relations
	* ORDER BY specifies an order for displaying the results of a query

#### The INSERT Command

* In its simplest form, INSERT is used to add a single tuple \(row\) to a relation \(table\)
	* We must specify the relation name and a list of values for the tuple. The values should be listed in the same order in which the corresponding attributes were specified in the CREATE TABLE command
* A second form of the INSERT statement allows the user to specify explicit attribute names that correspond to the values provided in the INSERT command
	* This is useful if a relation has many attributes but only a few of those attributes are assigned values in the new tuple
	* However, the values must include all attributes with NOT NULL specification and no default value
	* Attributes with NULL allowed or DEFAULT values are the ones that can be left out
* It is also possible to insert into a relation multiple tuples separated by commas in a single INSERT command
* A variation of the INSERT command inserts multiple tuples into a relation in conjunction with creating the relation and loading it with the result of a query

#### The DELETE Command

* The DELETE command removes tuples from a relation
* It includes a WHERE clause, similar to that used in an SQL query, to select the tuples to be deleted
* However, the deletion may propagate to tuples in other relations if referential triggered actions are specified in the referential integrity constraints of the DDL
* Depending on the number of tuples selected by the condition in the WHERE clause, zero, one, or several tuples can be deleted by a single DELETE command
* We must use the DROP TABLE command to remove the table definition

#### The UPDATE Command

* The UPDATE command is used to modify attribute values of one or more selected tuples
	* As in the DELETE command, a WHERE clause in the UPDATE command selects the tuples to be modified from a single relation
	* However, updating a primary key value may propagate to the foreign key values of tuples in other relations if such a referential triggered action is specified in the referential integrity constraints of the DDL
	* An additional SET clause in the UPDATE command specifies the attributes to be modified and their new values
	* Several tuples can be modified with a single UPDATE command
	* It is also possible to specify NULL or DEFAULT as the new attribute value

#### Additional Features of SQL

**SQL has a number of additional features that we have not described in this chapter but that we discuss elsewhere in the book. These are as follows:**  
* SQL has various techniques for writing programs in various programming languages that include SQL statements to access one or more databases
	* embedded \(and dynamic\) SQL, SQL/CLI \(Call Level Interface\) and its predecessor ODBC \(Open Data Base Connectivity\), and SQL/PSM \(Persistent Stored Modules\)
* Each commercial RDBMS will have, in addition to the SQL commands, a set of commands for specifying physical database design parameters, file structures for relations, and access paths such as indexes
	* We called these commands a storage definition language \(SDL\)
* SQL has transaction control commands
	* These are used to specify units of database processing for concurrency control and recovery purposes
* SQL has language constructs for specifying the granting and revoking of privileges to users
	* Privileges typically correspond to the right to use certain SQL commands to access certain relations
	* Each relation is assigned an owner, and either the owner or the DBA staff can grant to selected users the privilege to use an SQL statement — such as SELECT , INSERT , DELETE , or UPDATE — to access the relation
	* In addition, the DBA staff can grant the privileges to create schemas, tables, or views to certain users
* SQL has language constructs for creating triggers
	* These are generally referred to as active database techniques, since they specify actions that are automatically triggered by events such as database updates
* SQL has incorporated many features from object\-oriented models to have more powerful capabilities, leading to enhanced relational systems known as object\-relational
* SQL and relational databases can interact with new technologies such as XML and OLAP/data warehouses

### More SQL: Complex Queries, Triggers, Views, and Schema Modification

#### Comparisons Involving NULL and Three\-Valued Logic

* SQL has various rules for dealing with NULL values
* NULL is used to represent a missing value, but that it usually has one of three different interpretations:
	* value unknown \(value exists but is not known, or it is not known whether or not the value exists\)
	* value not available \(value exists but is purposely withheld\)
	* value not applicable \(the attribute does not apply to this tuple or is undefined for this tuple\)

_It is often not possible to determine which of the meanings is intended; for example, a NULL for the home phone of a person can have any of the three meanings. Hence, SQL does not distinguish among the different meanings of NULL._

* In general, each individual NULL value is considered to be different from every other NULL value in the various database records
* When a record with NULL in one of its attributes is involved in a comparison operation, the result is considered to be UNKNOWN \(it may be TRUE or it may be FALSE\)
* Hence, SQL uses a three-valued logic with values TRUE , FALSE , and UNKNOWN instead of the standard two\-valued \(Boolean\) logic with values TRUE or FALSE

* In select\-project\-join queries, the general rule is that only those combinations of tuples that evaluate the logical expression in the WHERE clause of the query to TRUE are selected
	* Tuple combinations that evaluate to FALSE or UNKNOWN are not selected
	*  However, there are exceptions to that rule for certain operations, such as outer joins

* SQL allows queries that check whether an attribute value is NULL
	* Rather than using = or <\> to compare an attribute value to NULL, SQL uses the comparison operators IS or IS NOT

#### Nested Queries, Tuples, and Set/Multiset Comparisons

* Some queries require that existing values in the database be fetched and then used in a comparison condition
	* Such queries can be conveniently formulated by using nested queries, which are complete select\-from\-where blocks within another SQL query
	* That other query is called the outer query
	* These nested queries can also appear in the WHERE clause or the FROM clause or the SELECT clause or other SQL clauses as needed
* If a nested query returns a single attribute and a single tuple, the query result will be a single \(scalar\) value
	* In such cases, it is permissible to use = instead of IN for the comparison operator
* In addition to the IN operator, a number of other comparison operators can be used to compare a single value v \(typically an attribute name\) to a set or multiset v \(typically a nested query\)
	* The = ANY \(or = SOME\) operator returns TRUE if the value v is equal to some value in the set V and is hence equivalent to IN
	* The two keywords ANY and SOME have the same effect
	* Other operators that can be combined with ANY \(or SOME\) include \>, \>=, <, <=, and <\>
	* The keyword ALL can also be combined with each of these operators

* In general, we can have several levels of nested queries
	* We can once again be faced with possible ambiguity among attribute names if attributes of the same name exist — one in a relation in the FROM clause of the outer query, and another in a relation in the FROM clause of the nested query
	* The rule is that a reference to an unqualified attribute refers to the relation declared in the inner most nested query

#### Correlated Nested Queries

* Whenever a condition in the WHERE clause of a nested query references some attribute of a relation declared in the outer query, the two queries are said to be correlated
* In general, a query written with nested select-from-where blocks and using the = or IN comparison operators can always be expressed as a single block query

#### The EXISTS and UNIQUE Functions in SQL

* EXISTS and UNIQUE are Boolean functions that return TRUE or FALSE; hence, they can be used in a WHERE clause condition
	* The EXISTS function in SQL is used to check whether the result of a nested query is empty \(contains no tuples\) or not
	* The result of EXISTS is a Boolean value TRUE if the nested query result contains at least one tuple, or FALSE if the nested query result contains no tuples
* EXISTS and NOT EXISTS are typically used in conjunction with a correlated nested query
* There is another SQL function, UNIQUE \(Q\), which returns TRUE if there are no duplicate tuples in the result of query Q; otherwise, it returns FALSE
	* This can be used to test whether the result of a nested query is a set \(no duplicates\) or a multiset \(duplicates exist\)

#### Explicit Sets and Renaming in SQL

* We have seen several queries with a nested query in the WHERE clause
	* It is also possible to use an explicit set of values in the WHERE clause, rather than a nested query
	* Such a set is enclosed in parentheses in SQL
* In SQL, it is possible to rename any attribute that appears in the result of a query by adding the qualifier AS followed by the desired new name
	* Hence, the AS construct can be used to alias both attribute and relation names in general, and it can be used in appropriate parts of a query

## Week 4
### Reading: Chapter 7
#### Comparisons Involving NULL and Three\-Valued Logic

* SQL has various rules for dealing with NULL values
* Consider the following examples to illustrate each of the meanings of NULL:
	* **Unknown value** : A person’s date of birth is not known, so it is represented by NULL in the database. An example of the other case of unknown would be NULL for a person’s home phone because it is not known whether or not the person has a home phone
	* **Unavailable or withheld value** : A person has a home phone but does not want it to be listed, so it is withheld and represented as NULL in the database
	* **Not applicable attribute** : An attribute LastCollegeDegree would be NULL for a person who has no college degrees because it does not apply to that person
* In general, each individual NULL value is considered to be different from every other NULL value in the various database records
* Note that in standard Boolean logic, only TRUE or FALSE values are permitted; there is no UNKNOWN value

* In select\-project\-join queries, the general rule is that only those combinations of tuples that evaluate the logical expression in the WHERE clause of the query to TRUE are selected
* Tuple combinations that evaluate to FALSE or UNKNOWN are not selected
* SQL allows queries that check whether an attribute value is NULL
	* Rather than using = or <\> to compare an attribute value to NULL , SQL uses the comparison operators IS or IS NOT
	* This is because SQL considers each NULL value as being distinct from every other NULL value, so equality comparison is not appropriate
* It follows that when a join condition is specified, tuples with NULL values for the join attributes are not included in the result

#### Nested Queries, Tuples, and Set/Multiset Comparisons

* Some queries require that existing values in the database be fetched and then used in a comparison condition
* Such queries can be conveniently formulated by using nested queries , which are complete select\-from\-where blocks within another SQL query
* That other query is called the outer query
* These nested queries can also appear in the WHERE clause or the FROM clause or the SELECT clause or other SQL clauses as needed
* If a nested query returns a single attribute and a single tuple, the query result will be a single \( scalar \) value
	* In such cases, it is permissible to use = instead of IN for the comparison operator
	* In general, the nested query will return a table \(relation\), which is a set or multiset of tuples
* SQL allows the use of tuples of values in comparisons by placing them within parentheses

* In addition to the IN operator, a number of other comparison operators can be used to compare a single value v \(typically an attribute name\) to a set or multiset v \(typically a nested query\)
* The = ANY \(or = SOME\) operator returns TRUE if the value v is equal to some value in the set V and is hence equivalent to IN
* The comparison condition \( v \> ALL V \) returns TRUE if the value v is greater than all the values in the set \(or multiset\) V

* In general, we can have several levels of nested queries:
	* We can once again be faced with possible ambiguity among attribute names if attributes of the same name exist— one in a relation in the FROM clause of the outer query, and another in a relation in the FROM clause of the nested query
	* The rule is that a reference to an unqualified attribute refers to the relation declared in the innermost nested query

#### Correlated Nested Queries

* Whenever a condition in the WHERE clause of a nested query references some attribute of a relation declared in the outer query, the two queries are said to be correlated
	* We can understand a correlated query better by considering that the nested query is evaluated once for each tuple \(or combination of tuples\) in the outer query
	* In general, a query written with nested select\-from\-where blocks and using the = or IN comparison operators can always be expressed as a single block query

#### The EXISTS and UNIQUE Functions in SQL

* EXISTS and UNIQUE are Boolean functions that return TRUE or FALSE
	* hence, they can be used in a WHERE clause condition
* The EXISTS function in SQL is used to check whether the result of a nested query is empty \(contains no tuples\) or not 
	*  The result of EXISTS is a Boolean value TRUE if the nested query result contains at least one tuple, or FALSE if the nested query result contains no tuples
* There is another SQL function, UNIQUE, which returns TRUE if there are no duplicate tuples in the result of query Q
	* otherwise, it returns FALSE
	* This can be used to test whether the result of a nested query is a set \(no duplicates\) or a multiset \(duplicates exist\)

#### Explicit Sets and Renaming in SQL

* It is possible to use an explicit set of values in the WHERE clause, rather than a nested query
	* Such a set is enclosed in parentheses in SQL
* In SQL, it is possible to rename any attribute that appears in the result of a query by adding the qualifier AS followed by the desired new name
	* Hence, the AS construct can be used to alias both attribute and relation names in general, and it can be used in appropriate parts of a query

#### Joined Tables in SQL and Outer Joins

* The concept of a joined table \(or joined relation\) was incorporated into SQL to permit users to specify a table resulting from a join operation in the FROM clause of a query
* This construct may be easier to comprehend than mixing together all the select and join conditions in the WHERE clause
* The concept of a joined table also allows the user to specify different types of join, such as NATURAL JOIN and various types of OUTER JOIN
	* In a NATURAL JOIN on two relations R and S, no join condition is specified; an implicit EQUIJOIN condition for each pair of attributes with the same name from R and S is created
	* Each such pair of attributes is included only once in the resulting relation
* If the names of the join attributes are not the same in the base relations, it is possible to rename the attributes so that they match, and then to apply NATURAL JOIN
* In this case, the AS construct can be used to rename a relation and all its attributes in the FROM clause
* The default type of join in a joined table is called an inner join, where a tuple is included in the result only if a matching tuple exists in the other relation
* If the user requires that all employees be included, a different type of join called OUTER JOIN must be used explicitly

* In SQL, the options available for specifying joined tables include:
	* INNER JOIN : only pairs of tuples that match the join condition are retrieved, same as JOIN
	* LEFT OUTER JOIN : every tuple in the left table must appear in the result; if it does not have a matching tuple, it is padded with NULL values for the attributes of the right table
	* RIGHT OUTER JOIN : every tuple in the right table must appear in the result; if it does not have a matching tuple, it is padded with NULL values for the attributes of the left table
	* FULL OUTER JOIN
* The keyword CROSS JOIN is used to specify the CARTESIAN PRODUCT operation
	* this should be used only with the utmost care because it generates all possible tuple combinations
* It is also possible to nest join specifications; that is, one of the tables in a join may itself be a joined table
	* This allows the specification of the join of three or more tables as a single joined table, which is called a multiway join

#### Aggregate Functions in SQL

* Aggregate functions are used to summarize information from multiple tuples into a single\-tuple summary
* Grouping is used to create subgroups of tuples before summarization
* A number of built\-in aggregate functions exist:
	* The COUNT function returns the number of tuples or values as specified in a query
	* The functions SUM , MAX , MIN , and AVG can be applied to a set or multiset of numeric values and return, respectively, the sum, maximum value, minimum value, and average \(mean\) of those values
	* These functions can be used in the SELECT clause or in a HAVING clause
	* The functions MAX and MIN can also be used with attributes that have nonnumeric domains if the domain values have a total ordering among one another

#### Grouping: The GROUP BY and HAVING Clauses

* In many cases we want to apply the aggregate functions to subgroups of tuples in a relation, where the subgroups are based on some attribute values
* In these cases we need to partition the relation into nonoverlapping subsets \(or groups\) of tuples
* Each group \(partition\) will consist of the tuples that have the same value of some attribute\(s\), called the grouping attribute\(s\)
* We can then apply the function to each such group independently to produce summary information about each group
* SQL has a GROUP BY clause for this purpose
	* The GROUP BY clause specifies the grouping attributes, which should also appear in the SELECT clause, so that the value resulting from applying each aggregate function to a group of tuples appears along with the value of the grouping attribute\(s\)
* If NULL s exist in the grouping attribute, then a separate group is created for all tuples with a NULL value in the grouping attribute

* Sometimes we want to retrieve the values of these functions only for groups that satisfy certain conditions
* SQL provides a HAVING clause, which can appear in conjunction with a GROUP BY clause, for this purpose
	* HAVING provides a condition on the summary information regarding the group of tuples associated with each value of the grouping attributes
	* Only the groups that satisfy the condition are retrieved in the result of the query

#### Other SQL Constructs: WITH and CASE

* The WITH clause allows a user to define a table that will only be used in a particular query; it is somewhat similar to creating a view that will be used only in one query and then dropped
* SQL also has a CASE construct, which can be used when a value can be different based on certain conditions
	* This can be used in any part of an SQL query where a value is expected, including when querying, inserting or updating tuples
* The CASE construct can also be used when inserting tuples that can have different attributes being NULL depending on the type of record being inserted into a table
	* as when a specialization is mapped into a single table or when a union type is mapped into relations

#### Recursive Queries in SQL

* An example of a recursive relationship between tuples of the same type is the relationship between an employee and a supervisor
* An example of a recursive operation is to retrieve all supervisees of a supervisory employee e at all levels — that is, all employees e′ directly supervised by e , all employees e′ directly supervised by each employee e′ , all employees e″′ directly supervised by each employee e″ , and so on
* This is repeated with successive levels until a fixed point is reached, where no more tuples are added to the view

#### Specifying Constraints as Assertions and Actions as Triggers

* CREATE ASSERTION , which can be used to specify additional types of constraints that are outside the scope of the built\-in relational model constraints \(primary and unique keys, entity integrity, and referential integrity\)
* CREATE TRIGGER , which can be used to specify automatic actions that the database system will perform when certain events and conditions occur
	* This type of functionality is generally referred to as active databases

#### Specifying General Constraints as Assertions in SQL

* In SQL, users can specify general constraints— those that do not fall into any of the categories described previously via declarative assertions using the CREATE ASSERTION statement
* Each assertion is given a constraint name and is specified via a condition similar to the WHERE clause of an SQL query
	* this is followed by the keyword CHECK
	* which is followed by a condition in parentheses that must hold true on every database state for the assertion to be satisfied
* The constraint name can be used later to disable the constraint or to modify or drop it
* Any WHERE clause condition can be used, but many constraints can be specified using the EXISTS and NOT EXISTS style of SQL conditions
* Whenever some tuples in the database cause the condition of an ASSERTION statement to evaluate to FALSE , the constraint is violated

* The basic technique for writing such assertions is to specify a query that selects any tuples that violate the desired condition
	* By including this query inside a NOT EXISTS clause, the assertion will specify that the result of this query must be empty so that the condition will always be TRUE
* Note that the CHECK clause and constraint condition can also be used to specify constraints on individual attributes and domains and on individual tuples 
* A major difference between CREATE ASSERTION and the individual domain constraints and tuple constraints is that the CHECK clauses on individual attributes, domains, and tuples are checked in SQL only when tuples are inserted or updated in a specific table

#### Introduction to Triggers in SQL

* In many cases it is convenient to specify the type of action to be taken when certain events occur and when certain conditions are satisfied
* For example, it may be useful to specify a condition that, if violated, causes some user to be informed of the violation.
* A manager may want to be informed if an employee’s travel expenses exceed a certain limit by receiving a message whenever this occurs
* The condition is thus used to monitor the database
	* Other actions may be specified, such as executing a specific stored procedure or triggering other updates
* The CREATE TRIGGER statement is used to implement such actions in SQL

* A typical trigger which is regarded as an ECA \(Event, Condition, Action\) rule has three components:
	* The event\(s\) : These are usually database update operations that are explicitly applied to the database. In some cases, it may be necessary to write more than one trigger to cover all possible cases. These events are specified after the keyword BEFORE in our example, which means that the trigger should be executed before the triggering operation is executed. An alternative is to use the keyword AFTER , which specifies that the trigger should be executed after the operation specified in the event is completed.
	* The condition that determines whether the rule action should be executed: Once the triggering event has occurred, an optional condition may be evaluated. If no condition is specified, the action will be executed once the event occurs. If a condition is specified, it is first evaluated, and only if it evaluates to true will the rule action be executed. The condition is specified in the WHEN clause of the trigger.
	* The action to be taken: The action is usually a sequence of SQL statements, but it could also be a database transaction or an external program that will be automatically executed.

_Triggers can be used in various applications, such as maintaining database consistency, monitoring database updates, and updating derived data automatically._

#### Concept of a View in SQL

* A view in SQL terminology is a single table that is derived from other tables
* These other tables can be base tables or previously defined views
* A view does not necessarily exist in physical form; it is considered to be a virtual table , in contrast to base tables , whose tuples are always physically stored in the database
	* This limits the possible update operations that can be applied to views, but it does not provide any limitations on querying a view
* We can think of a view as a way of specifying a table that we need to reference frequently, even though it may not exist physically

#### Specification of Views in SQL

* In SQL, the command to specify a view is CREATE VIEW
* The view is given a \(virtual\) table name \(or view name\), a list of attribute names, and a query to specify the contents of the view
* If none of the view attributes results from applying functions or arithmetic operations, we do not have to specify new attribute names for the view, since they would be the same as the names of the attributes of the defining tables in the default case

* A view is supposed to be always up\-to\-date
	* if we modify the tuples in the base tables on which the view is defined, the view must automatically reflect these changes
* Hence, the view does not have to be realized or materialized at the time of view definition but rather at the time when we specify a query on the view
* It is the responsibility of the DBMS and not the user to make sure that the view is kept up\-to\-date

* The disadvantage of this approach is that it is inefficient for views defined via complex queries that are time\-consuming to execute
	* especially if multiple view queries are going to be applied to the same view within a short period of time
* The second strategy, called view materialization , involves physically creating a temporary or permanent view table when the view is first queried or created and keeping that table on the assumption that other queries on the view will follow
	* In this case, an efficient strategy for automatically updating the view table when the base tables are updated must be developed in order to keep the view up\-to\-date
* Techniques using the concept of incremental update have been developed for this purpose, where the DBMS can determine what new tuples must be inserted, deleted, or modified in a materialized view table when a database update is applied to one of the defining base tables
* The view is generally kept as a materialized \(physically stored\) table as long as it is being queried
	* If the view is not queried for a certain period of time, the system may then automatically remove the physical table and recompute it from scratch when future queries reference the view

* Different strategies as to when a materialized view is updated are possible:	
	* The immediate update strategy updates a view as soon as the base tables are changed
	* the lazy update strategy updates the view when needed by a view query
	* the periodic update strategy updates the view periodically \(in the latter strategy, a view query may get a result that is not up\-to\-date\)

* A user can always issue a retrieval query against any view
	* However, issuing an INSERT, DELETE, or UPDATE command on a view table is in many cases not possible
* In general, an update on a view defined on a single table without any aggregate functions can be mapped to an update on the underlying base table under certain conditions
* For a view involving joins, an update operation may be mapped to update operations on the underlying base relations in multiple ways
	* Hence, it is often not possible for the DBMS to determine which of the updates is intended

* Generally, a view update is feasible when only one possible update on the base relations can accomplish the desired update operation on the view
* Whenever an update on the view can be mapped to more than one update on the underlying base relations, it is usually not permitted

_It is also possible to define a view table in the FROM clause of an SQL query. This is known as an in-line view . In this case, the view is defined within the query itself._

#### Views as Authorization Mechanisms

* Views can be used to hide certain attributes or tuples from unauthorized users
* A view can restrict a user to only see certain columns; for example, only the first name, last name, and address of an employee may be visible

#### The DROP Command

* The DROP command can be used to drop named schema elements, such as tables, domains, types, or constraints
	* One can also drop a whole schema if it is no longer needed by using the DROP SCHEMA command
* There are two drop behavior options: CASCADE and RESTRICT
* For example, to remove the COMPANY database schema and all its tables, domains, and other elements, the CASCADE option is used
* If the RESTRICT option is chosen in place of CASCADE , the schema is dropped only if it has no elements in it; otherwise, the DROP command will not be executed
	* To use the RESTRICT option, the user must first individually drop each element in the schema, then drop the schema itself
* If the RESTRICT option is chosen instead of CASCADE , a table is dropped only if it is not referenced in any constraints
* With the CASCADE option, all such constraints, views, and other elements that reference the table being dropped are also dropped automatically from the schema, along with the table itself
* The DROP command can also be used to drop other types of named schema elements, such as constraints or domains

#### The ALTER Command

* The definition of a base table or of other named schema elements can be changed by using the ALTER command
* For base tables, the possible alter table actions include adding or dropping a column \(attribute\), changing a column definition, and adding or dropping table constraints
* If no default clause is specified, the new attribute will have NULL s in all the tuples of the relation immediately after the command is executed; hence, the NOT NULL constraint is not allowed in this case

* To drop a column, we must choose either CASCADE or RESTRICT for drop behavior
	* If CASCADE is chosen, all constraints and views that reference the column are dropped automatically from the schema, along with the column
	* If RESTRICT is chosen, the command is successful only if no views or constraints \(or other schema elements\) reference the column
* One can also change the constraints specified on a table by adding or dropping a named constraint