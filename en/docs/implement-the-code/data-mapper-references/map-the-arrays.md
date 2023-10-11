To convert from one array type to another, map the input array to the output array. If the arrays are compatible, they will be connected with a blue line. If they are incompatible, the connecting line will appear in red.

!!! Info
    You can use the Ballerina query support to convert one array type to another. To use a query in a Data Mapper, select the array by clicking on it. Then, it will provide you with several buttons. Click the code action button (bulb sign) and select **Convert to query**. Then, the Data Mapper will convert the mapping to a query. Next, move into the query and do the mapping between the array types.

<img src="../../assets/data-mapper/map-the-arrays-1.gif" class="cInlineImage-full"/>

## Process the data further

You can further process the data within the query expression. Currently, the Data Mapper supports the following intermediate clauses.

| Clause                    	| Description                                                          	|
|---------------------------------	|----------------------------------------------------------------------	|
| `Where`                	| Filter data based on a given condition.                                 	|
| `Let`   	| Define local variables within the query expression.                   	|
| `Limit`  	| Limit the number of elements returned from the query expression.                                               	|
| `Order by`             	| Sort data within the query expression in `ascending` or `descending` order.	|
| `Join`   	| Perform an inner join.                  	|
| `Outer join`  	| Perform a left outer join.                                              	|

<img src="../../assets/data-mapper/map-the-arrays-2.gif" class="cInlineImage-full"/>

Once the array type mapping is completed, select the transform function name in the top breadcrumb bar to navigate to the root view of mapping.