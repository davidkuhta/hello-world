# Join Problem Walkthroughs
## Example 1
### Stats
|Fill Factor|Dir. Entry Size|Tuple Size|Page Size|    
|:---------:|:-------------:|:--------:|:-------:|  
|     0.5   |    5 bytes    | 100 bytes|400 bytes|

### Relations
| Attribute\Relation |    T1    |    T2    |    T3    |    T4    |    
|-------------------:|:--------:|:--------:|:--------:|:--------:|
|       Tuples       |  2000    |  20000   |    20    |  200000  |  
| Primary Hash Index |          |     ✓    |          |          |  
|Secondary Hash Index|     ✓    |          |          |          |  
| Primary Tree Index |          |          |    ✓     |     ✓    |  
|Secondary Tree Index|          |     ✓    |          |     ✓    |  

### Prepartion Steps 
1. Compute the Directory Entries Per Page
   1.  floor(<sup>Page Size * Fill Factor</sup>&frasl;<sub>Dir Entry Size</sub>)  
   2.  floor(<sup>400 * 0.5</sup>&frasl;<sub>5</sub>) 
   3.  40 <sup>DEs</sup>&frasl;<sub>Page</sub>
   
|Fill Factor|Dir. Entry Size|Tuple Size|Page Size|DE/Page|    
|:---------:|:-------------:|:--------:|:-------:|:-----:|     
|     0.5   |    5 bytes    | 100 bytes|400 bytes|  40   |  

2. Compute the Tuples Per Page
   1.  floor(<sup>Page Size * Fill Factor</sup>&frasl;<sub>Tuple Size</sub>) 
   2.  floor(<sup>400 * 0.5</sup>&frasl;<sub>100</sub>)  
   3.  2 <sup>Tups</sup>&frasl;<sub>Page</sub>

|Fill Factor|Dir. Entry Size|Tuple Size|Page Size|DE/Page|Tups/Page|    
|:---------:|:-------------:|:--------:|:-------:|:-----:|:-------:|   
|     0.5   |    5 bytes    | 100 bytes|400 bytes|  40   |    2    |  

3. Compute the Page Sizes for each of the relations T1 thru T4. (Note: we need to end up in units of pages!)
   1.  T1 = <sup>2000 Tuples</sup>&frasl;<sub>2 Tuples/Page</sub> = 1000 Pages  
   1.  T2 = <sup>20000 Tuples</sup>&frasl;<sub>2 Tuples/Page</sub> = 10000 Pages  
   1.  T3 = <sup>20 Tuples</sup>&frasl;<sub>2 Tuples/Page</sub> = 10 Pages  
   1.  T4 = <sup>200000 Tuples</sup>&frasl;<sub>2 Tuples/Page</sub> = 100000 Pages  

| Attribute\Relation |    T1    |    T2    |    T3    |    T4    |      
|-------------------:|:--------:|:--------:|:--------:|:--------:|
|       Tuples       |  2000    |  20000   |    20    |  200000  | 
|       Pages        |  1000    |  10000   |    10    |  100000  |  

4. Compute the Lookup Costs for each of the indexes relations T1 thru T4. (Note: Costs is to lookup 1 tuple in page units!)
   1.  Equations
       1. Hash Index Cost = 1
       2. Primary Tree Index Cost = ceiling(log<sub>DE&frasl;Page</sub>(# of Relation Pages)) + 1
       3. Secondary Tree Index Cost = ceiling(log<sub>DE&frasl;Page</sub>(<sup># of Relation Tuples</sup>&frasl;<sub>DE/Page</sub>)) + 2
   2.  T1: Primary Tree Index = 3
       1.  ceiling(Log<sub>40</sub>(1000)) + 1 = ceiling(1.872) + 1 = 2 + 1 = 3 
   3.  T2: Primary Hash Index = 1  
   3.  T2: Secondary Tree Index = 4
       1.  ceiling(Log<sub>40</sub>(10000)) + 1 = ceiling(2.496) + 1 = 3 + 1 = 4 
   4.  T3: Primary Tree Index = 2
       1.  ceiling(Log<sub>40</sub>(10)) + 1 = ceiling(.624) + 1 = 1 + 1 = 2  
   4.  T2: Secondary Tree Index = 5
       1.  ceiling(Log<sub>40</sub>(100000)) + 1 = ceiling(3.12) + 1 = 4 + 1 = 5   
   4.  T2: Secondary Tree Index = 5
       1.  ceiling(Log<sub>40</sub>(100000)) + 1 = ceiling(3.12) + 1 = 4 + 1 = 5  

| Attribute\Relation |    T1    |    T2    |    T3    |    T4    |      
|-------------------:|:--------:|:--------:|:--------:|:--------:|
|       Tuples       |  2000    |  20000   |    20    |  200000  | 
|       Pages        |  1000    |  10000   |    10    |  100000  |  
      
### Solution Steps
1.  Find the Relation with the least number of tuples and compare the cost of of joining against the other
   1. T3 < T1 < T2 < T4
   
| T3 ⋈<sub>attr</sub> TX Cost   |    T1    |    T2    |    T4    |   
|-------------------------------:|:--------:|:--------:|:--------:|
|       Tuples                   |  2000    |  20000   |    20    |  
| Hash Inner Nested Loop         |          |     ✓    |          |  
|Primary BTree Inner Nested Loop |     ✓    |          |          |  
|Seconary BTree Inner Nested Loop|          |          |    ✓     |  
|Nested Loops                    |     ✓    |          |     ✓    |   
|Hash Join                       |     ✓    |          |     ✓    |    

Hash-INL	Index nested loops using Hash Index
Primary-BTree-INL	Index nested loops using Primary BTree
Sec-BTree-INL	Index nested loops using Secondary BTree
NL	Nested loops
HashJoin	Hash Join
