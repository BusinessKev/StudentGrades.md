
![FileStudentGrades](https://user-images.githubusercontent.com/79744165/109430419-b0851600-7a01-11eb-9353-f3adea01127b.jpg)
# StudentGrades.md
Database with Entities Student, Enrollment, Class
## Er Diagram on https://mermaid-js.github.io/mermaid-live-editor/#/
```Er
erDiagram
    
    Student ||--o{ Enrollment : has
    Enrollment o{ -- || Class: has
    
    Enrollment{
        int grade
    }

    Student {
        string name
        string email
        string phoneNumber
        boolean isReleased
    }

    Class {
       string name
       string hours 
    }
```
[![](https://mermaid.ink/img/eyJjb2RlIjoiZXJEaWFncmFtXG4gICAgXG4gICAgU3R1ZGVudCB8fC0tb3sgRW5yb2xsbWVudCA6IGhhc1xuICAgIEVucm9sbG1lbnQgb3sgLS0gfHwgQ2xhc3M6IGhhc1xuICAgIFxuICAgIEVucm9sbG1lbnR7XG4gICAgICAgIGludCBncmFkZVxuICAgIH1cblxuICAgIFN0dWRlbnQge1xuICAgICAgICBzdHJpbmcgbmFtZVxuICAgICAgICBzdHJpbmcgZW1haWxcbiAgICAgICAgc3RyaW5nIHBob25lTnVtYmVyXG4gICAgICAgIGJvb2xlYW4gaXNSZWxlYXNlZFxuICAgIH1cblxuICAgIENsYXNzIHtcbiAgICAgICBzdHJpbmcgbmFtZVxuICAgICAgIHN0cmluZyBob3VycyBcbiAgICB9XG5cbiAgIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)](https://mermaid-js.github.io/mermaid-live-editor/#/edit/eyJjb2RlIjoiZXJEaWFncmFtXG4gICAgXG4gICAgU3R1ZGVudCB8fC0tb3sgRW5yb2xsbWVudCA6IGhhc1xuICAgIEVucm9sbG1lbnQgb3sgLS0gfHwgQ2xhc3M6IGhhc1xuICAgIFxuICAgIEVucm9sbG1lbnR7XG4gICAgICAgIGludCBncmFkZVxuICAgIH1cblxuICAgIFN0dWRlbnQge1xuICAgICAgICBzdHJpbmcgbmFtZVxuICAgICAgICBzdHJpbmcgZW1haWxcbiAgICAgICAgc3RyaW5nIHBob25lTnVtYmVyXG4gICAgICAgIGJvb2xlYW4gaXNSZWxlYXNlZFxuICAgIH1cblxuICAgIENsYXNzIHtcbiAgICAgICBzdHJpbmcgbmFtZVxuICAgICAgIHN0cmluZyBob3VycyBcbiAgICB9XG5cbiAgIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)
  
# SQL code
## Create Tables
```SQL
create table students(
  student_id integer primary key, email text not null unique, 
  phone_number text not null unique, 
  is_released boolean
);

```
```SQL
CREATE TABLE enrollments(
    student_id INTEGER NOT NULL,
    class_id INTEGER NOT NULL,
    enrollment_grade INTEGER NOT NULL,
FOREIGN KEY(student_id) REFERENCES students(student_id),
FOREIGN KEY(class_id) REFERENCES classes(calss_id)
PRIMARY KEY (student_id,class_id)
);
```
```SQL
create table classes(
  class_id integer primary key, 
  class_name text not null unique, 
  class_hours text not null
);
```
## Insert Values
```SQL
insert into students(email,phone_number,is_released)
values
("kevin@mail.com","+1-202-555-0148 ",True),
("david@gmail.de","+1-202-555-0130",True),
("Tim@gmail.de","+1-202-555-0164",True),
("Pascal@mail.de","+1-202-555-0100",True),
("dielara@kanake.pop","+1-202-555-0154",False);
```
```SQL
insert into enrollments(student_id,class_id,enrollment_grade) 
values
(1,2,1),
(2,3,3),
(3,2,6),
(4,1,4),
(5,5,2);
```
```SQL
insert into classes(class_name,class_hours)
values
("Finance","7"),
("Accounting","5"),
("Sport","4"),
("Politics","15"),
("Acting","2");
```
## query
```SQL
select 
  student_id, email, enrollment_grade, class_name 
from enrollments 
  join classes using (class_id) 
  join students using(student_id)
  order by student_id not null;
```
```
student_id    email              enrollment_grade       class_name
2	        david@gmail.de	        1	                Finance
2       	david@gmail.de	        6	                Accounting
3       	Tim@gmail.de	        3	                Sport
4	        Jeremy-Pascal@mail.de	3	                Politics
5	        dielara@kanake.pop      2	                Acting
```
