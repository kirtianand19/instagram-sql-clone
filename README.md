# Instagram-Like SQL Database Implementation

## Project Description
This project involves designing and implementing a database schema for an Instagram-like application. The database includes various entities such as users, photos, comments, tags, and follows. A large dataset, simulating realistic user behaviors, was inserted to perform complex queries and analyze user engagement.

## Features
- **Schema Design**: Created tables for users, photos, comments, tags, and follows, ensuring normalization and referential integrity.
- **Data Insertion**: Inserted over 20,000 records with realistic user personas, including active users, lurkers, bots, and celebrities.
- **Data Analysis**: Executed complex queries to analyze user activity, detect inactive accounts, identify popular hashtags, and track engagement metrics.

## Technologies Used
- **Database**: MySQL
- **Tools**: MySql Workbench
- **Languages**: SQL

## Key Achievements
- Designed and implemented a robust database schema aligned with real-world application requirements.
- Developed a dataset with realistic user personas to enhance the reliability of data analyses.
- Successfully executed complex queries to extract valuable insights, supporting strategic decision-making.

## Database Schema
The database schema includes the following tables:
- **Users**: Stores user information.
- **Photos**: Stores photo information.
- **Comments**: Stores comments made by users on photos.
- **Tags**: Stores tags applied to photos.
- **Follows**: Stores information about which users follow which other users.

## Example Queries
### 1. Finding 5 Oldest Users
```sql
SELECT username, created_at 
FROM users 
ORDER BY created_at 
LIMIT 5;

### 2. Most Popular Registration Day
SELECT DAYNAME(created_at) AS Registration_Day, COUNT(*) AS registration_count 
FROM users 
GROUP BY Registration_Day 
ORDER BY registration_count DESC 
LIMIT 1;

### 3. Users Who Have Never Posted a Photo
SELECT username 
FROM users 
LEFT JOIN photos ON users.id = photos.user_id 
WHERE photos.created_at IS NULL;

### 4. Contest Winner for Most Likes on a Single Photo
SELECT photos.id, username, photos.image_url, COUNT(*) AS Total_Likes 
FROM photos 
INNER JOIN likes ON photos.id = likes.photo_id 
INNER JOIN users ON photos.user_id = users.id 
GROUP BY photos.id 
ORDER BY Total_Likes DESC 
LIMIT 1;

### 5. Average Posts per User
SELECT ROUND((SELECT COUNT(*) FROM photos) / (SELECT COUNT(*) FROM users), 2) AS avg;

### 6. Top 5 Most Commonly Used Hashtags
SELECT tag_name, COUNT(*) AS total 
FROM tags 
LEFT JOIN photo_tags ON tags.id = photo_tags.tag_id 
GROUP BY tags.id 
ORDER BY total DESC 
LIMIT 5;

### 7. Finding Bots: Users Who Have Liked Every Single Photo
SELECT username, COUNT(*) AS num_likes 
FROM likes 
INNER JOIN users ON likes.user_id = users.id 
GROUP BY username 
HAVING num_likes = (SELECT COUNT(*) FROM photos);


