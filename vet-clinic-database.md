# 🐾 Vet Clinic Database

This project sets up a **vet clinic database** with animals’ information and sample queries.

---

## 📖 Getting Started

This repository includes files with plain SQL that can be used to recreate a database:

- `schema.sql` → defines the structure of the database.  
- `data.sql` → inserts sample records into the database.  
- `queries.sql` → contains queries to retrieve useful data.  

---

## 🗄️ Schema (`schema.sql`)

```sql
-- Create database
CREATE DATABASE vet_clinic;

-- Switch to the database
\c vet_clinic;

-- Create animals table
CREATE TABLE animals (
    id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    name VARCHAR(100),
    date_of_birth DATE,
    escape_attempts INT,
    neutered BOOLEAN,
    weight_kg DECIMAL(5,2)
);
````

---

## 🐕 Sample Data (`data.sql`)

```sql
-- Insert sample animals
INSERT INTO animals (name, date_of_birth, weight_kg, neutered, escape_attempts)
VALUES ('Agumon', '2020-02-03', 10.23, TRUE, 0);

INSERT INTO animals (name, date_of_birth, weight_kg, neutered, escape_attempts)
VALUES ('Gabumon', '2018-11-15', 8.00, TRUE, 2);

INSERT INTO animals (name, date_of_birth, weight_kg, neutered, escape_attempts)
VALUES ('Pikachu', '2021-01-07', 15.04, FALSE, 1);

INSERT INTO animals (name, date_of_birth, weight_kg, neutered, escape_attempts)
VALUES ('Devimon', '2017-05-12', 11.00, TRUE, 5);
```

---

## 🔎 Queries (`queries.sql`)

```sql
-- 1. Find all animals whose name ends in "mon".
SELECT * FROM animals WHERE name LIKE '%mon';

-- 2. List the name of all animals born between 2016 and 2019.
SELECT name FROM animals 
WHERE date_of_birth BETWEEN '2016-01-01' AND '2019-12-31';

-- 3. List the name of all animals that are neutered and have less than 3 escape attempts.
SELECT name FROM animals 
WHERE neutered = TRUE AND escape_attempts < 3;

-- 4. List the date of birth of all animals named either "Agumon" or "Pikachu".
SELECT date_of_birth FROM animals 
WHERE name IN ('Agumon', 'Pikachu');

-- 5. List name and escape attempts of animals that weigh more than 10.5kg.
SELECT name, escape_attempts FROM animals 
WHERE weight_kg > 10.5;

-- 6. Find all animals that are neutered.
SELECT * FROM animals WHERE neutered = TRUE;

-- 7. Find all animals not named Gabumon.
SELECT * FROM animals WHERE name <> 'Gabumon';

-- 8. Find all animals with a weight between 10.4kg and 17.3kg (inclusive).
SELECT * FROM animals 
WHERE weight_kg BETWEEN 10.4 AND 17.3;
```

---

## 📸 Screenshots

Run the queries above and take a screenshot of the results.
Attach the screenshot in your **Pull Request description**.

---

## 📝 License

This project is [MIT](./LICENSE) licensed.

