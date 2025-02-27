Click the triple dots button at the end of the field to see the actions that can be performed for the selected field.

## Initialize arrays, add and delete elements

Actions are determined by the type of the selected field. For instance, clicking the triple dots button of an array-typed field will present the **Initialize Array** option. After initializing the array, elements can be added by clicking the **+ Add Element** button. Additionally, any array element can be deleted by clicking the triple dots button on that element.

<img src="../../assets/data-mapper/initialize-arrays.gif" class="cInlineImage-full"/>

## Add/Edit constant values/expressions 

If a particular field is empty and accepting a constant/expression, you will see the **Add value** action after clicking the triple dots button. This will open up the expression editor. You can provide a constant value or construct any complex expression via it.

1. Add a hard-coded visa type for foreign students.

    ```ballerina
    const D_TIER_4_VISA = "D-tier-4";
    ```

    <img src="../../assets/data-mapper/constant-values-1.gif" class="cInlineImage-full"/>

    If a particular field is having a value, you will see the **Edit value** action once you click the triple dots button.
    
2. Add an 'F' suffix to the `student id` of each foreign student.

    <img src="../../assets/data-mapper/constant-values-2.gif" class="cInlineImage-full"/>

3. Fill in the `totalCredits` field by getting the summation of the credits in each CS course.

    !!! Tip 
        You can use the [`reduce()`](https://lib.ballerina.io/ballerina/lang.array/0.0.0/functions#reduce) array function for this by passing the combining function below to get the sum.

    ```ballerina
    var totalCredits = function(int total, record {string id; string name; int credits;} course) returns int => total + (course.id.startsWith("CS") ? course.credits : 0);
    ```

    <img src="../../assets/data-mapper/constant-expressions.gif" class="cInlineImage-full"/>