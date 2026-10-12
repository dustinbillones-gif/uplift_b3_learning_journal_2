# uplift_b3_learning_journal_2
This document summarizes my key learnings, SQL queries, challenges, real-world applications, self-assessment, and next steps as I continue learning SQL.

---

## 1. What I Learned

I learned a lot from the previous meetings on SQL, especially filtering and differentiating queries.

The way I understand basic queries is through this simple example:

```sql
SELECT *
FROM customers c
LIMIT 5;
```

- **`SELECT`** refers to the columns that I want to see. In this case, the asterisk (`*`) returns all columns in the table.
- **`FROM`** refers to the table where the columns will be extracted from.
- **`LIMIT 5`** refers to the number of rows I want to display. This is similar to the `.head()` function in Pandas.

Another important concept I learned is the difference between `WHERE` and `HAVING`. The former is used to filter non-aggregated data, while the latter is used for aggregated data.

The way I understand non-aggregated versus aggregated data is that aggregated data can involve creating a new column using a function or a combination of functions and operations. This allows us to gather more information from an existing table.

For example, we can calculate a new `Profit` column from existing `Revenue` and `Cost` columns by subtracting the cost from the revenue.

---

## 2. A Query I Am Proud Of

The query I am most proud of is the one I wrote for **Question 3, Part B**. This was particularly challenging for me because of the number of requirements.

### Step 1: Checking Table Metadata

Before writing my main query, I checked the columns available in the tables I needed to use.

**Customers table**

```sql
SELECT *
FROM customers c
LIMIT 5;
```

Allows me to review the columns contained in the `customers` table.

**Tracks table**

```sql
SELECT *
FROM tracks t
LIMIT 5;
```

Allows me to review the columns contained in the `tracks` table.

**Invoices table**

```sql
SELECT *
FROM invoices i
LIMIT 5;
```

Allows me to review the columns contained in the `invoices` table.

**Invoice Items table**

```sql
SELECT *
FROM invoice_items ii
LIMIT 5;
```

Allows me to review the columns contained in the `invoice_items` table.

### Step 2: Writing the Main Query

```sql
SELECT
    c.CustomerId,
    c.FirstName,
    c.LastName,
    t.Name AS TrackName,
    ii.Quantity,
    ii.UnitPrice
FROM customers c
LEFT JOIN invoices i
    ON c.CustomerId = i.CustomerId
LEFT JOIN invoice_items ii
    ON i.InvoiceId = ii.InvoiceId
LEFT JOIN tracks t
    ON t.TrackId = ii.TrackId
WHERE c.CustomerId = 5
ORDER BY ii.InvoiceLineId;
```

### Step 3: Understanding the Query

| SQL Clause | Purpose |
|---|---|
| `SELECT` | Displays the columns I need to present. |
| `FROM customers c` | Identifies the `customers` table as the starting table and assigns it the alias `c`. |
| `LEFT JOIN invoices i` | Joins the invoices table with the customers table through their common column, `CustomerId`. |
| `LEFT JOIN invoice_items ii` | Joins the invoice_items table with the invoices table through their common column, `InvoiceId`. |
| `LEFT JOIN tracks t` | Joins the tracks table with the invoice_items table through their common column, `TrackId`. |
| `WHERE c.CustomerId = 5` | Filters the `CustomerId` column to show rows where the value is equal to 5. |
| `ORDER BY ii.InvoiceLineId` | Sorts the rows using the values from the `InvoiceLineId` column in ascending order. |

This query helped me practice retrieving specific columns, joining multiple tables, filtering records, and sorting the results.

---

## 3. A Mistake or Struggle

For this section, my answer is the same code I used in Section 2.

The reason I was proud of this code was that I had a difficult time figuring it out because of the number of requirements.

Initially, I kept receiving the following error message:

```text
SQL Error [1]:
[SQLITE_ERROR] SQL error or missing database
(no such column: i.CustomerId)
```

I did not initially realize that I was referencing the wrong table for my `LEFT JOIN`.

After reviewing my query, I was able to identify the correct table relationships and write the following code:

```sql
SELECT
    c.CustomerId,
    c.FirstName,
    c.LastName,
    t.Name AS TrackName,
    ii.Quantity,
    ii.UnitPrice
FROM customers c
LEFT JOIN invoices i
    ON c.CustomerId = i.CustomerId
LEFT JOIN invoice_items ii
    ON i.InvoiceId = ii.InvoiceId
LEFT JOIN tracks t
    ON t.TrackId = ii.TrackId
WHERE c.CustomerId = 5
ORDER BY ii.InvoiceLineId;
```

This experience taught me the importance of understanding table relationships and checking which columns belong to each table before writing a query.

---

## 4. Connecting to the Real World

SQL is still widely used for working with data because the basics are surprisingly easy to learn and understand.

Much like Python, SQL queries are written in simple English-like statements that are relatively easy to read. SQL is also very efficient at retrieving multiple rows and columns of data.

While Excel can also handle data, there are limits to how much data it can load and process efficiently. With SQL, the practical limits depend on the database system, its configuration, and the available hardware resources, such as RAM.

Learning SQL will help me work with larger datasets and complement the Python and Pandas skills I am currently developing.

---

## 5. Self-Assessment

The following table represents my current self-assessment of my SQL knowledge, using a scale of 1 to 5.

**Rating scale:** 1 = Lowest confidence, 5 = Highest confidence.

| Topic | Rating |
|---|:---:|
| Basic `SELECT`, `WHERE`, `ORDER BY` | 5/5 |
| Aggregation (`COUNT`, `SUM`, `AVG`, `GROUP BY`, `HAVING`) | 3/5 |
| Joins (2 tables) | 5/5 |
| Joins (3 or more tables) | 2/5 |
| Subqueries | 1/5 |
| CTEs (`WITH`) and window functions | 1/5 |
| `CREATE`, `INSERT`, `UPDATE`, `DELETE` | 1/5 |

### Two Highest Ratings

I marked **Basic SELECT, WHERE, ORDER BY** and **Joins (2 Tables)** as my highest-rated topics because they felt very straightforward for me.

### Three Lowest Ratings

The main reason I rated **Subqueries, CTEs and window functions, and CREATE, INSERT, UPDATE, DELETE** the lowest in my self-assessment is honestly because I have not had the time to study them in detail.

I am confident that I will learn them and use them in my SQL journey, but that may take a few more days, if not weeks.

---

## 6. Goals and Next Steps

By next week, I will focus on the following goals:

- Learn the basics of **subqueries** and **common table expressions (CTEs)**.
- Improve my ability to query using the **Core SQL SELECT Statement**.
- Develop a deeper understanding of **SQL joins**.
- Memorize the seven-step guide for retrieving data in SQL.

The seven steps are:

```sql
SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY
LIMIT;
```

I will continue practicing these concepts to improve my ability to retrieve, filter, combine, and analyze data using SQL.

---

*This reflection documents my current learning progress and the areas I plan to improve as I continue developing my SQL skills.*
