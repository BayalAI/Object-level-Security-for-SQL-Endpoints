In this case let's say you have data in tables of various patients. Now a doctor can only see all data of patients related to medical history and all but cannot see billing data or card information. The finance department of that hospital can see billing data and finance related data, but not the actual medical reports. Thus, segregation has to be on column level.

They cannot see workspace, they cannot see all tables, they also cannot see all columns, only columns pertaining to their area.

A hospital maintains a comprehensive medical database that includes patient records, treatment histories, billing information, and research data. The database needs to ensure that only authorized personnel can access specific data, protecting patient privacy and complying with regulations like HIPAA.

 Create the Role:


```
CREATE ROLE DoctorGroup;
CREATE ROLE NurseGroup;
```


Grant Permissions to the Role:
SQL


```
GRANT SELECT ON patientrecords (PatientName, TreatmentDate) TO NurseGroup;
GRANT SELECT ON patientrecords (PatientName, SSN, Diagnosis, TreatmentDate) TO DoctorGroup;
```

Classic example of Column level security where for doctors, all columns of data are visible, since you assigned all columns permission to DoctorGroup. But for nurses, they can only see specific columns since you gave specific access to NurseGroup