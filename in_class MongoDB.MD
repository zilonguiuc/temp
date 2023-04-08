# University of Illinois MongoDB Database Design (Student Collections)

We will create a database called "university" that will store information about the students

### Step 1: Create a University Database
Create a new database called "university" using the MongoDB shell.
```javascript
use university

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
 
 
]```javascript
db.students.insert({
  name: "John Doe",
  major: "Computer Science",
  GPA: 3.5,
  enrolled_courses: [
    { course_name: "Database Systems", course_grade: "A" },
    { course_name: "Web Development", course_grade: "B" }
  ]
})


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
db.students.insertMany([
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

### Step 5: Show All Documents
Retrieve all documents from the "students" collection and display them in the MongoDB shell.
```javascript
db.students.find().pretty()

```
### Step 6: Delete a Document
Delete the document with the name "Bob Johnson" from the "students" collection.
```javascript
db.students.deleteOne({ name: "Bob Johnson" })

```
### Step 7: Update a Field
Update the "GPA" field of the document with the name "John Doe" to 3.7.
```javascript
db.students.updateOne({ name: "John Doe" }, { $set: { GPA: 3.7 } })

```
### Step 8: Find Documents with a Single Condition
Retrieve the document from the "students" collection with the major "Mathematics".
```javascript
db.students.findOne({ major: "Mathematics" })

```
### Step 9: Find Documents with Multiple Conditions
Retrieve all documents from the "students" collection with the major "Computer Science" and a course named "Web Development".
```javascript
db.students.find({ major: "Computer Science", "enrolled_courses.course_name": "Web Development" }).pretty()

```
### Step 10: Sort Documents
Retrieve all documents from the "students" collection and sort them by "GPA" in descending order.
```javascript
db.students.find().sort({ GPA: -1 }).pretty()

```
### Step 11: Update a Field and Remove Another Field
Update the document in the "students" collection with the email "jdoe@illinois.edu" to remove the "enrolled_courses" field.
```javascript
db.students.updateOne({ name: "John Doe" }, { $unset: { enrolled_courses: 1 } })

```
### Step 12: Remove a Field for a Certain Document
Remove the "major" field from the document with the name "Samantha Lee" in the "students" collection.
```javascript
db.students.updateOne({ name: "Samantha Lee" }, { $unset: { major: 1 } })

```
### Step 13: Add a Field for a Student
Add a new field called "graduation_year" with a value of 2022 to the document with the name "David Kim".
```javascript
db.students.updateOne({ name: "David Kim" }, { $set: { graduation_year: 2022 } })

```
### Step 14: Add a Field to All Documents
Add a new field called "status" with a value of "enrolled" to all documents in the "students" collection.
```javascript
db.students.updateMany({}, { $set: { status: "enrolled" } })

```
### Step 15: Count Documents
Count the number of documents in the "students" collection.
```javascript
db.students.count()

```
### Step 16: Find Documents that Match a Regular Expression
Find all documents in the "students" collection where the name contains the string "doe".
```javascript
db.students.find({ name: { $regex: /doe/i } }).pretty()

```
### Step 17: Find Documents that Match a Range of Values
Find all documents in the "students" collection where the GPA is between 3.5 and 3.9.
```javascript
db.students.find({ GPA: { $gt: 3.5, $lt: 3.9 } }).pretty()

```

### Step 18: Limit the Number of Documents Returned in a Query
Retrieve the first two documents from the "students" collection.
```javascript
db.students.find().limit(2)

```
### Step 19: Remove a Collection
Remove the "students" collection from the "university" database.
```javascript
db.students.drop()

```

### Step 20: Delete the Database
Delete the "university" database.
```javascript
use university
db.dropDatabase()

```

Good Job!
