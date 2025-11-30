# Music Library Database Project 🧩🎶🎧

## Overview  🔰

🎹 The Music Library Database Project is a relational database management system designed to organize and manage music-related data such as; 

Artists, 
albums, 
songs, 
users, 
playlists  and user favorites.

🎹 It provides a structured framework for storing, querying, and analysing music-related information efficiently.

## Purpose ❇️

The main purpose of this project is to create a comprehensive database system that enables users to:

- Store information about artists, albums, songs, users, and playlists.
- Manage user preferences, such as favorite songs and albums.
- Explore music data through various queries and analyses.
- Facilitate the creation and management of playlists.
- Provide insights into music trends and user preferences.

## ✨ Features ✨

### 1. Data Model 💿

*The database consists of the following 6 main tables:*

1.  **Artists:** Stores information about music artists.

To View the contents of each table execute the following :

[ SELECT * FROM Artists; } --- ( switch out Artists with the name of the table your trying to retieve data from.

| artist_id | name           | nationality | genre      |
|-----------|----------------|-------------|------------|
| 1         | The Weeknd     | Canadian    | R&B        |
| 2         | Taylor Swift   | American    | Pop        |
| 3         | Ariana Grande  | American    | Pop        |
| 4         | Rihanna        | Bajan   | R&B        |


2.  **Albums:** Stores information about music albums, including release date and genre.

| album_id | Title                        | artist_id | release_date | Genre     |
|----------|------------------------------|-----------|--------------|-----------|
| 1        | Dawn FM                      | 1         | 2022-01-07   | R&B/Soul  |
| 2        | After Hours                  | 1         | 2020-03-20   | R&B/Soul  |
| 3        | The Tortured Poets Department| 2         | 2024-04-19   | Folk-pop  |
| 4        | Midnights                    | 2         | 2022-10-21   | Electropop|
| 5        | Eternal Sunshine             | 3         | 2024-03-08   | Pop       |
| 6        | Positions                    | 3         | 2020-10-30   | R&B/Soul  |
| 7        | Anti                         | 4         | 2016-01-28   | R&B/Soul  |
| 8        | Unapologetic                 | 4         | 2012-11-19   | Pop       |

3.  **Songs:** Stores information about individual songs, including title, duration, and track number.

| song_id | Title                                | Duration | track_number | album_id |
|---------|--------------------------------------|----------|--------------|----------|
| 1       | Blinding Lights                      | 00:03:20 | 9            | 2        |
| 2       | Out of Time                          | 00:03:35 | 7            | 1        |
| 3       | Fortnight                            | 00:03:49 | 1            | 3        |
| 4       | Anti-Hero                            | 00:03:21 | 3            | 4        |
| 5       | We can’t be friends (wait for your love)| 00:03:49 | 10           | 5        |
| 6       | 34+35                                | 00:02:54 | 2            | 6        |
| 7       | Work                                 | 00:03:39 | 4            | 7        |
| 8       | Diamonds                             | 00:03:45 | 2            | 8        |

4.  **Users:** Stores information about system users, including username and email.
5.  **Playlists:** Stores information about user-created playlists.
6.  **UserFavorites:** Stores information about user-favorited songs and albums.

### 2.Stored Procedures ❌ Functions
The project includes stored procedures and functions for:

#### Stored Procedures ✅
-  Retrieving album counts for artists.


-  1.  Call the stored procedure to get album count for 'Rihanna'

  {  CALL GetArtistAlbumCount('Rihanna'); }

#### Stored Functions 🛑
-  2. Calculating the release year of albums.
-  3. Determining the genre of an artist's albums.

*-- Query to get the release year of an album using the stored function*

SELECT album_id, title, GetAlbumReleaseYear(album_id) AS release_year
FROM Albums;

*-- Integrate the GetArtistAlbumGenre stored function into a query.*

{ SELECT name AS artist_name, GetArtistAlbumGenre(name) AS album_genre
FROM Artists; }


### 3. Views 🌊 🌃
- - A view named *MusicLibrary* is created to combine data from the *Artists*, *Albums*, and *Songs* tables.

- - This provides easier access to music-related information.

Songs Released in a Specific Year:

{ SELECT 
    song_title,
    album_title,
    artist_name,
    YEAR(album_release_date) AS release_year
FROM 
    MusicLibrary
WHERE 
    YEAR(album_release_date) = 2022
ORDER BY 
    artist_name, album_title, song_title; } 


### 4. Error Handling ⧮
**Error handling** is implemented throughout the project to prevent duplicate object creation and ensure data integrity.

### 5. Query Optimization 🔆
**Indexes** are created on foreign key columns to optimize query performance.

### 6. Triggers 🫵

A trigger named *UpdateArtistGenre* was created to automatically updates the genre of an artist when a new album is inserted into the database.

### 7. Event 🎭
An event named *UpdateFavoritePlaylist* was created to update the user's favorite playlist based on their recent listening history.

### 8. Usage 🪫

 **Database Creation:** 
 
 The project starts by creating the music_library database if it doesn't exist and switching to it.

- **Table Creation and Data Insertion:** The necessary tables (***Artists, Albums, Songs, Users, Playlists, UserFavorites***) are created, and sample data is inserted into them.

- **Stored Procedures X Functions:** Stored procedures and functions are created to perform various operations, such as retrieving album counts and determining album release years and genres.

- **Views:** A view named MusicLibrary is created to combine data from multiple tables for easy access.

- **Error Handling:** Error handling is implemented to prevent duplicate object creation and ensure data integrity.

- **Query Optimization:** Indexes are created on foreign key columns to optimize query performance.

- **Triggers:**

1. First query the Artists table to view the current genre of an artist.

   [ SELECT * FROM Artists; ]

This will show you the current genre of each artist in the database.


2. Update the genre of an album associated with a particular artist. 

For example, I want to update the genre of an album for "The Weeknd" from "R&B" to "Alternative R&B".

{ UPDATE Albums
SET genre = 'Alternative R&B'
WHERE artist_id = (SELECT artist_id FROM Artists WHERE name = 'The Weeknd')
LIMIT 1;  }

After running this query, the genre of the album should be updated.

3. Verify the Trigger's Effect:

Query the Artists table again to verify if the genre of the artist has been updated according to Trigger 4.

{ SELECT * FROM Artists WHERE name = 'The Weeknd'; }

- **Event:** 

SHOW EVENTS;  -- make sure the event exists

Scheduled to run periodically (every day in my case)

{ SELECT * FROM Playlists WHERE title = 'My Favorites'; }



Monitor Event Status:
monitor the event's status and last execution time using the information_schema.events table.


## Conclusions 💭

- - This project provides a robust and efficient solution for managing music-related data. 

- - It offers a comprehensive set of features for storing, querying, and analyzing music information.

- - This makes it a valuable tool for music enthusiasts, researchers, and industry professionals alike.
