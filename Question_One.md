### Question - 1

You have the following database tables:

**divisions**

| id | name |
| -- | ---- |

**departments**

| id | name | division_id |
| -- | ---- | ----------- |

**teams**

| id | name | department_id |
| -- | ---- | ------------- |

**users**

| id | name | team_id |
| -- | ---- | ------- |

---

### Task

Write an SQL query to display the following information:

```
user_id, user_name, team_id, team_name, department_id, department_name, division_id, division_name
```
