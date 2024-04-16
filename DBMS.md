Database Management System

Database is a collection of interrelated data
Management System is used to manage the data present in the DB (access, edit, delete, create)

Goal of DBMS - Provide efficent storage and management mechanisms for data

Disadvantages of File System:
1. Data Redundancy  and Inconsistency -
	1. Information maybe duplicated across various files
	2. Different files may have different formats, which may hamper the efficiently
2. Difficulty in accessing data

### Views of Data

We would want to provide different access permissions to different users. For this we incorporate Data Abstraction in form of Views

View is a sub-database of the main database which shows only those data which are requested.
Multiple views of the same database is possible

### Data Abstraction

1. Physical Level -
	1. Low level Data Structures
2. Logical Level -
	1. Describes the data properties and relationships
	2. Physical Data Independence
3. View/User Level -
	1. Part of the database which is requested by the user

<b>Instance</b> : Database state and its data at a particular moment of time
<b>Schema</b> : Design of the database

## Data Models

Collection of conceptual tools which describe the data, its relationships and semantics, and constraints

Types of Data Models:
1. Relational Model
	1. Data and their relationships are represented by tables (called relations)
2. Entity - Relationship Model (ER Model)
	1. Uses collection of entities and their relationships among each other
3. Object Base Data Model
	1. Combines OOP and ER Model
4. Semistructured Data Model:
	1. Individual Data items of the same type may have different set of attributes (XML)
5. Network Data Model
6. Hierarchical Data Model

#### Database Languages
1. DDL (Data Definition Language):
	1. Used to specify the database schema
2. DML (Data Manipulation Language):
	1. Used to specify queries and updates

## ER Model

Entity
Entity Set
Attributes
Relations

# Functional Dependency

Key - minimum list of attributes that functional determine rest of the attributes

Super Key - Superset of Keys

ID x y z vx vy vz

For a molecule, only ID or (x,y,z) is unique
The x y z in pairs or individual can be same
Vx vy vz can be same for various molecules

ID -> x y z vx vy vz
x y z -> ID vx vy vz
ID x y z -> vx vy vz

A -> B
B -> C
A -> C
A B -> C

set of FD -> all relational instances (tuples) that satisfy the FD

FD S follows from FD T if Set of FD S $\subset$ Set of FD T

Two FDs equivalent if T follows from S and S follows from T

Splitting Rule
$A_1, A_2, ..., A_n \rightarrow B_1, B_2, ..., B_n$
$A_1, A_2, ..., A_n \rightarrow B_1$
$A_1, A_2, ..., A_n \rightarrow B_2$
...
$A_1, A_2, ..., A_n \rightarrow B_n$

Converse is Combining Rule

Trivial FD -
Right Side attributes $\subset$ Left Side attributes

Trivial dependency rule -
Remove those right side attributes which also appear in the left (right should not become empty)

Functional Dependency -  
{A, B} -> C  
  
Each value on the left-hand side is associated with exactly one value on the right-hand side  
  
Multi-valued Dependency -  
When one value of the LHS is associated with only a specific set of values on the RHS  
  
Violation of First Normal Form -  
Using row order to convey information  
Mixing Data types  
Designing a table without a primary key  
Storing a repeating group of data items on a single row  
  
Deletion Anomaly -  
A deletion of a single entry in a row within a table removes other vital information  
  
Update Anomaly -  
When the attributes of some of the rows with common attributes get updated, then there is a data inconsistency  
  
Insertion Anomaly -  
  
Second Normal Form -  
Each non-key attribute must depend on the entire primary key  
We can't have a non-prime attribute that depends on part of a candidate key  
  
Third Normal Form -  
There should be no functional dependency between two non-key attributes  
Every non-key attribute in a table should only depend on the primary key  
Each non-prime attribute in a table should depend on every candidate key; it should never depend on part of a candidate key; and it should never depend on other non-prime attributes  
  
For all functional dependencies X $\rightarrow$ A in set F from attribute set R where $X \in R$ , the following must hold: 
1.  $A \in X$ (Trivial FD)
2. X is super key
3. A is part of some key in R

Violation of 3NF:
1. Partial Dependency - X is proper subset of some key in R
2. Transistive Dependency - X is not a proper subset of any key

The issue here is that prime attributes (or tables with only prime attributes) may depend only on the part of the candidate key  
  
Boyce - Codd Normal Form -  
Every attribute in a table should only depend on the primary key  
Except for trivial functional dependencies, every functional dependency in a table must depend on a candidate key (or on a superset of a candidate key).  

For all functional dependencies X $\rightarrow$ A in set F from attribute set R where $X \in R$ , the following must hold: 
1.  $A \in X$ (Trivial FD)
2. X is super key

To check if a relation is in BCNF form:  
Consider the set of functional dependencies  
If all LHS attributes are superkey, then yes  
  
To check if an attribute is a superkey for a relation:  
Calculate its attribute closure in the set of functional dependencies  
If closure contains all attributes, then super/candidate key  
  
Attribute Closure of X in F: 

~~~
closure set = {X}
Loop till closure set doesn't change:  
	If(U -> V in F) then
		closure = closure U {V}
	endif
~~~

Super Key -  
Candidate key or superset of a candidate key  
  
Candidate key -  
Attribute (or combination of attributes) that uniquely identifies a row in the table  
So for each non-key attribute, we can define a functional dependency from candidate key to non-key attributes  
  
Prime Attribute -  
An attribute that belongs to at least one candidate key  
  
Non-prime Attribute -  
An attribute that doesn't belong to any candidate key  
  
Fourth Normal Form -  
Multivalued dependencies in a table must be multivalued dependencies on the key  
  
Fifth Normal Form -  
The table (in 4NF) cannot be describable as the logical result of joining some tables together