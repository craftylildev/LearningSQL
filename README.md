--1

SELECT 

 FirstName, 

 LastName, 

 CustomerID, 

 Country 

FROM Customer 

WHERE Country != 'USA';

--2
SELECT * 
FROM Customer 
WHERE Country = 'Brazil';

--3
SELECT 
  c.FirstName || " " || c.LastName,
  i.InvoiceId, 
  i.InvoiceDate, 
  i.BillingCountry
FROM Customer as c 
INNER JOIN Invoice i on i.CustomerId = c.CustomerId
WHERE i.BillingCountry = 'Brazil';

--4
SELECT
  e.*
FROM Employee as e
WHERE e.Title = 'Sales Support Agent';

--5
SELECT * 
FROM Invoice
WHERE BillingCountry = 'Belgium' 
OR BillingCountry = 'Canada'
OR BillingCountry = 'Ireland';

--6
