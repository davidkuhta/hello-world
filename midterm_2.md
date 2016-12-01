## Midterm 2 Study Guide  

__Important Definitions with Examples__  

__*Superkey*__  
  
Given the following EMPLOYEE relation: 

|_**SSn**_|Ename|Bdate|Address|Dnumber|
|---|---|---|---|---|  
  
where SSn is the __key__ for the relation and {Ssn}, {Ssn, Ename}, {Ssn,Ename,Bdate}, and any set of attributes that includes Ssn are all superkeys. If a relation schema has more than one key, each is called a candidate key. One of the candidate keys is arbitrarily designated to be the primary key, and the others are called secondary keys. In a practical relational database, each relation schema must have a primary key. If no candidate key is known for a relation, the entire relation can be treated as a default superkey. In the previous schema, {Ssn} is the only candidate key for EMPLOYEE, so it is also the primary key. 

__*Prime attribute verses non-prime attribute*__  
  
Given the following schema, both Ssn and number are __prime attributes__ whereas the __Hours__ attribute is __nonprime__:  

|_**Ssn**_|_**number**_|Hours|  
|---|---|---|  

  
__*Full Functional Dependency verses Partial Functional Dependency*__  
  
These topics deal primarily with deciding whether a relation schema is in 2NF.  Althought not covered specifically in class, they are important topics to understand for the upcoming examples.  




__Topics__
 - __Attribute Closure__  
 - __Finding Candidate Keys__  
 - __Minimal Cover__  
 
 
 