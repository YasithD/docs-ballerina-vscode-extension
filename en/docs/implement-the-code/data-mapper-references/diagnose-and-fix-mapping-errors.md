During the mapping process, you may encounter errors due to type mismatches between input and output fields. Once these errors are fixed, the connection will appear in blue to indicate that there are no errors.

!!! Info
    In this example, if you map the `person age` to the `student age`, it will result in a type mismatch error since the `input age` type is an integer and the `output age` type is a string. The Data Mapper will connect the two fields with a red line and show an alert sign. You can see the error by hovering over the alert sign. It will show the `incompatible types: expected 'string', found 'int'` error. To fix the error, hover over the alert sign and click **Fix by editing expression**. Then, the Data Mapper will open the expression editor for the specific expression. You can modify the expression using it to return a string.

<img src="../../assets/data-mapper/diagnose-and-fix-mapping-errors.gif" class="cInlineImage-full"/>