### Aggregate input and output fields

You can derive one output parameter by combining two or more input parameters. In this example, the value of the `fullName` output parameter is a combination of the values of the `firstName` and `lastName` input parameters. You can map them as shown below.

!!! Info
    To aggregate fields, you can map two or more fields to the same output field. The Data Mapper will automatically combine the two fields and assign them to the output field. By default, the fields will be combined with a plus operator. If you want to use a different operator or method to combine two fields, click the **Code** button and customize the expression using the expression editor.

<img src="https://wso2.com/ballerina/vscode/docs/img/visual-programming/datamapper/concatination.gif" class="cInlineImage-full"/>