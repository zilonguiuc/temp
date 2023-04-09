# MongoDB In-Class Excise  - University of Illinois MongoDB Database Design (Student Collections) 

We will create a database called "university" that will store information about the students

### Step 1: Create a University Database
Create a new database called "university" using the MongoDB shell.
```javascript
 

```
### Step 2: Create a "students" Collection
Create a new collection called "students" in the "university" database.
```javascript
db.createCollection("students")

```
### Step 3: Insert a Document
Insert a new document into the "students" collection with the following properties:
 ```
 {
  name: "John Doe",
  major: "Computer Science",
  GPA: 3.5,
  enrolled_courses: [
    { course_name: "Database Systems", course_grade: "A" },
    { course_name: "Web Development", course_grade: "B" }
  ]
}
```
 
 
 ```javascript
 
 ```


### Step 4: Insert Multiple Documents
Insert the following documents into the "students" collection:
 
 ```
  {
    name: "Jane Smith",
    major: "Mathematics",
    GPA: 3.9,
    enrolled_courses: [
      { course_name: "Calculus", course_grade: "A+" },
      { course_name: "Statistics", course_grade: "A" }
    ]
  },
  {
    name: "Bob Johnson",
    major: "English",
    GPA: 3.2,
    enrolled_courses: [
      { course_name: "American Literature", course_grade: "B+" },
      { course_name: "Creative Writing", course_grade: "A-" }
    ]
  },
  {
    name: "Samantha Lee",
    major: "Biology",
    GPA: 3.8,
    enrolled_courses: [
      { course_name: "Genetics", course_grade: "A" },
      { course_name: "Anatomy", course_grade: "A+" }
    ]
  },
  {
    name: "David Kim",
    major: "Economics",
    GPA: 3.4,
    enrolled_courses: [
      { course_name: "Macroeconomics", course_grade: "B+" },
      { course_name: "Microeconomics", course_grade: "B" }
    ]
  }
]) 
```

 ```javascript
 

```

### Step 5: Show All Documents
Retrieve all documents from the "students" collection and display them in the MongoDB shell.
```javascript
 

```
### Step 6: Delete a Document
Delete the document with the name "Bob Johnson" from the "students" collection.
```javascript
 

```
### Step 7: Update a Field
Update the "GPA" field of the document with the name "John Doe" to 3.7.
```javascript
 

```
### Step 8: Find Documents with a Single Condition
Retrieve the document from the "students" collection with the major "Mathematics".
```javascript
 

```
### Step 9: Find Documents with Multiple Conditions
Retrieve all documents from the "students" collection with the major "Computer Science" and a course named "Web Development".
```javascript
 

```
### Step 10: Sort Documents
Retrieve all documents from the "students" collection and sort them by "GPA" in descending order.
```javascript
 

```
### Step 11: Update a Field and Remove Another Field
Update the document in the "students" collection with the email "jdoe@illinois.edu" to remove the "enrolled_courses" field.
```javascript
 

```
### Step 12: Remove a Field for a Certain Document
Remove the "major" field from the document with the name "Samantha Lee" in the "students" collection.
```javascript
 

```
### Step 13: Add a Field for a Student
Add a new field called "graduation_year" with a value of 2022 to the document with the name "David Kim".
```javascript
 

```
### Step 14: Add a Field to All Documents
Add a new field called "status" with a value of "enrolled" to all documents in the "students" collection.
```javascript
 

```
### Step 15: Count Documents
Count the number of documents in the "students" collection.
```javascript
 

```
### Step 16: Find Documents that Match a Regular Expression
Find all documents in the "students" collection where the name contains the string "doe".
```javascript
 

```
### Step 17: Find Documents that Match a Range of Values
Find all documents in the "students" collection where the GPA is between 3.5 and 3.9.
```javascript
 

```

### Step 18: Limit the Number of Documents Returned in a Query
Retrieve the first two documents from the "students" collection.
```javascript
 

```
### Step 19: Remove a Collection
Remove the "students" collection from the "university" database.
```javascript
 

```

### Step 20: Delete the Database
Delete the "university" database.
```javascript
 

```

Good Job!
