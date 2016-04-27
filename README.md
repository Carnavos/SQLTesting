# SQLTesting

SELECT
cus.CustomerID,
cus.FirstName || ' ' || cus.LastName AS FullName,
cus.Country
FROM Customer as cus
WHERE
Country <> "USA"

SELECT
cus.CustomerID,
cus.FirstName || ' ' || cus.LastName AS FullName,
cus.Country
FROM Customer as cus
WHERE
Country == "Brazil"

SELECT
cus.FirstName || ' ' || cus.LastName as FullName,
inv.InvoiceId,
inv.InvoiceDate,
inv.BillingCountry
FROM Customer as cus
INNER JOIN Invoice as inv ON cus.CustomerId = inv.CustomerId
WHERE
Country == "Brazil";

