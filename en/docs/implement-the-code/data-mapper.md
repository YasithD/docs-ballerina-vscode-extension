# Data Mapper

The Data Mapper of Ballerina is a tool designed to facilitate seamless data transformation through an user interface. When you engage with the Data Mapper via its interface, it automatically generates the necessary Ballerina source code to execute the data mapping. This feature ensures that the Ballerina source code serves as the single source of truth for the Visual Data Mapper, allowing you to open, edit, and manage existing data mappings crafted through the source code without compromising the user experience.

In the subsequent sections, we will walk through a practical scenario where the Data Mapper is employed to transform input records into a specific output record format. This hands-on approach aims to provide a clear understanding of the Data Mapper’s functionality and its application in real-world data transformation tasks.

## Sample use case

Imagine a scenario where you have records of **students** and the **courses** they are enrolled in, both in distinct formats. Your task is to transform these input records into a consolidated format that provides a comprehensive view of each student's details and their enrolled courses.

Below are the sample input records:

**Input 1: Person**

```json
{
    "id": "1001",
    "firstName": "Vinnie",
    "lastName": "Hickman",
    "age": 15,
    "country": "UK"
}
```

**Input 2: Course**

```json
{
    "id": "CS6002",
    "name": "Computation Structures",
    "credits": 4
}
```
Your goal is to transform these inputs into the following output format:

**Output**

```json
{
    "id": "1001F",
    "fullName": "Vinnie Hickman",
    "age": "15",
    "courses": [
        {"title": "CS6002 - Computation Structures", "credits": 4},
        {"title": "CS6003 - Circuits and Electronics", "credits": 3},
        {"title": "CS6004 - Signals and Systems", "credits": 3}
    ],
    "totalCredits": 10,
    "visaType": "D tier-4"
}
```

## Creating the transformation function

The Data Mapper allows you to visually map the input data structures to the expected output structure, generating the Ballerina code necessary for the transformation.

### Opening Data Mapper:
You can open the Data Mapper through either the **Visualize CodeLens** or the **Diagram View**.

#### Via Visualize CodeLens:
  1. In your `main.bal` file, define an empty expression-bodied function.
     ```ballerina
     function name() => ();
     ```
  2. Click the **Visualize** CodeLens displayed above the function to open the Data Mapper view.
     ![Open via CodeLens](https://wso2.com/ballerina/vscode/docs/img/visual-programming/datamapper/open-via-code-lens.gif)

#### Via Diagram View:
  1. Open the file in Diagram View.
  2. Click the **+ Component** button.
  3. Select the desired file.
  4. Click **Data Mapper** in the **Add Constructs** pane.
     ![Open via Diagram View](https://wso2.com/ballerina/vscode/docs/img/visual-programming/datamapper/open-via-diagram.gif)

### Defining inputs and output:
After opening the Data Mapper, define the input and output records for the transformation function. Inputs and output can be any data type in Ballerina. This example converts JSON and an array of JSON to JSON, and thereby, you can use Ballerina record types as inputs and output.

In the Data Mapper form, you have several options to provide the input and output records. If the records are already defined in your package, you can select one of those. If you are starting from scratch, you can either create the record from the [Record Editor view](https://wso2.com/ballerina/vscode/docs/references/record-editor/) or import a JSON to create a matching record.

This example imports JSON files and creates the records as shown below.
![Define Inputs and Output](https://wso2.com/ballerina/vscode/docs/img/visual-programming/datamapper/define-inputs-n-output.gif)

### Define the mappings

Map the input fields with the fields in the JSON output as described below. Once you've configured the transformation function using the Data Mapper, the tool will generate the necessary Ballerina code for you.

- [Basic mapping](references/data-mapper/basic-mapping.md)
- [Diagnose and fix mapping errors](references/data-mapper/diagnose-and-fix-mapping-errors.md)
- [Aggregate input and output fields](references/data-mapper/aggregate-input-and-output-fields.md)
- [Map the arrays](references/data-mapper/map-the-arrays.md)
- [Add local variables](references/data-mapper/add-local-variables.md)
- [Manipulate fields without drawing connections](references/data-mapper/manipulate-fields-without-drawing-connections.md)

After mapping the data with the instructions provided in the above sections, your transformation code will look like this.

```ballerina
import ballerina/io;

type Person record {
    string id;
    string firstName;
    string lastName;
    int age;
    string country;
};

type Course record {
    string id;
    string name;
    int credits;
};

type Student record {
    string id;
    string fullName;
    string age;
    record {
        string title;
        int credits;
    }[] courses;
    int totalCredits;
    string visaType;
};

const D_TIER_4_VISA = "D-tier-4";

var totalCredits = function(int total, record {string id; string name; int credits;} course) returns int => total + (course.id.startsWith("CS") ? course.credits : 0);

function transform(Person person, Course[] courses) returns Student => let var isForeign = person.country != "LK" in {
    id: person.id + (isForeign ? "F" : ""),
    age: person.age.toString(),
    fullName: person.firstName + " " + person.lastName,
    courses: from var coursesItem in courses
        where coursesItem.id.startsWith("CS")
        select {
            title: coursesItem.id + " - " + coursesItem.name,
            credits: coursesItem.credits
        },
    visaType: isForeign ? D_TIER_4_VISA : "n/a",
    totalCredits: courses.reduce(totalCredits, 0)
};
```

## Testing the code

It’s crucial to validate the data mapping functionality through testing. Below is a step-by-step guide on crafting and executing a Ballerina test to ensure the transformation function works as expected.

### Crafting the test:
Create a Ballerina test file and write a test function (For more information on Ballerina Tests, check the following [documentation](https://ballerina.io/learn/test-ballerina-code/test-a-simple-function)). This function should invoke the `transform` function with sample `Person` and `Course` records, then assert whether the output matches the expected `Student` record.

Here’s a sample test function:

```ballerina
import ballerina/test;

@test:Config {}
function testTransformFunction() {
    Person testPerson = {
        id: "1001",
        firstName: "Vinnie",
        lastName: "Hickman",
        age: 15,
        country: "UK"
    };

    Course[] testCourses = [
        {
            id: "CS6002",
            name: "Computation Structures",
            credits: 4
        }
    ];

    Student expectedStudent = {
        id: "1001F",
        fullName: "Vinnie Hickman",
        age: "15",
        courses: [
            {title: "CS6002 - Computation Structures", credits: 4}
        ],
        totalCredits: 4,
        visaType: "D-tier-4"
    };

    Student resultStudent = transform(testPerson, testCourses);
    test:assertEquals(resultStudent, expectedStudent, msg = "Test Failed!");
}
```

### Executing the test:
- Open a terminal in the directory containing your Ballerina project.
- Run the command `ballerina test` to execute the test suite. Ballerina will compile and run the test function, providing you with real-time feedback on the test results.

### Verifying test success:
If the test function is successful, you’ll see an output similar to the following:

```bash
Compiling source
    <Your_Package_Name>

Running Tests

    <Your_Package_Name>


        1 passing
        0 failing
        0 skipped
```

This output indicates that the `transform` function correctly transforms the input records into the desired output format.

## Conclusion

With this hands-on scenario, you've learned how to use the Data Mapper in the Ballerina language to simplify the process of transforming input records into a specific output record format. By visually mapping data structures and generating the necessary Ballerina code, the Data Mapper offers a user-friendly approach to data transformation tasks, validated through careful testing to ensure reliability and accuracy.