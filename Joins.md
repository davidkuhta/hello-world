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
   1.  floor((Page Size * Fill Factor)/ Dir Entry Size)
   2.  floor ((400\*0.5/5)/ 5)
   3.  40 DE/page
   
|Fill Factor|Dir. Entry Size|Tuple Size|Page Size|DE/Page|    
|:---------:|:-------------:|:--------:|:-------:|:-----:|     
|     0.5   |    5 bytes    | 100 bytes|400 bytes|  40   |  

2. Compute the Tuples Per Page
   1.  floor((Page Size * Fill Factor)/ Dir Entry Size)
   2.  floor ((400\*0.5/100)/ 5)
   3.  2 Tups/page

|Fill Factor|Dir. Entry Size|Tuple Size|Page Size|DE/Page|Tups/Page|    
|:---------:|:-------------:|:--------:|:-------:|:-----:|:-------:|   
|     0.5   |    5 bytes    | 100 bytes|400 bytes|  40   |    2    |  

3. Compute the Page Sizes for each of the relations T1 thru T4. (Note: we need to end up in units of pages!)
   1.  T1 = (<sup>2000 Tuples</sup>&frasl;<sub>2 <sup>tuples</sup>/Page</sub>) = 1000 Pages  
   1.  T2 = (20000 Tuples / 2 (Tuples/Page)) = 10000 Pages  
   1.  T3 = (20 Tuples / 2 (Tuples/Page)) = 10 Pages  
   1.  T4 = (200000 Tuples / 2 (Tuples/Page)) = 100000 Pages  

| Attribute\Relation |    T1    |    T2    |    T3    |    T4    |      
|-------------------:|:--------:|:--------:|:--------:|:--------:|
|       Tuples       |  2000    |  20000   |    20    |  200000  | 
|       Pages        |  1000    |  10000   |    10    |  100000  |  
      
### Solution Steps
1.  
