
# SQL - Assignment-1

- Department
- Professor
- Student

```sql

CREATE DATABASE universitydb;

USE universitydb;

CREATE TABLE department(
dept_id int not null auto_increment primary key,
dept_name text not null
);

CREATE TABLE professor(
prof_id int not null auto_increment primary key,
prof_name text not null,
dept_id int not null, 
foreign key(dept_id) references department(dept_id)
);

CREATE TABLE student(
student_id int not null auto_increment primary key,
name text not null,
age int not null,
dept_id int not null,
advisor_id int not null,
foreign key(dept_id) references department(dept_id),
foreign key(advisor_id) references professor(prof_id)
);


```