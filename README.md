**1.** Provide a query showing Customers (just their full names, customer ID and country) who are not in the US.
```
SELECT 
 FirstName, 
 LastName, 
 CustomerID, 
 Country 
FROM Customer 
WHERE Country != 'USA'
```

**2.** Provide a query only showing the Customers from Brazil.
```
SELECT * 
FROM Customer 
WHERE Country = 'Brazil'
```

**3.** Provide a query showing the Invoices of customers who are from Brazil. The resultant table should show the customer's full name, Invoice ID, Date of the invoice and billing country.
```
SELECT 
  c.FirstName || " " || c.LastName,
  i.InvoiceId, 
  i.InvoiceDate, 
  i.BillingCountry
FROM Customer as c 
INNER JOIN Invoice i on i.CustomerId = c.CustomerId
WHERE i.BillingCountry = 'Brazil'
```

**4.** Provide a query showing only the Employees who are Sales Agents.
```
SELECT
  e.*
FROM Employee as e
WHERE e.Title = 'Sales Support Agent'
```

**5.** Provide a query showing a unique list of billing countries from the Invoice table.
```
SELECT * 
FROM Invoice
WHERE BillingCountry = 'Belgium' 
OR BillingCountry = 'Canada'
OR BillingCountry = 'Ireland'
```

**6.** Provide a query that shows the invoices associated with each sales agent. The resultant table should include the Sales Agent's full name.
```
SELECT
  e.FirstName || " " || e.LastName,
  i.InvoiceId
FROM Employee as e
INNER JOIN Customer c on e.EmployeeId = c.SupportRepId
INNER JOIN Invoice i on c.CustomerId = i.CustomerId
```

**7.** Provide a query that shows the Invoice Total, Customer name, Country and Sale Agent name for all invoices and customers.
```
SELECT
  i.Total,
  c.FirstName || " " || c.LastName,
  c.Country,
  e.FirstName || " " || e.LastName
FROM Invoice as i
INNER JOIN Customer c on i.CustomerId = c.CustomerId
INNER JOIN Employee e on e.EmployeeId = c.SupportRepId
```

**8.** How many Invoices were there in 2009 and 2011? What are the respective total sales for each of those years?(include both the answers and the queries used to find the answers)
```
SELECT
  SUM(Total),  
  strftime('%Y', InvoiceDate) as InvoiceYear,
  COUNT(Total)
FROM Invoice 
WHERE strftime('%Y', InvoiceDate)
IN ('2009')
UNION
SELECT
  SUM(Total),  
  strftime('%Y', InvoiceDate) as InvoiceYear,
  COUNT(Total)
FROM Invoice 
WHERE strftime('%Y', InvoiceDate)
IN ('2011')

```
```
Answers:
YEAR - COUNT - TOTAL
2009 - 83    - 449.4600000000003
2011 - 83    - 469.5800000000003
```

**9.** Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for Invoice ID 37.
```
SELECT
COUNT(InvoiceLineId)
FROM InvoiceLine
WHERE InvoiceId = 37
```

**10.** Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for each Invoice. HINT: GROUP BY
```
SELECT
COUNT(InvoiceLineId)
FROM InvoiceLine
GROUP BY (InvoiceId)
```

**11.** Provide a query that includes the track name with each invoice line item.
```
SELECT
  il.InvoiceLineId,
  t.Name as TrackName
FROM InvoiceLine as il
INNER JOIN Track t on il.TrackId = t.TrackId
```

**12.** Provide a query that includes the purchased track name AND artist name with each invoice line item.
```
SELECT 
  il.InvoiceLineId, 
  t.Name, 
  ar.Name 
FROM InvoiceLine il 
INNER JOIN Track t on t.TrackId = il.TrackId 
INNER JOIN Album al on al.AlbumId = t.AlbumId 
INNER JOIN Artist ar on ar.ArtistId = al.ArtistId
```

**13.** Provide a query that shows the # of invoices per country. HINT: GROUP BY
```
SELECT
  BillingCountry,
  COUNT(InvoiceId)
FROM Invoice
GROUP BY BillingCountry
```

**14.** Provide a query that shows the total number of tracks in each playlist. The Playlist name should be include on the resulant table.
```
SELECT
  p.Name as PlaylistName,
  COUNT(pt.TrackId) as NumberOfTracks
FROM Playlist p
INNER JOIN PlaylistTrack pt on pt.PlaylistId = p.PlaylistId
INNER JOIN Track t on t.TrackId  = pt.TrackId
GROUP BY PlaylistName
```

**15.** Provide a query that shows all the Tracks, but displays no IDs. The resultant table should include the Album name, Media type and Genre.

```
SELECT
  t.Name as TrackName,
  al.Title as AlbumName,
  mt.Name as MediaType,
  g.Name as Genre
FROM Track t
INNER JOIN Album al on al.AlbumId = t.AlbumId
INNER JOIN Genre g on g.GenreId  = t.GenreId
INNER JOIN MediaType mt on mt.MediaTypeId = t.MediaTypeId
```

**16.** Provide a query that shows all Invoices but includes the # of invoice line items.


**17.** Provide a query that shows total sales made by each sales agent.


**18.** Which sales agent made the most in sales in 2009? HINT: MAX


**19.** Which sales agent made the most in sales over all?


**20.** Provide a query that shows the # of customers assigned to each sales agent.


**21.** Provide a query that shows the total sales per country. Which country's customers spent the most?


**22.** Provide a query that shows the most purchased track of 2013.


**23.** Provide a query that shows the top 5 most purchased tracks over all.


**24.** Provide a query that shows the top 3 best selling artists.


**25.** Provide a query that shows the most purchased Media Type.
