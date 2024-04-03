# GroupProjectMIST4610-Group1

## Team Members: 
Gwen Wentworth

Caroline Cooper

[Hubah Akhtar]( https://github.com/hubahakhtar/Project1 )

[Kishen Patel]( https://github.com/supersomeone03/Project-1)

Charlie Kim 

###Problem description:
Pretend you are the owner/operator of an emergency healthcare clinic needing to build a relational database. You hired some students from the MIST 4610 class at the University of Georgia 
to create the database for you. They need to know more about your organization to identify which entities, attributes, and relationships are important for you. Start by describing your business as a real client 

###Data Model: 

Our model is based on a hypothetical hospital,the patient entity is representative of the patient. We can store many attributes, their contact info, date of birth, etc. The patient is linked to their emergency contacts, which they can have many of. Each patient is assigned one room which can have multiple types of equipment. Patients also are linked to their invoices, which they can have many of. Patients can also leave reviews about the hospital, this entity stores their comments and the rating given from 1-5. Patients can also arrive at their appointment via hospital transportation, such as an ambulance or helicopter. This is noted in the transportation entity. 

Their appointment, which stores that date and appointment type, is linked to the staff table, where one staff member can be assigned many appointments but only one staff member is assigned to an appointment. The staff entity is connected to the payroll entity, which stores information on the employee's pay rate, amount, hours worked, and the date the check was issued. 

![datamodel](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/6d61a203-e7eb-44c1-b69d-e79b9ccb71cb)

###Data Dictonary: 
![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/15c67da6-6599-47a2-8355-4afbd062d3ea)
![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/4d762486-5ede-4fe6-9e88-9a26828b9d76)
![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/fee98406-80a5-4ec7-bbd9-b5430d5340cc)
![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/b972e404-21f1-4767-9573-f8bcbe950986)
![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/03b6b069-234e-4803-a1df-62b3094b0299)
![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/13131b4d-a442-46a7-88fb-74430e4ec39d)
![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/b382de7f-9a7b-4614-91b8-fb4a8b81fa85)
![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/4faced4e-b4e5-4e7e-86ff-624f4f99a577)
![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/c46a6bd3-81e6-44ba-8a9e-e3ff0875b168)
![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/e7e61daf-7935-4fd3-af2e-03f1befffbc8)
![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/bf7be95c-6f76-4925-8af8-b38645060699)
![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/97904006-042a-4ca2-8c07-1e39e5b536d0)

### Simple Queries 

1 Select the name and DOB for all patients born in 1999 

SELECT patient_Name, `date of birth`  

FROM patient 

WHERE `date of birth` regexp "1999"; 

 ![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/a30bf304-ce27-4060-a2e8-479d8457d876)

2 Show the name of patient and show their invoice number and amount due 


SELECT patient_Name, Invoice_InvoiceNum, Charge 

FROM patient 

JOIN patient_has_Invoice ON patient_has_Invoice.patient_patientID = patient.patientID; 

![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/a4033758-5b2e-4ca0-9159-c7e4d00fb04b)
 
3 Display all existing appointments along with the date and name of patient 

SELECT patient_Name, appointmentID, Date 

FROM patient 

JOIN Appointment ON Appointment.patient_patientID= patient.patientID; 

 ![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/ef536e62-f940-4426-adbf-dbf91f2c95c7)

4 Display all appointments for a particular staff member 

SELECT staffID, staffName, staff_schedule,appointmentID, Date 
FROM Staff 
JOIN Appointment ON Appointment.Staff_staffID = Staff.staffID 

WHERE staffID = "1552"; 

![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/c7d6b85c-0274-420a-a4b7-6154daf814bf)

###6 Complex Queries: 

1 Display the patient name, DOB, and their review number and review description 

SELECT p.`date of birth`,p.patient_Name, r.reviewNum, r.Desc 

FROM patient p 

JOIN Review r ON p.patientID = r.patient_patientID; 

 ![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/fc50f224-b85e-40c2-9b25-7ae5d94ff579)

#2 Find all appointments scheduled for 2027-10-21 along with the patient's name and the staff assigned to each appointment. 

SELECT a.appointmentID, a.Date, p.patient_Name, s.staffName 

FROM Appointment a 

JOIN patient p ON a.patient_patientID = p.patientID 

JOIN Staff s ON a.Staff_staffID = s.staffID 

WHERE DATE(a.Date) ='2027-10-21'; 

![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/1ea334c9-3241-4106-8c8b-55614b81df16)

#3 Evaluate staff performance based on the number of appointments attended and the corresponding average patient reviews. 

SELECT s.staffID, s.staffName,   

COUNT(a.appointmentID) AS num_appointments_attended,  

AVG(r.Rating) AS average_review_rating 

FROM Staff s 

JOIN Appointment a ON s.staffID = a.Staff_staffID 

JOIN Procedures pr ON a.appointmentID = pr.Appointment_appointmentID 

JOIN patient p ON p.patientID = a.patient_patientID 

JOIN Review r ON r.patient_patientID = p.patientID 

GROUP BY s.StaffID, s.StaffName; 
 
![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/d6732138-83be-4fe5-884b-d13f5b938255)

#4 Retrieve all appointments scheduled for Cesaro Troake along with their emergency contact details.  

SELECT a.appointmentID, a.Date, e.EC_Phone, e.EC_Address, p.patient_Name 

FROM Appointment a 

JOIN patient p ON a.patient_patientID = p.patientID 

JOIN Emergency_Contact e ON p.patientID = e.patient_patientID 

WHERE p.patient_Name = 'Cesaro Troake’; 

![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/fc638be6-d467-4e33-827f-1f8733387399)

#5 Determine the average number of appointments per staff member over a given period, and display those exceeding the average in descending order 

SELECT Staff.staffID, Staff.staffName, COUNT(Appointment.appointmentID) AS NumberOfAppointments 

FROM Staff 

JOIN Appointment ON Staff.staffID = Appointment.Staff_staffID 

WHERE Appointment.Date BETWEEN '2025-08-25' AND '2027-11-03' 

GROUP BY Staff.staffID, Staff.staffName 

HAVING COUNT(Appointment.appointmentID) > (SELECT (AVG(AppointmentCounts.NumberOfAppointments) - 0.1) -- Slight adjustment for precision FROM ( 
SELECT COUNT(Appointment.appointmentID) AS NumberOfAppointments 
FROM Appointment 
 WHERE Appointment.Date BETWEEN '2025-08-25' AND '2027-11-03' 
GROUP BY Appointment.Staff_staffID 
) AS AppointmentCounts  ) 

ORDER BY NumberOfAppointments DESC; 
 
![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/c4e4e684-f062-4270-b7c8-56bbf45ff12a)

#6 Identify patients with the largest balance due on their invoices with a balance exceeding $10,000. Order the balances due in descending order and display the total average balance due. 


SELECT patient.patientID, patient.patient_Name, Invoice.InvoiceNum, SUM(Invoice.Balence_Due) AS TotalBalanceDue, 
(SELECT AVG(Balence_Due) FROM Invoice) AS TotalAverageBalanceDue 
FROM patient 

JOIN patient_has_Invoice ON patient.patientID = patient_has_Invoice.patient_patientID 

JOIN Invoice ON patient_has_Invoice.Invoice_InvoiceNum = Invoice.InvoiceNum 

GROUP BY patient.patientID, patient.patient_Name, Invoice.InvoiceNum 

HAVING SUM(Invoice.Balence_Due) > 10000 

ORDER BY TotalBalanceDue DESC; 

![image](https://github.com/gaw63800/GroupProjectMIST4610-Group1/assets/150155143/6237059d-e165-4e0f-a1aa-d58288e70a7e)





