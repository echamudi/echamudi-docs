# SQL

## Copy from another table

```SQL
UPDATE BeerReviewsWithText
SET beer_brewername = (SELECT brewery_name
                       FROM BR.BeerReviews
                       WHERE ID = BeerReviewsWithText.ID)
```

https://stackoverflow.com/questions/17702902/in-sqlite3-copy-a-column-from-one-table-to-another-table


