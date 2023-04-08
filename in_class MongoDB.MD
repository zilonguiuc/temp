# University of Illinois MongoDB Database Design

We will create a database called "illinois_university" that will store information about the students, instructors, and courses at the University of Illinois. Here is an example schema for the database:

**students:** 

* Each document will represent a student and will have the following fields: `id` (unique identifier for the student), `first_name`, `last_name`, `email`, `major`, `enrolled_courses` (an array of course IDs that the student is currently enrolled in).

```css
{
  "_id": ObjectId("6161b8bb835db764ab266e8d"),
  "first_name": "John",
  "last_name": "Smith",
  "email": "jsmith@illinois.edu",
  "major": "Computer Science",
  "enrolled_courses": [
    ObjectId("6161b8bb835db764ab266e8e"),
    ObjectId("6161b8bb835db764ab266e8f")
  ]
}

```
**instructors:** 
* Each document will represent an instructor and will have the following fields: `id` (unique identifier for the instructor), `first_name`, `last_name`, `email`, `department`, `teaching_courses` (an array of course IDs that the instructor is currently teaching).


```css
{
  "_id": ObjectId("6161b8bb835db764ab266e93"),
  "first_name": "Jane",
  "last_name": "Doe",
  "email": "jdoe@illinois.edu",
  "department": "Computer Science",
  "teaching_courses": [
    ObjectId("6161b8bb835db764ab266e8e"),
    ObjectId("6161b8bb835db764ab266e8f")
  ]
}

```
**courses:** 

* Each document will represent a course and will have the following fields: `id` (unique identifier for the course), `name`, `description`, `instructor_id` (the ID of the instructor who is teaching the course), `enrolled_students` (an array of student IDs who are currently enrolled in the course).

```css
{
  "_id": ObjectId("6161b8bb835db764ab266e8e"),
  "name": "Data Structures and Algorithms",
  "description": "Learn advanced data structures and algorithms with Java.",
  "instructor_id": ObjectId("6161b8bb835db764ab266e93"),
  "enrolled_students": [
    ObjectId("6161b8bb835db764ab266e8d"),
    ObjectId("6161b8bb835db764ab266e90"),
    ObjectId("6161b8bb835db764ab266e91")
  ]
}
```


### 1. Insert a new document into the `students` collection with the following information: `first_name` = "Emily", `last_name` = "Jones", `email` ="ejones@illinois.edu", `major` = "Mathematics", `enrolled_courses` = [ObjectId("6161b8bb835db764ab266e8e")].

```css
db.students.insertOne({
  "first_name": "Emily",
  "last_name": "Jones",
  "email": "ejones@illinois.edu",
  "major": "Mathematics",
  "enrolled_courses": [
    ObjectId("6161b8bb835db764ab266e8e")
  ]
})

```
1. Insert a new document into the `instructors` collection with the following information: `first_name` = "John", `last_name` = "Doe", `email` = "[jdoe@illinois.edu](mailto:jdoe@illinois.edu" target="_new)", `department` = "Computer Science", `teaching_courses` = [ObjectId("6161b8bb835db764ab266e8e"), ObjectId("6161b8bb835db764ab266e8f")].
```css
db.instructors.insertOne({
  "first_name": "John",
  "last_name": "Doe",
  "email": "jdoe@illinois.edu",
  "department": "Computer Science",
  "teaching_courses": [
    ObjectId("6161b8bb835db764ab266e8e"),
    ObjectId("6161b8bb835db764ab266e8f")
  ]
})

```
1. Insert a new document into the `courses` collection with the following information: `name` = "Database Systems", `description` = "Learn about relational database design and SQL.", `instructor_id` = ObjectId("6161b8bb835db764ab266e94"), `enrolled_students` = [ObjectId("6161b8bb835db764ab266e8d"), ObjectId("6161b8bb835db764ab266e90"), ObjectId("6161b8bb835db764ab266e91")].
```css
db.courses.insertOne({
  "name": "Database Systems",
  "description": "Learn about relational database design and SQL.",
  "instructor_id": ObjectId("6161b8bb835db764ab266e94"),
  "enrolled_students": [
    ObjectId("6161b8bb835db764ab266e8d"),
    ObjectId("6161b8bb835db764ab266e90"),
    ObjectId("6161b8bb835db764ab266e91")
  ]
})

```
1. Use the `find` method to retrieve all documents from the `students` collection.
```lua
db.students.find()

```
1. Use the `find` method to retrieve the document from the `instructors` collection with the email address "[jdoe@illinois.edu](mailto:jdoe@illinois.edu" target="_new)".
```lua
db.instructors.find({"email": "jdoe@illinois.edu"})

```
1. Use the `findOne` method to retrieve the first document from the `courses` collection.
```scss
db.courses.findOne()

```
1. Use the `updateOne` method to add the student `ObjectId("6161b8bb835db764ab266e92")` to the `enrolled_students` array of the course `ObjectId("6161b8bb835db764ab266e8f")`.
```json
db.courses.updateOne(
  {"_id": ObjectId("6161b8bb835db764ab

```


 --------
**You:**
can you show me step 7 to 12

 --------
**ChatGPT:**
Sure, here are the steps 7 to 12 of the assignment:
1. Use the `updateOne` method to add the student `ObjectId("6161b8bb835db764ab266e92")` to the `enrolled_students` array of the course `ObjectId("6161b8bb835db764ab266e8f")`.
```css
db.courses.updateOne(
  {"_id": ObjectId("6161b8bb835db764ab266e8f")},
  {"$addToSet": {"enrolled_students": ObjectId("6161b8bb835db764ab266e92")}}
)

```
1. Update the `instructors` collection to add the course `ObjectId("6161b8bb835db764ab266e90")` to the `teaching_courses` array of the instructor with the ID `ObjectId("6161b8bb835db764ab266e94")`.
```css
db.instructors.updateOne(
  {"_id": ObjectId("6161b8bb835db764ab266e94")},
  {"$addToSet": {"teaching_courses": ObjectId("6161b8bb835db764ab266e90")}}
)

```
1. Use an aggregation pipeline to find the number of students enrolled in each course. Return a list of documents with the fields `course_name` (the name of the course) and `enrollment_count` (the number of students enrolled in the course).
```bash
db.courses.aggregate([
  {"$lookup": {
    "from": "students",
    "localField": "enrolled_students",
    "foreignField": "_id",
    "as": "students"
  }},
  {"$project": {
    "_id": 0,
    "course_name": "$name",
    "enrollment_count": {"$size": "$students"}
  }}
])

```
1. Use an aggregation pipeline to find the average number of enrolled students per course. Round the result to two decimal places.
```kotlin
db.courses.aggregate([
  {"$lookup": {
    "from": "students",
    "localField": "enrolled_students",
    "foreignField": "_id",
    "as": "students"
  }},
  {"$project": {
    "_id": 0,
    "enrollment_count": {"$size": "$students"}
  }},
  {"$group": {
    "_id": null,
    "avg_enrollment": {"$avg": "$enrollment_count"}
  }},
  {"$project": {
    "_id": 0,
    "avg_enrollment": {"$round": ["$avg_enrollment", 2]}
  }}
])

```
1. Use an aggregation pipeline to find the instructor who is teaching the most courses. Return a document with the fields `instructor_name` (the name of the instructor) and `course_count` (the number of courses the instructor is teaching).
```bash
db.instructors.aggregate([
  {"$lookup": {
    "from": "courses",
    "localField": "teaching_courses",
    "foreignField": "_id",
    "as": "courses"
  }},
  {"$project": {
    "_id": 0,
    "instructor_name": {"$concat": ["$first_name", " ", "$last_name"]},
    "course_count": {"$size": "$courses"}
  }},
  {"$sort": {"course_count": -1}},
  {"$limit": 1}
])

```
1. Use an aggregation pipeline to find the most popular major among the enrolled students. Return a document with the fields `major_name` (the name of the major) and `enrollment_count` (the


 --------
**You:**
can you show me step 13 to 15

 --------
**ChatGPT:**
Sure, here are the steps 13 to 15 of the assignment:
1. Use the `$set` operator to add a new field called `start_date` to each document in the `courses` collection. Set the value of `start_date` to ISODate("2023-08-21T00:00:00Z") for all courses.
```bash
db.courses.updateMany(
  {},
  {"$set": {"start_date": ISODate("2023-08-21T00:00:00Z")}}
)

```
1. Use the `$unset` operator to remove the `enrolled_courses` field from the document in the `students` collection with the email address "[ejones@illinois.edu](mailto:ejones@illinois.edu" target="_new)".
```perl
db.students.updateOne(
  {"email": "ejones@illinois.edu"},
  {"$unset": {"enrolled_courses": ""}}
)

```
1. Use the `$lookup` operator to join the `courses` and `instructors` collections on the `instructor_id` field. Return a list of documents with the fields `course_name` (the name of the course) and `instructor_name` (the name of the instructor who is teaching the course).
```bash
db.courses.aggregate([
  {"$lookup": {
    "from": "instructors",
    "localField": "instructor_id",
    "foreignField": "_id",
    "as": "instructor"
  }},
  {"$project": {
    "_id": 0,
    "course_name": "$name",
    "instructor_name": {"$concat": ["$instructor.first_name", " ", "$instructor.last_name"]}
  }}
])

```
I hope this helps! Let me know if you have any questions or need further assistance.


 --------
