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


