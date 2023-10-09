### Diagnose and fix mapping errors

Use the `toBalString` lang lib function to convert the int to string as shown below.

!!! Info
    When you map the input fields to output fields, some of them might not be compatible due to type mismatch. In this example, if you map the `person age` to the `student age`, it will result in a type mismatch error since the `input age` type is an integer and the `output age` type is a string. The Data Mapper will connect the two fields with a red line and show an alert sign. You can see the error by hovering over the alert sign. It will show the `incompatible types: expected 'string', found 'int'` error. To fix the error, hover over the alert sign and click **Fix by editing expression**. Then, the Data Mapper will open the expression editor for the specific expression. You can modify the expression using it to return a string.

<img src="https://wso2.com/ballerina/vscode/docs/img/visual-programming/datamapper/fix-diagnostics.gif" class="cInlineImage-full"/>

!!! Info
    Once you fix the error, the connection appears in blue to indicate that there are no errors.