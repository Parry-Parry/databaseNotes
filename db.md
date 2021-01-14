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