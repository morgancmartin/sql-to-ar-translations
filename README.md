# sql-to-ar-translations
SQL to Active Record translations (practice exercises)

## Authors
Morgan and Vishal.

## Exercises

1)
```sql
SELECT *
FROM
users;
```
```ruby
User.all
```

2)
```sql
SELECT *
FROM
users
WHERE
user.id = 1;
```
```ruby
User.find(1)
```

3)
```sql
SELECT *
FROM posts
ORDER BY created_at DESC
LIMIT 1;
```
```ruby
Post.all.last
```

4)
```sql
SELECT *
FROM users JOIN posts
ON posts.author_id = users.id
WHERE
posts.created_at >= '2014-08-31 00:00:00';
```
```ruby
User.joins("JOIN posts ON posts.author_id = users.id")
    .where("posts.created_at > '2014-08-31 00:00:00'")
```

5)
```sql
SELECT
count(*)
FROM users
GROUP BY favorite_color
HAVING count(*) > 1;
```
```ruby
User.select("COUNT(*) AS color_count")
  .group(:favorite_color)
  .having("color_count > 1")
```

