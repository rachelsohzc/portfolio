+++
title = "Creating an e-commerce database"
description = ""
type = ["posts","post"]
tags = [
    "Databases",
    "Relational DBs",
    "Python",
    "SQLite",
    "DBBrowser",
]
date = "2022-01-21"
categories = [
    "Databases",
    "Python",
]
+++

[THIS IS AN COMPLETED PROJECT](https://github.com/rachelsohzc/E-commerce-Database)

We wanted to mimic a database of a huge e-commerce site like Amazon. This project solely focuses on breaking down a huge database into smaller tables to deliver both operations and insights.

You can find some main features of the project here:

### Database rules

Since we broke down the company’s database into smaller tables, we needed a way to connect certain records while running queries. Therefore, we made primary keys during the creation of the tables for table matching for queries.

```
{{ create_products_query = '''CREATE TABLE IF NOT EXISTS Products (
ProductID TEXT PRIMARY KEY,
Category TEXT NOT NULL,
SubCategory TEXT NOT NULL,
Brand TEXT NOT NULL,
ProdDescription TEXT NOT NULL)
''' }}
```

Going back to the real-life scenario of a company, we can use an example. For instance, if Amazon had a ratings input that ranged from 1 to 5, a value outside of 1 to 5 shouldn’t be allowed to be entered into the database. Therefore, we also made relevant triggers for each table.

```
{{ trigger_1 = '''
CREATE TRIGGER bef_update_RRating BEFORE UPDATE ON Reviews
BEGIN
SELECT CASE
WHEN ((SELECT Reviews.RRating FROM Reviews WHERE NEW.RRating < 1 OR NEW.RRating > 5) IS NOT NULL)
THEN RAISE(FAIL, 'ERROR: Invalid rating score.')
END;
END;
'''}}
```

View the full project repository **[here](https://github.com/rachelsohzc/E-commerce-Database)**