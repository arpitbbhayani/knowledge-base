Instagram has millions of photos, and each has tens of hashtags, so how does Instagram efficiently serves hashtags for a search query?

Instagram uses Postgres as its primary transactions database. For each hashtag, it stores the `media_count` in a table. This allows us to render the Hashtag and some meta information on the search page.

Note: Instagram could also use a dedicated search engine for this usecase, but this usecase is trivial to use something as sophisticated as ElasticSearch. We take a look at how they do it with Postgres.

A naive query to get hashtags for a given prefix ordered by count would look something like this

```
SELECT * from hashtags
WHERE name LIKE 'snow%'
ORDER BY media_count
DESC LIMIT 10;
```

Executing this query would require the database engine to filter out the hashtags starting with `snow` and then sort. Sorting is an expensive operation and this query required the engine to sort 15000 rows.

Under high load, this sorting becomes a pain. So, what's the way out?

The key insight here is the fact that hashtags have a long-tail distribution i.e. most hashtags will have far fewer media counts and while serving we are always ordering by `media_count`.

Hence, instead of indexing everything, we can simply index the hashtags having `media_count > 100` because other hashtags are highly unlikely to be surfaced.

## Partial Indexes

Postgres database has this exact same capability and it is called Partial Indexing. With partial indexes, we can keep only a subset of data in the index.

We can create a partial index on our hashtags table like

```
CREATE INDEX CONCURRENTLY ON hashtags WHERE media_count > 100;
```

With this index, the query we fire would have to scan a very limited number of index entries to spit out the result.

The SQL query to get hashtags with the prefix `snow%` would look something like this

```
SELECT * from hashtags
WHERE name LIKE 'snow%'
AND media_count > 100
ORDER BY media_count
DESC LIMIT 10;
```

The above query required it to sort only 169 rows, completing its evaluation superfast. This is a classic usecase where we all can utilize Partial Indexes.