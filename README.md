# Project Management Form

This project is a web-based form for managing project data, developed as a mini-project during an internship. The form stores user data in JSONPowerDB and supports REST APIs and serverless technology. Projects can be added or updated based on their project ID. The form automatically checks the project ID and uses APIs to populate other input fields, allowing users to update project details as needed. The application uses AJAX requests for smooth and fast interactions, and it can store various data types such as numbers, strings, dates, etc.

## Website
You can access the project [here](https://kunal5163.github.io/login2xplore-project/).

## Features
- Add new projects.
- Update existing projects based on project ID.
- Automatically fetch and populate project data based on project ID.
- Store various data types such as numbers, strings, dates, etc.
- Use AJAX for seamless and fast interactions.

## Input Fields
- **Project ID**: Unique identifier for each project (Primary Key).
- **Project Name**: Name of the project.
- **Assigned To**: Person assigned to the project.
- **Assignment Date**: Date the project was assigned.
- **Deadline**: Project deadline date.

## Benefits of Using JSONPowerDB
- Can store structured, semi-structured, and unstructured data, including various file types and big data.
- Dynamic relational constraints during CRUD operations, allowing relational data management without pre-defining primary keys, foreign keys, unique keys, databases, tables, etc.
- Free from technology constraints; low-code and easy to use from any technology via HTTP REST API.
- Minimal learning curve, enabling faster development, reduced time to market, and lower development costs.
- Assists developers in managing databases using various tools and techniques.

## Usage
To execute commands and interact with the database, follow the examples below:

### Execute API
```javascript
var baseUrl = "http://api.login2explore.com:5577";

function executeCommand(reqString, apiEndPointUrl) {
    var url = baseUrl + apiEndPointUrl;
    var jsonObj;
    
    $.post(url, reqString, function (result) {
        jsonObj = JSON.parse(result);
    }).fail(function (result) {
        var dataJsonObj = result.responseText;
        jsonObj = JSON.parse(dataJsonObj);
    });
    return jsonObj;
}
```
### Create Put Request String
```javascript
function createPUTRequest(connToken, jsonObj, dbName, relName) {
    var putRequest = "{\n"
            + "\"token\" : \"" + connToken + "\","
            + "\"dbName\": \"" + dbName + "\",\n"
            + "\"cmd\" : \"PUT\",\n"
            + "\"rel\" : \"" + relName + "\","
            + "\"jsonStr\": \n" + jsonObj + "\n"
            + "}";
    return putRequest;
}
```
### Example of Creating and Executing a PUT Request
```javascript
ar token = 'YOUR_TOKEN';
var dbname = 'PROJECT-MANAGEMENT-DB';
var relation = "PROJECT-TABLE";
var projectData = {
    Project_id: "1",
    Project_name: "Project Management System",
    Assigned_to: "John Doe",
    Assignment_date: "2024-07-17",
    Deadline: "2024-08-17"
};
var jsonObj = JSON.stringify(projectData);
var putRequest = createPUTRequest(token, jsonObj, dbname, relation);

var response = executeCommand(putRequest, "/api/iml");
console.log(response);
```
