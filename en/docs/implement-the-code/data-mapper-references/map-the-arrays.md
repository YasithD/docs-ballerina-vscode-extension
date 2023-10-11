To convert from one array type to another, map the input array to the output array. The arrays will be connected with a blue line if they are compatible, and with a red line if they are incompatible. You can utilize the Ballerina query support for this conversion. In the Data Mapper, select the array and click the code action button (bulb sign), then select **Convert to query**. This will convert the mapping to a query, allowing you to map between the array types within the query.

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