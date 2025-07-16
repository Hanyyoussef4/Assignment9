# 📦 Module 9: Working with Raw SQL in pgAdmin

## 📁 Directory Structure

```
module9_is601/
├── screenshots/
│   ├── docker_ps.png
│   ├── Successful run of Docker Compose services.png
│   ├── CREATE TABLE_USER.png
│   ├── CREATE_TABLE_CALCULATIONS.png
│   ├── Insert 02 (records to user table).png
│   ├── Insert 03 (records to Calculations Table).png
│   ├── Select_From_Order By.png
│   ├── Join Tables.png
│   ├── Update Record in Table.png
│   └── Delete Record from Table.png
├── Documentation/
│   ├── Module9_Working with Raw SQL in pgAdmin.pdf
│   ├── Module9_Reflection.docx
├── docker-compose.yml
├── Dockerfile
├── main.py
├── README.md
└── requirements.txt
```

---

## 🚀 Quick Start

1. **Clone the repository**

   ```bash
   git clone https://github.com/Hanyyoussef4/Assignment9.git
   cd Assignment9
   ```
2. **Build and launch services**

   ```bash
   docker compose up --build -d
   ```
3. **Verify containers**

   ```bash
   docker compose ps
   ```
4. **Access pgAdmin**

   * Open [http://localhost:5050](http://localhost:5050)
   * Create server with:

     * Host: `db`, Port: `5432`, Database: `fastapi_db`, 
   * Open Query Tool on `fastapi_db`.
*username and password "see the docker compose file"
---

## 📖 Documentation & Evidence

* **GitHub Repository:**
  [https://github.com/Hanyyoussef4/Assignment9.git](https://github.com/Hanyyoussef4/Assignment9.git)

* **Docker Compose Setup:**
  All services defined in `docker-compose.yml` build and run without errors; confirmed via `docker compose ps` listing all three services as "Up".

* **Documentation Files (in `Documentation/`):**

  * `Module9_Working with Raw SQL in pgAdmin.pdf` (PDF with embedded screenshots and captions)
  * `Module9_Reflection.docx` (Reflection on key experiences and challenges)

* **Screenshots (in `screenshots/`):**

  1. `docker_ps.png` – `docker compose ps` output showing `db`, `pgadmin`, and `api` services all Up.
  2. `Successful run of Docker Compose services.png` – Logs confirming all containers started without errors.
  3. `CREATE TABLE_USER.png` – `CREATE TABLE users` executed successfully.
  4. `CREATE_TABLE_CALCULATIONS.png` – `CREATE TABLE calculations` executed successfully.
  5. `Insert 02 (records to user table).png` – `INSERT` into `users` and subsequent `SELECT * FROM users` displaying inserted rows.
  6. `Insert 03 (records to Calculations Table).png` – `INSERT` into `calculations` and subsequent `SELECT * FROM calculations` displaying inserted rows.
  7. `Select_From_Order By.png` – `SELECT id, ... ORDER BY id;` showing current `id` values for calculations.
  8. `Join Tables.png` – Results of join between `users` and `calculations`.
  9. `Update Record in Table.png` – `UPDATE calculations SET result = 6 WHERE id = <correct_id>;` returned `UPDATE 1`.
  10. `Delete Record from Table.png` – `DELETE FROM calculations WHERE id = <correct_id>;` returned `DELETE 1`.

---

## 📝 SQL Scripts

### (A) Create Tables

```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  username VARCHAR(50) NOT NULL UNIQUE,
  email VARCHAR(100) NOT NULL UNIQUE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE calculations (
  id SERIAL PRIMARY KEY,
  operation VARCHAR(20) NOT NULL,
  operand_a FLOAT NOT NULL,
  operand_b FLOAT NOT NULL,
  result FLOAT NOT NULL,
  timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  user_id INTEGER NOT NULL,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

### (B) Insert Records

```sql
INSERT INTO users (username, email)
VALUES
  ('alice', 'alice@example.com'),
  ('bob',   'bob@example.com'),
  ('hany',  'hy326@njit.edu');

INSERT INTO calculations (operation, operand_a, operand_b, result, user_id)
VALUES
  ('add',      2, 3,  5, 1),
  ('divide',  10, 2,  5, 2),
  ('multiply', 4, 5, 20, 3);
```

### (C) Query Data

```sql
SELECT * FROM users;
SELECT * FROM calculations;
SELECT u.username, c.operation, c.operand_a, c.operand_b, c.result
FROM calculations c
JOIN users u ON c.user_id = u.id;
```

### (D) Update a Record

```sql
UPDATE calculations
SET result = 6
WHERE id = <correct_id>;
```

### (E) Delete a Record

```sql
DELETE FROM calculations
WHERE id = <correct_id>;
```

---

## 📋 Submission

1. Ensure `Documentation/` and `screenshots/` contain your evidence PDF, reflection doc, and raw screenshots.
2. Commit all changes:

   ```bash
   git add .
   git commit -m "Complete Module 9: SQL evidence and documentation"
   git push origin main
   ```
3. Submit your GitHub repo URL as instructed by your instructor.
