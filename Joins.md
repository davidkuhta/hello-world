# Join Problem Walkthroughs
## Example 1
### Stats
|Fill Factor|Dir. Entry Size|Tuple Size|Page Size|DE/Page|Tups/Page|    
|-----------|---------------|----------|---------|-------|---------|   
|     0.5   |    5 bytes    | 100 bytes|400 bytes|  40   |    2    |

### Relations
| Attribute\Relation |    T1    |    T2    |    T3    |    T4    |    
|--------------------|----------|----------|----------|----------|
|       Tuples       |  2000    |  20000   |    20    |  200000  |  
| Primary Hash Index |          |     ✓    |          |          |  
|Secondary Hash Index|     ✓    |          |          |          |  
| Primary Tree Index |          |          |    ✓     |     ✓    |  
|Secondary Tree Index|          |     ✓    |          |     ✓    |  

### Prepartion Steps 
1. Compute the Directory Entries Per Page
   1. floor(\frac{Page Size * Fill Factor}{Dir Entry Size})
   2. floor(\frac{400 * 0.5}{5}) =
   3. *40 \frac{Directory Entries}{Per Page}
   2. Floor((Page Size * Fill Factor)/ Tuple Size) = floor ((400\*0.5/5)/ 5) = 2 Tups/page
1. Compute the Tuples Per Page
2. Compute the Page Sizes for each of the relations T1 thru T4.

| Attribute\Relation |    T1    |    T2    |    T3    |    T4    |     
|--------------------|----------|----------|----------|----------|    
|       Tuples       |  2000    |  20000   |    20    |  200000  |
      
3. Step 3
