### **Rest Students Details API Testing with Postman Newman**

This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API.

### **Features**

- Tests for GET, POST, PUT, DELETE requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations

## API Documentation:

- https://documenter.getpostman.com/view/34581549/2sA3QniEST

### **Technology used:**

- Postman
- Newman

### **Prerequisite:**

- Node Js
- Newman
- Newman Html Report Library

### **Installation**

1. Postman: If you haven't already, [download and install Postman.](https://www.postman.com/downloads/)
2. Clone the repository:

```console
git clone https://github.com/ifoysalahmmed/Automated-Testing-of-Rest-Students-Details-API-with-Newman-Report.git
```

3. Import the Postman collection:
   - Open Postman.
   - Click on the Import button.
   - Select the file from the repository.
4. Import the Postman environment:
   - In Postman, click on the gear icon in the top right corner.
   - Select **Import** and choose the file.
5. Newman and Report Installation Process:
   - Newman Install Command:
   ```console
   npm install -g newman
   ```
   - Newman Html Report Install Command:
   ```console
   npm install -g newman-reporter-htmlextra
   ```

### **Usage**

1. Select Environment:
   - In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
2. Run Collection:
   - Select the imported collection from the Collections sidebar.
   - Click on the Runner button to open the collection runner.
   - Select the desired environment.
   - Click Start Test to run the collection.
3. View Results:
   - Once the tests are complete, view the results in the Runner tab.
   - Detailed test results can be viewed for each request.

## **Testing**

## Test Case Scenarios:

## _**1. Get All Students Details**_

### Request URL: https://thetestingworldapi.com/api/studentsDetails

### Request Method: GET

### Response Body:

```console
[
    {
        "id": 10279307,
        "first_name": "Ms.",
        "middle_name": "Melody",
        "last_name": "Sanford",
        "date_of_birth": "2024-05-22"
    },
    {
        "id": 10279306,
        "first_name": "T5",
        "middle_name": "M5",
        "last_name": "L5",
        "date_of_birth": "1990-02-03 00:00:00"
    },
    So on...
]
```

## _**2. Create A Student Details**_

### Request URL: https://thetestingworldapi.com/api/studentsDetails

### Request Method: POST

### Pre-request Script:

```console
var firstName = pm.variables.replaceIn('{{$randomFirstName}}');
pm.environment.set("FirstName", firstName);

var lastName = pm.variables.replaceIn('{{$randomLastName}}');

var middleName = firstName + lastName;
pm.environment.set("MiddleName", middleName);

pm.environment.set("LastName", lastName);

var year = Math.floor(Math.random() * (2050 - 1980 + 1)) + 1980;
var month = Math.floor(Math.random() * 12) + 1;
month = (month < 10) ? '0' + month : month;
var day = Math.floor(Math.random() * 28) + 1;
day = (day < 10) ? '0' + day : day;
var dateOfBirth = day + '/' + month + '/' + year;
pm.environment.set("DateOfBirth", dateOfBirth);
```

### Request Body:

```console
{
    "first_name": "{{FirstName}}",
    "middle_name": "{{MiddleName}}",
    "last_name": "{{LastName}}",
    "date_of_birth": "{{DateOfBirth}}"
}
```

### Response Body:

```console
{
    "id": 10279308,
    "first_name": "Catherine",
    "middle_name": "CatherineCremin",
    "last_name": "Cremin",
    "date_of_birth": "15/06/2016"
}
```

## _**3. Verify Created Student Details**_

### Request URL: https://thetestingworldapi.com/api/studentsDetails/StudentID

### Request Method: GET

### Response Body:

```console
{
    "status": "true",
    "data": {
        "id": 10279308,
        "first_name": "Catherine",
        "middle_name": "CatherineCremin",
        "last_name": "Cremin",
        "date_of_birth": "15/06/2016"
    }
}
```

## _**4. Update Student Details**_

### Request URL: https://thetestingworldapi.com/api/studentsDetails/StudentID

### Request Method: PUT

### Pre-request Script:

```console
var firstName = pm.variables.replaceIn('{{$randomFirstName}}');
pm.environment.set("FirstName", firstName);

var lastName = pm.variables.replaceIn('{{$randomLastName}}');

var middleName = firstName + lastName;
pm.environment.set("MiddleName", middleName);

pm.environment.set("LastName", lastName);

var year = Math.floor(Math.random() * (2050 - 1980 + 1)) + 1980;
var month = Math.floor(Math.random() * 12) + 1;
month = (month < 10) ? '0' + month : month;
var day = Math.floor(Math.random() * 28) + 1;
day = (day < 10) ? '0' + day : day;
var dateOfBirth = day + '/' + month + '/' + year;
pm.environment.set("DateOfBirth", dateOfBirth);
```

### Request Body:

```console
{
    "id": {{StudentID}},
    "first_name": "{{FirstName}}",
    "middle_name": "{{MiddleName}}",
    "last_name": "{{LastName}}",
    "date_of_birth": "{{DateOfBirth}}"
}
```

### Response Body:

```console
{
    "status": "true",
    "msg": "update  data success"
}
```

## _**5. Check After The Update**_

### Request URL: https://thetestingworldapi.com/api/studentsDetails/StudentID

### Request Method: GET

### Response Body:

```console
{
    "status": "true",
    "data": {
        "id": 10279308,
        "first_name": "Florence",
        "middle_name": "FlorenceHarvey",
        "last_name": "Harvey",
        "date_of_birth": "06/06/2002"
    }
}
```

## _**6. Create Technical Skills**_

### Request URL: https://thetestingworldapi.com/api/technicalskills

### Request Method: POST

### Pre-request Script:

```console
var languages = [
    "Java", "Python", "JavaScript", "C++", "Ruby", "Swift",
    "Go", "Rust", "Scala", "Kotlin", "TypeScript", "PHP",
    "Perl", "Haskell", "Elixir", "Clojure", "Objective-C",
    "Dart", "Lua", "F#", "Shell", "R", "MATLAB", "Groovy",
    "Visual Basic", "Ada", "Fortran", "Pascal", "Assembly"
];

var randomIndex1 = Math.floor(Math.random() * languages.length);
var randomLanguage1 = languages[randomIndex1];
pm.environment.set("Language1", randomLanguage1);

var randomIndex2;
do {
    randomIndex2 = Math.floor(Math.random() * languages.length);
} while (randomIndex2 === randomIndex1);

var randomLanguage2 = languages[randomIndex2];
pm.environment.set("Language2", randomLanguage2);

var randomNumber = Math.floor(Math.random() * 10);
var randomYearExp = randomNumber + ' ' + 'year';
pm.environment.set("YearExp", randomYearExp);

var randomUsedNumber = Math.floor(Math.random() * 2);
var randomLastUsed = randomUsedNumber === 0 ? "Recent" : "1 year";
pm.environment.set("LastUsed", randomLastUsed);
```

### Response Body:

```console
{
    "id": 1,
    "language": [
        "{{Language1}}",
        "{{Language2}}"
    ],
    "yearexp": "{{YearExp}}",
    "lastused": "{{LastUsed}}",
    "st_id": {{StudentID}}
}
```

### Response Body:

```console
{
    "status": "true",
    "msg": "Add  data success"
}
```

## _**7. Create Student Address**_

### Request URL: https://thetestingworldapi.com/api/addresses

### Request Method: POST

### Pre-request Script:

```console
var houseNumber = pm.variables.replaceIn("{{$randomInt}}");
pm.environment.set("HouseNumber", houseNumber);

var city = pm.variables.replaceIn("{{$randomCity}}");
pm.environment.set("City", city);

var state = pm.variables.replaceIn("{{$randomCity}}");
pm.environment.set("State", state);

var country = pm.variables.replaceIn("{{$randomCountry}}");
pm.environment.set("Country", country);

var std_Code1 = pm.variables.replaceIn("{{$randomCreditCardMask}}");
pm.environment.set("Std_Code1", std_Code1);

var std_Code2 = pm.variables.replaceIn("{{$randomCreditCardMask}}");
pm.environment.set("Std_Code2", std_Code2);

var home1 = pm.variables.replaceIn("{{$randomPhoneNumber}}");
pm.environment.set("Home1", home1);

var home2 = pm.variables.replaceIn("{{$randomPhoneNumber}}");
pm.environment.set("Home2", home2);

var mobile1 = pm.variables.replaceIn("{{$randomPhoneNumber}}");
pm.environment.set("Mobile1", mobile1);

var mobile2 = pm.variables.replaceIn("{{$randomPhoneNumber}}");
pm.environment.set("Mobile2", mobile2);
```

### Request Body:

```console
{
    "Permanent_Address": {
        "House_Number": "{{HouseNumber}}",
        "City": "{{City}}",
        "State": "{{City}}",
        "Country": "{{Country}}",
        "PhoneNumber": [
            {
                "Std_Code": "{{Std_Code1}}",
                "Home": "{{Home1}}",
                "Mobile": "{{Mobile1}}"
            },
            {
                "Std_Code": "{{Std_Code2}}",
                "Home": "{{Home2}}",
                "Mobile": "{{Mobile2}}"
            }
        ]
    },
    "stId": {{StudentID}}
}
```

### Response Body:

```console
{
    "status": "true",
    "msg": "Add  data success"
}
```

## _**8. Get Student Full Details**_

### Request URL: https://thetestingworldapi.com/api/FinalStudentDetails/StudentID

### Request Method: GET

### Response Body:

```console
{
    "status": "true",
    "data": {
        "first_name": "Florence",
        "middle_name": "FlorenceHarvey",
        "last_name": "Harvey",
        "date_of_birth": "06/06/2002",
        "TechnicalDetails": [
            {
                "id": 794037,
                "language": [
                    "Ada",
                    "Perl"
                ],
                "yearexp": "1 year",
                "lastused": "Recent",
                "st_id": "10279308"
            }
        ],
        "Address": [
            {
                "Permanent_Address": {
                    "House_Number": "541",
                    "City": "Kuvalisview",
                    "State": "Kuvalisview",
                    "Country": "San Marino",
                    "PhoneNumber": [
                        {
                            "Std_Code": "3019",
                            "Home": "320-992-7604",
                            "Mobile": "302-798-0984"
                        },
                        {
                            "Std_Code": "3037",
                            "Home": "756-933-4009",
                            "Mobile": "736-987-8256"
                        }
                    ]
                },
                "Current_Address": null,
                "stId": "10279308"
            }
        ]
    }
}
```

## _**9. Delete Student Record**_

### Request URL: https://thetestingworldapi.com/api/studentsDetails/StudentID

### Request Method: DELETE

### Response Body:

```console
{
    "status": "true",
    "msg": "Delete  data success"
}
```

## _**10. Check After The Delete**_

### Request URL: https://thetestingworldapi.com/api/FinalStudentDetails/StudentID

### Request Method: GET

### Response Body:

```console
{
    "status": "false",
    "msg": "No File Found"
}
```

## Run Command:

- Run Command for Console:

```console
newman run Rest_Students_Details_API.postman_collection.json -e Rest_Students_Details_API.postman_environment.json
```

- Run Command for Report:

```console
newman run Rest_Students_Details_API.postman_collection.json -e Rest_Students_Details_API.postman_environment.json -r cli,htmlextra
```

## Newman Report Summary:
