
>
SELECT S.name  
FROM   Sailors AS S, Reserves AS R  
WHERE  S.sid = R.sid AND R.bid = 102  

> **π<sub>name</sub>(<sub>bid=102</sub>(Sailors⋈<sub>sid</sub>Reserves))**


>  
SELECT name,age   
FROM Sailors  
WHERE age < 30  

> **π<sub>name,age</sub>(σ<sub>age<30</sub>(Sailors))**


Projection

**π<sub>name</sub>(σ<sub>bid=102</sub>(Sailors⋈<sub>sid</sub>Reserves))**

Consider the following schema:  

Suppliers(__*sid*__: integer, sname: string, address: string)   
Parts(__*pid*__: integer, pname: string, color: string)   
Catalog(__*sid: integer, pid: integer*__, cost: real)  

Find the names of suppliers who supply a red part. 

RA&nbsp;&nbsp;&nbsp;**π<sub>sname</sub>(π<sub>sid</sub>((π<sub>pid</sub>σ<sub>color='red'</sub>Parts)⋈Catalog)⋈Suppliers)**

SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT S.sname          
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Suppliers S, Parts P, Catalog C   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE P.color=’red’ AND C.pid=P.pid AND C.sid=S.sid  
      
Find the sids of suppliers who supply some red or green part. 

RA          **π<sub>sid</sub>(π<sub>pid</sub>(σ<sub>color='red' V color='green'</sub>Parts)⋈Catalog)** 
      
SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT C.sid   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Catalog C, Parts P   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE (P.color = ‘red’ OR P.color = ‘green’)   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AND P.pid = C.pid  