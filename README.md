---
author: Lektion 6
date: MMMM dd, YYYY
paging: "%d / %d"
---

# Teams lektion 6

## Agenda

1. Frågor och repetition
2. Introduktion till normalisering
3. Genomgång av övningar (7 & 9)
4. Eget arbete med handledning

---

# Introduktion till normalisering

En samling med sätt, så kallade normalformer, att designa och strukturera tabeller för att uppnå integritet och förhindra data duplicering.

Normalformer: 1NF, 2NF & 3NF. Varje form har specifika regler att följa.

---

# Ett exempel utan normalisering

```sql
CREATE TABLE book_orders (
  isbn TEXT,
  title TEXT,
  author TEXT,
  author_email TEXT,
  customer_id INT,
  customer_name TEXT,
  date DATE,
  price DECIMAL
);
```

Data upprepas med den tabellen. Som exempel upprepas `author` för varje order med samma bok.

---

# Normalformer

## Första formen (1NF)

Varje rad och kolumn (cell) måste ha endast ett värde. En cell får inte innehålla en lista. "Listor" av saker skall hanteras genom relationer.

Följer inte 1NF:

| person_id | emails       |
| --------- | ------------ |
| 1         | mail1, mail2 |

## Andra formen (2NF)

Alla kolumner måste vara helt beroende av alla primära nycklar.

Följer inte 2NF: `student_id | student_name | course_id | course_name | course_description`

## Tredje formen (3NF)

Tabell får inte ha beroenden till kolumner (i andra tabeller) som inte är nycklar. Relationer får endast byggas genom nycklar.

Följer inte 3NF: `patient_id | patient_name | doctor_number`

---

# Exempel utan normalisering

```sql
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    date DATE,
    product_ids TEXT,
    product_amounts TEXT,
    product_descriptions TEXT,
    total_price DECIMAL,
);
```

---

# Exempel med normalisering

```sql
CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    date DATE,
);

CREATE TABLE order_items (
    order_id INT REFERENCES orders(id),
    product_id INT REFERENCES products(id),
    product_amount INT,
    PRIMARY KEY (order_id, product_id)
);

CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    description TEXT,
    price DECIMAL
);
```

---

# Tips vid design av tabeller

- Använd `SERIAL` eller `UUID` för primära nycklar
  - De är enkla att hantera, behöver aldrig ändras och är unika
- Separera tabeller konceptuellt
  - Exempel: studerande och kurser är inte samma sak, gör dem till separata tabeller
- Skapa nya tabeller för "listor" av saker, och bilda relationer
- Följ principer för normalisering
