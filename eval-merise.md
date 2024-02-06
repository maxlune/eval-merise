## MLD

Student (id, email, password)  
Teacher (id, email, password)  
Course (id, course_name)  
Session (id, session_name, student_id, teacher_id, course_id, photolist_id schedule_id, DateTime)  
Assessement (id, assessement_type_id, session_id, score)  
AssessementType (id, assessement_type_name)  
Schedule (id, start_date, end_date)  
PhotoList (id, name, path)  


## Script SQL

```sql
CREATE TABLE Student (
    id INT PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL
);

CREATE TABLE Teacher (
    id INT PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL
);

CREATE TABLE Course (
    id INT PRIMARY KEY,
    course_name VARCHAR(255)
);

CREATE TABLE Schedule (
    id INT PRIMARY KEY,
    start_date DATE NOT NULL,
    end_date DATE NOT NULL
);

CREATE TABLE PhotoList (
    id INT PRIMARY KEY,
    name VARCHAR(255),
    path VARCHAR(255)
);

CREATE TABLE AssessementType (
    id INT PRIMARY KEY,
    assessement_type_name VARCHAR(255)
);

CREATE TABLE Session (
    id INT PRIMARY KEY,
    session_name VARCHAR(255),
    student_id INT,
    teacher_id INT,
    course_id INT,
    schedule_id INT,
    photo_list_id INT,
    DateTime DATETIME,
    FOREIGN KEY (student_id) REFERENCES Student(id),
    FOREIGN KEY (teacher_id) REFERENCES Teacher(id),
    FOREIGN KEY (course_id) REFERENCES Course(id),
    FOREIGN KEY (schedule_id) REFERENCES Schedule(id),
    FOREIGN KEY (photo_list_id) REFERENCES PhotoList(id)
);

CREATE TABLE Assessement (
    id INT PRIMARY KEY,
    assessement_type_id INT NOT NULL,
    session_id INT NOT NULL,
    score DECIMAL(5,2),
    FOREIGN KEY (assessement_type_id) REFERENCES AssessementType(id),
    FOREIGN KEY (session_id) REFERENCES Session(id)
);

CREATE TABLE Session_PhotoList (
    session_id INT,
    photo_list_id INT,
    FOREIGN KEY (session_id) REFERENCES Session(id),
    FOREIGN KEY (photo_list_id) REFERENCES PhotoList(id)
);
```