### Original Form:

| assignment_id | student_id | due_date | professor | assignment_topic                | classroom | grade | relevant_reading    | professor_email   |
| :------------ | :--------- | :------- | :-------- | :------------------------------ | :-------- | :---- | :------------------ | :---------------- |
| 1             | 1          | 23.02.21 | Melvin    | Data normalization              | WWH 101   | 80    | Deumlich Chapter 3  | l.melvin@foo.edu  |
| 2             | 7          | 18.11.21 | Logston   | Single table queries            | 60FA 314  | 25    | Dümmlers Chapter 11 | e.logston@foo.edu |
| 1             | 4          | 23.02.21 | Melvin    | Data normalization              | WWH 101   | 75    | Deumlich Chapter 3  | l.melvin@foo.edu  |
| 5             | 2          | 05.05.21 | Logston   | Python and pandas               | 60FA 314  | 92    | Dümmlers Chapter 14 | e.logston@foo.edu |
| 4             | 2          | 04.07.21 | Nevarez   | Spreadsheet aggregate functions | WWH 201   | 65    | Zehnder Page 87     | i.nevarez@foo.edu |
| ...           | ...        | ...      | ...       | ...                             | ...       | ...   | ...                 | ...               |




### Why Not Compliant with 4NF

The original data set is not compliant with 4NF because it contains **multi-valued dependencies** and **does not represent a normalized structure**. For example, the assignment_topic and relevant_reading columns represent **multi-valued dependencies** as a professor may assign multiple readings for a single assignment topic. Also, the professor and classroom columns are functionally dependent on the **combination of course section**(identified by assignment_id) and due_date, as different sections of the same course may have different professors and classrooms.


### 1 Courses

| course_id | course_name |
| :-------- | :---------- |
| 1         | Intro to CS   |
| 2         | Database |
| 3         | Web Development |
| ...       | ...         |

Primary Key: `course_id`

### 2 Professors

| professor_id | professor_name | professor_email    |
| :----------- | :------------- | :----------------- |
| 1            | Melvin         | l.melvin@foo.edu   |
| 2            | Logston        | e.logston@foo.edu  |
| 3            | Nevarez        | i.nevarez@foo.edu  |
| ...          | ...            | ...                |

Primary Key: `professor_id`


### 3 Sections

| section_id | course_id | professor_id | classroom |
| :--------- | :-------- | :----------- | :-------- |
| 1          | 1         | 1            | WWH 101   | 
| 2          | 2         | 2            | 60FA 314  |
| 3          | 3         | 3            | WWH 201   |
| ...        | ...       | ...          | ...       |

Primary Key: `section_id`

Foreign Keys: `course_id`, `professor_id`


### 4 Assignments

| assignment_id | section_id | assignment_topic      | due_date | 
| :------------ | :--------- | :-------------------- | :------- |
| 1             | 1          | Data normalization    | 23.02.21 |
| 2             | 2          | Single table queries  | 18.11.21 |
| 4             | 3          | Spreadsheet aggregate functions | 04.07.21 |
| ...           | ...       | ...        | ...                   | ...      |

Primary Key: `assignment_id`

Foreign Key: `section_id`

### 5 Grades

| student_id | assignment_id | grade |
| :--------- | :------------ | :---- |
| 1          | 1             | 80    |
| 7          | 2             | 25    |
| 4          | 1             | 75    |
| ...        | ...           | ...   |

Primary Keys:`student_id` 

Foreign Keys: `student_id`, `assignment_id`


### 6 Readings


| reading_id    | section_id | assignment_topic                | due_date  | relevant_reading   |
|---------------|------------|---------------------------------|-----------|--------------------|
| 1             | 1          | Data normalization              | 23.02.21  | Deumlich Chapter 3 |
| 2             | 2          | Single table queries            | 18.11.21  | Dümmlers Chapter 11|
| 1             | 3          | Data normalization              | 23.02.21  | Deumlich Chapter 3 |
| ...           | ...        | ...                             | ...       | ...                |

Primary Key: `reading_id`

Foreign Keys: `reading_id`,  `section_id`



### Changes Made for 4NF Compliance

**Split** the original table into separate tables representing distinct entities such as courses, professors, sections, assignments, grades, and readings.

**Introduced** surrogate keys (e.g., course_id, professor_id, section_id) to uniquely identify each entity.

Ensured each table represents a **single theme or entity type**, eliminating multi-valued dependencies.

**Created foreign key relationships** between related tables (e.g., section_id in Assignments table referencing section_id in Sections table).

Ensured each table has a **primary key** to uniquely identify rows.


### The ER Diagram

![Example Image](/images/er.drawio.svg)