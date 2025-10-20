## 🧮 SQL Question: Person and Address Join

### Table: `Person`

| Column Name | Type    |
| ----------- | ------- |
| personId    | int     |
| lastName    | varchar |
| firstName   | varchar |

* `personId` is the **primary key** (column with unique values) for this table.
* This table contains information about the **ID**, **first name**, and **last name** of each person.

---

### Table: `Address`

| Column Name | Type    |
| ----------- | ------- |
| addressId   | int     |
| personId    | int     |
| city        | varchar |
| state       | varchar |

* `addressId` is the **primary key** for this table.
* Each row contains information about the **city** and **state** of one person with the matching `personId`.

---

### 🧩 Task

Write a SQL query to **report the first name, last name, city, and state** of each person in the `Person` table.
If a person’s address is **not present** in the `Address` table, report **NULL** for the city and state.

Return the result table in any order.

---

### 📊 Example

#### Input

**Person table:**

| personId | lastName | firstName |
| -------- | -------- | --------- |
| 1        | Wang     | Allen     |
| 2        | Alice    | Bob       |

**Address table:**

| addressId | personId | city          | state      |
| --------- | -------- | ------------- | ---------- |
| 1         | 2        | New York City | New York   |
| 2         | 3        | Leetcode      | California |

---

#### Output

| firstName | lastName | city          | state    |
| --------- | -------- | ------------- | -------- |
| Allen     | Wang     | NULL          | NULL     |
| Bob       | Alice    | New York City | New York |

---

### 💡 Explanation

* `personId = 1` does **not** exist in the `Address` table → returns `NULL` for city and state.
* `personId = 2` exists in the `Address` table → returns corresponding city and state.
