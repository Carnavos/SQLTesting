# SQLTesting

SELECT
cus.CustomerID,
cus.FirstName || ' ' || cus.LastName AS FullName,
cus.Country
FROM Customer as cus
WHERE
Country <> "USA";

SELECT
cus.CustomerID,
cus.FirstName || ' ' || cus.LastName AS FullName,
cus.Country
FROM Customer as cus
WHERE
Country == "Brazil";

SELECT
cus.FirstName || ' ' || cus.LastName as FullName,
inv.InvoiceId,
inv.InvoiceDate,
inv.BillingCountry
FROM Customer as cus
INNER JOIN Invoice as inv ON cus.CustomerId = inv.CustomerId
WHERE
Country == "Brazil";

SELECT
emp.EmployeeId,
emp.FirstName || ' ' || emp.LastName as FullName,
emp.Title
FROM
Employee as emp
WHERE
Title == "Sales Support Agent";

SELECT DISTINCT
inv.BillingCountry
FROM Invoice as inv;

SELECT
emp.FirstName || ' ' || emp.LastName as AssociatedRepName,
inv.InvoiceId,
inv.Total
FROM Customer as cust
INNER JOIN Employee as emp ON cust.SupportRepId = emp.EmployeeId
INNER JOIN Invoice as inv ON cust.CustomerId = inv.CustomerId
WHERE
Title == "Sales Support Agent";

SELECT 
COUNT(InvoiceId) as InvoiceNumber,
SUM(Total)
FROM Invoice
WHERE InvoiceDate BETWEEN  '2009-01-00 00:00:00' AND '2009-12-31 24:00:00';
Answer: 83 and $449.46 


SELECT 
COUNT(InvoiceId) as InvoiceNumber,
SUM(Total)
FROM Invoice
WHERE InvoiceDate BETWEEN  '2011-01-00 00:00:00' AND '2011-12-31 24:00:00';
Answer: 83 and $469.58

SELECT COUNT(InvoiceId) 
FROM InvoiceLine
WHERE InvoiceId = '37';
Answer: 4

SELECT
invl.InvoiceId,
Count(InvoiceId) as LineItemCount
FROM InvoiceLine as invl
GROUP BY InvoiceId;

SELECT
inv.InvoiceId,
inv.InvoiceLineId,
tr.Name
FROM InvoiceLine as inv
INNER JOIN Track as tr ON inv.TrackId = tr.TrackId;

SELECT
invl.InvoiceId,
tr.Name as TrackName,
ar.Name as ArtistName
FROM 
Track as tr
INNER JOIN Album ON tr.AlbumId = Album.AlbumId
INNER JOIN Artist as ar ON Album.ArtistId = ar.ArtistId
INNER JOIN InvoiceLine as invl ON tr.TrackId = invl.TrackId;

SELECT
DISTINCT inv.BillingCountry, 
Count(inv.InvoiceId)
FROM Invoice as inv
GROUP BY inv.BillingCountry

SELECT
Playlist.Name as PlaylistName,
Count(Track.TrackId) as TrackAmount
FROM PlaylistTrack
INNER JOIN Playlist ON PlaylistTrack.PlaylistId = Playlist.PlaylistId
INNER JOIN Track ON PlaylistTrack.TrackId = Track.TrackId
GROUP BY Playlist.Name;

SELECT
Track.Name as TrackName,
Album.Title as AlbumTitle,
MediaType.Name as MediaType,
Genre.Name as Genre
FROM Track
INNER JOIN Album ON Track.AlbumId = Album.AlbumId
INNER JOIN  MediaType ON Track.MediaTypeId = MediaType.MediaTypeId
INNER JOIN Genre ON Track.GenreId = Genre.GenreId

SELECT
Count(InvoiceLine.InvoiceLineId) as NumOfLineItems,
*
FROM Invoice
INNER JOIN InvoiceLine ON Invoice.InvoiceId = InvoiceLine.InvoiceLineId
GROUP BY InvoiceLine.InvoiceId

SELECT
Employee.FirstName || ' ' || Employee.LastName as RepName,
Count(Invoice.InvoiceId) as TotalSales
FROM Customer
INNER JOIN Invoice ON Customer.CustomerId = Invoice.CustomerId
INNER JOIN Employee ON Customer.SupportRepId = Employee.EmployeeId
GROUP BY Employee.LastName

SELECT
Employee.FirstName || ' ' || Employee.LastName as RepName,
Count(Invoice.InvoiceId) as Sales
FROM Customer
INNER JOIN Invoice ON Customer.CustomerId = Invoice.CustomerId
INNER JOIN Employee ON Customer.SupportRepId = Employee.EmployeeId
WHERE 
InvoiceDate BETWEEN  '2009-01-00 00:00:00' AND '2009-12-31 24:00:00'
GROUP BY Employee.LastName
ORDER BY Count(Invoice.InvoiceId) DESC LIMIT 1

SELECT
Employee.FirstName || ' ' || Employee.LastName as RepName,
Count(Invoice.InvoiceId) as Sales
FROM Customer
INNER JOIN Invoice ON Customer.CustomerId = Invoice.CustomerId
INNER JOIN Employee ON Customer.SupportRepId = Employee.EmployeeId
GROUP BY Employee.LastName
ORDER BY Count(Invoice.InvoiceId) DESC LIMIT 1

SELECT
Employee.FirstName || ' ' || Employee.LastName as RepName,
Count(Customer.CustomerId) as CustomerCount
FROM Customer
INNER JOIN Employee ON Customer.SupportRepId = Employee.EmployeeId
GROUP BY Employee.LastName

SELECT
Customer.Country,
Count(Invoice.InvoiceId) as TotalSales
FROM Customer
INNER JOIN Invoice ON Customer.Country = Invoice.BillingCountry
GROUP BY Customer.Country

SELECT
InvoiceLine.TrackId,
Count(InvoiceLine.TrackId)
FROM InvoiceLine
INNER JOIN Invoice ON InvoiceLine.InvoiceId = Invoice.InvoiceId
WHERE Invoice.InvoiceDate BETWEEN  '2013-01-00 00:00:00' AND '2013-12-31 24:00:00'
GROUP BY InvoiceLine.TrackId
ORDER BY Count(InvoiceLine.TrackId)
DESC

SELECT
InvoiceLine.TrackId,
Count(InvoiceLine.TrackId),
Invoice.InvoiceDate
FROM InvoiceLine
INNER JOIN Invoice ON InvoiceLine.InvoiceId = Invoice.InvoiceId
GROUP BY InvoiceLine.TrackId
ORDER BY Count(InvoiceLine.TrackId)
DESC LIMIT 5

SELECT
Artist.Name as ArtistName,
SUM(InvoiceLine.UnitPrice) as SalesDollarSum
FROM InvoiceLine
INNER JOIN Track ON InvoiceLine.TrackId = Track.TrackId
INNER JOIN Album ON Track.AlbumId = Album.AlbumId
INNER JOIN Artist ON Album.ArtistId = Artist.ArtistId
INNER JOIN Invoice ON InvoiceLine.InvoiceId = Invoice.InvoiceId
GROUP BY Artist.Name
ORDER BY SUM(InvoiceLine.UnitPrice) DESC LIMIT 3

SELECT
MediaType.Name as MostPurchasedMT,
Count(InvoiceLine.InvoiceLineId) as Purchases
FROM InvoiceLine
INNER JOIN Track ON InvoiceLine.TrackId = Track.TrackId
INNER JOIN MediaType ON Track.MediaTypeId = MediaType.MediaTypeId
GROUP BY MediaType.Name
ORDER BY Count(InvoiceLine.InvoiceLineId) DESC LIMIT 1
