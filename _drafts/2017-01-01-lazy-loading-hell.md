---
layout: post
title: Lazy Loading Hell
---

During my work on
The syllabus took 10+ seconds to load.

[//]: <> (What is a Syllabus?)
[//]: <> ("An outline of the subjects in a course of study or teaching.")

A syllabus is an outline of a course and usually includes information about the teacher, course objectives, assignments and calendar for the couse.
It basically was suppose to be able to access and summarize every bit of data the CMS contained.

We had a simple ORM model.
Objects mapped directly to the DB.

Our dev environment was php based with a sql DB elsewhere.
We were setup with Fiddler to be able to see

600+ calls to the database.

To understand why I have to go back to our ORM.
Here is a short snippet of what it looked like.

```php
<?php
$course = new Course($courseID);
$assignments = $course->getAssignments();
$firstAssignment = $assignments[0];
$title = $firstAssignment->getTitle();
```

We would have an ID to the course, create an object to assign that row in the DB and then get the assignments.
However everything was lazy loaded and here is basically what each ORM object did on init.

```php
<?php
class Course
{
    public $id;
    private $isLoaded;
    public $assignments;

    public function __construct($id)
    {
      $this->id = $id;
    }

    public function getAssignments()
    {
      if ($this->isLoaded) {
        return $this->assignments
      } else {
        $this->syncLoad();
        return $this->assignments;
      }
    }
```

So you only get data for an object when you request that data.
But I said everything is lazy loaded... all the way down.

When you request the array of assignments you get an array of unloaded assignment objects.
You only really got the IDs of the assignments.

A course can have a lot of lists of data like assignments, quizzes, calendar items, people, learning objectives and etc.
Sometime this data has it's own set of subdata.
[//]: <> (Think of subobject data)

The syllabus effectivly need to load everything in order to get a summary of it.
In large course it would be several hundred DB calls.
Till this point lazy loading in this manner was not really an issue.

I forget the exact solution but

All our objects had been setup so that
