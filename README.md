# sql-to-ar-translations
SQL to Active Record translations (practice exercises)

## Authors
Morgan and Vishal.

## Exercises

### SQL to AR
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

### AR to SQL

1)
```ruby
Post.all
```
```sql
SELECT *
FROM posts
```

2)
```ruby
Post.first
```

```sql
SELECT *
FROM posts
ORDER BY id
LIMIT 1
```

3)
```ruby
Post.last
```

```sql
SELECT *
FROM posts
ORDER BY id DESC
LIMIT 1
```

4)
```ruby
Post.where(:id => 4)
```

```sql
SELECT *
FROM posts
WHERE id=4
```

5)
```ruby
Post.find(4)
```

```sql
SELECT *
FROM posts
WHERE id=4
```

6)
```ruby
User.count
```

```sql
SELECT COUNT(*)
FROM posts
```

7)
```ruby
Post.select(:name).where(:created_at > 3.days.ago).order(:created_at)
```

```sql
SELECT name
FROM posts
ORDER BY created_at
WHERE created_at > DATEADD(day,-3,GETDATE())
```

8)
```ruby
Post.select("COUNT(*)").group(:category_id)
```

```sql
SELECT COUNT(*)
FROM posts
GROUP BY category_id
```

9)
```ruby
All posts created before 2014
```

```sql
SELECT *
FROM posts
WHERE created_at < 2014
```

10)
```ruby
A list of all (unique) first names for authors who have written at least 3 posts
```

```sql
SELECT DISTINCT first_name, COUNT(*)
FROM authors
JOIN posts ON authors.id=posts.authorid
GROUP BY authors.id
HAVING COUNT(*) >= 3
```

11)
```ruby
The posts with titles that start with the word "The"
```

```sql
SELECT *
FROM posts
WHERE title LIKE 'The%'
```

12)
```ruby
Posts with IDs of 3,5,7, and 9
```

```sql
SELECT *
FROM posts
WHERE id IN (3,5,7,9)
```

### Custom Translation: 3 Queries

1) How many posts are written by authors who are older than 46?
```sql
SELECT COUNT(*)
FROM posts JOIN authors ON posts.authorid = authors.id
WHERE age > 46
```
```ruby
Post.joins("JOIN authors ON posts.authorid = authors.id")
    .where("age > 46")
    .count
```

2) Which author has written the most posts?
```sql
SELECT name
FROM authors JOIN posts ON authors.id = posts.authorid
GROUP BY authors.id
ORDER BY COUNT(*)
LIMIT 1
```
```ruby
Author.joins("JOIN posts ON authors.id = posts.authorid")
      .group("authors.id")
      .order("COUNT(*)")
      .first
```

3)
```sql

```
```ruby

```

