# StudentGrades.md
Database with Entities Student, Enrollment, Class
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

  
