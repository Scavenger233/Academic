# Schema: `modified_concerts_schema.sql`

```sql
CREATE TABLE Artist (
    artist_id INT PRIMARY KEY,
    name VARCHAR(255) NOT NULL
);

CREATE TABLE Album (
    album_id INT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    release_year INT
);

CREATE TABLE Song (
    song_id INT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    duration TIME
);

CREATE TABLE Concert (
    concert_id INT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    date DATE,
    location VARCHAR(255)
);

CREATE TABLE Fan (
    fan_id INT PRIMARY KEY,
    name VARCHAR(255) NOT NULL
);

CREATE TABLE Ticket (
    ticket_id INT PRIMARY KEY,
    concert_id INT,
    FOREIGN KEY (concert_id) REFERENCES Concert(concert_id)
);

-- Many-to-many relationship tables
CREATE TABLE Album_Artist (
    album_id INT,
    artist_id INT,
    PRIMARY KEY (album_id, artist_id),
    FOREIGN KEY (album_id) REFERENCES Album(album_id),
    FOREIGN KEY (artist_id) REFERENCES Artist(artist_id)
);

CREATE TABLE Song_Artist (
    song_id INT,
    artist_id INT,
    PRIMARY KEY (song_id, artist_id),
    FOREIGN KEY (song_id) REFERENCES Song(song_id),
    FOREIGN KEY (artist_id) REFERENCES Artist(artist_id)
);

CREATE TABLE Concert_Artist (
    concert_id INT,
    artist_id INT,
    PRIMARY KEY (concert_id, artist_id),
    FOREIGN KEY (concert_id) REFERENCES Concert(concert_id),
    FOREIGN KEY (artist_id) REFERENCES Artist(artist_id)
);

CREATE TABLE Fan_Favorite_Artist (
    fan_id INT,
    artist_id INT,
    PRIMARY KEY (fan_id, artist_id),
    FOREIGN KEY (fan_id) REFERENCES Fan(fan_id),
    FOREIGN KEY (artist_id) REFERENCES Artist(artist_id)
);

CREATE TABLE Fan_Ticket (
    fan_id INT,
    ticket_id INT,
    PRIMARY KEY (fan_id, ticket_id),
    FOREIGN KEY (fan_id) REFERENCES Fan(fan_id),
    FOREIGN KEY (ticket_id) REFERENCES Ticket(ticket_id)
);

CREATE TABLE Album_Song (
    album_id INT,
    song_id INT,
    PRIMARY KEY (album_id, song_id),
    FOREIGN KEY (album_id) REFERENCES Album(album_id),
    FOREIGN KEY (song_id) REFERENCES Song(song_id)
);
```

## Sample Data: `data.sql`

```sql
-- Insert artists
INSERT INTO Artist (artist_id, name) VALUES (1, 'Artist A'), (2, 'Artist B');

-- Insert albums
INSERT INTO Album (album_id, title, release_year) VALUES (1, 'Album X', 2022), (2, 'Album Y', 2023);

-- Insert songs
INSERT INTO Song (song_id, title, duration) VALUES (1, 'Song One', '00:03:30'), (2, 'Song Two', '00:04:00');

-- Insert concerts
INSERT INTO Concert (concert_id, name, date, location) VALUES (1, 'Concert 1', '2024-11-10', 'Venue A'), (2, 'Concert 2', '2024-11-12', 'Venue B');

-- Insert fans
INSERT INTO Fan (fan_id, name) VALUES (1, 'Fan X'), (2, 'Fan Y');

-- Insert tickets
INSERT INTO Ticket (ticket_id, concert_id) VALUES (1, 1), (2, 2);

-- Insert relationships
INSERT INTO Album_Artist (album_id, artist_id) VALUES (1, 1), (1, 2), (2, 2);
INSERT INTO Song_Artist (song_id, artist_id) VALUES (1, 1), (2, 2);
INSERT INTO Concert_Artist (concert_id, artist_id) VALUES (1, 1), (2, 2);
INSERT INTO Fan_Favorite_Artist (fan_id, artist_id) VALUES (1, 1), (2, 2);
INSERT INTO Fan_Ticket (fan_id, ticket_id) VALUES (1, 1), (2, 2);
INSERT INTO Album_Song (album_id, song_id) VALUES (1, 1), (1, 2), (2, 1);
```


# To demonstrate advanced SQL skills, we can create a view that provides insights into the most popular artists based on ticket purchases. This view will aggregate the number of tickets purchased for each artist and filter only those artists who have a high number of tickets sold, showcasing usage of `JOIN`, `GROUP BY`, and `HAVING` clauses.

The view will be called `PopularArtists`, and it will display:
- `artist_id`
- `artist_name`
- `concert_count` (number of concerts associated with the artist)
- `total_tickets` (total number of tickets purchased for this artist's concerts)

The criteria for popularity is defined as artists who have had more than a threshold number of tickets sold across all their concerts.

### SQL to Create the View (PopularArtists)

```sql
CREATE VIEW PopularArtists AS
SELECT 
    a.artist_id,
    a.name AS artist_name,
    COUNT(DISTINCT ac.concert_id) AS concert_count,
    COUNT(ft.ticket_id) AS total_tickets
FROM 
    Artists a
JOIN 
    Artists_Concerts ac ON a.artist_id = ac.artist_id
JOIN 
    Tickets t ON ac.concert_id = t.concert_id
JOIN 
    Fans_Tickets ft ON t.ticket_id = ft.ticket_id
GROUP BY 
    a.artist_id, a.name
HAVING 
    COUNT(ft.ticket_id) > 5;
```

### Explanation of the View

1. **JOIN Operations**: 
   - We join `Artists` and `Artists_Concerts` to get all concerts associated with each artist.
   - Then, we join `Tickets` and `Fans_Tickets` to account for all tickets purchased by fans for those concerts.

2. **GROUP BY Clause**:
   - We group by `artist_id` and `name` to aggregate data for each artist.

3. **Aggregation Functions**:
   - `COUNT(DISTINCT ac.concert_id)` gives the number of unique concerts an artist has participated in.
   - `COUNT(ft.ticket_id)` gives the total tickets purchased for that artist’s concerts.

4. **HAVING Clause**:
   - We use `HAVING` to filter artists with more than 5 total tickets purchased (this threshold can be adjusted as needed to define "popularity").

This view provides insights into popular artists based on ticket purchases and demonstrates advanced SQL features like complex joins, grouping, and filtering with `HAVING`.

# Here are two triggers for the modified schema: a `BEFORE` trigger and an `AFTER` trigger.

### 1. BEFORE Trigger
The `BEFORE` trigger will ensure that when inserting a new concert, the date cannot be in the past. If an attempt is made to add a concert with a past date, the trigger will raise an error, preventing the insertion.

#### Trigger Code

```sql
DELIMITER //

CREATE TRIGGER check_concert_date_before_insert
BEFORE INSERT ON Concerts
FOR EACH ROW
BEGIN
    IF NEW.concert_date < CURDATE() THEN
        SIGNAL SQLSTATE '45000' 
        SET MESSAGE_TEXT = 'Concert date cannot be in the past';
    END IF;
END;
//

DELIMITER ;
```

#### Explanation:
- **Trigger Event**: `BEFORE INSERT`
- **Table**: `Concerts`
- **Condition**: Checks if `NEW.concert_date` is earlier than the current date (`CURDATE()`).
- **Action**: If the concert date is in the past, an error is raised, and the insertion is prevented.

### 2. AFTER Trigger
The `AFTER` trigger will update a counter of total tickets purchased for each concert whenever a new ticket is added. This trigger can maintain an additional field, `total_tickets`, in the `Concerts` table, which keeps track of the number of tickets purchased for each concert.

Assuming we add a `total_tickets` column to the `Concerts` table to hold this information:

#### Table Modification (Adding total_tickets)

```sql
ALTER TABLE Concerts
ADD COLUMN total_tickets INT DEFAULT 0;
```

#### Trigger Code

```sql
DELIMITER //

CREATE TRIGGER update_total_tickets_after_insert
AFTER INSERT ON Fans_Tickets
FOR EACH ROW
BEGIN
    UPDATE Concerts
    SET total_tickets = total_tickets + 1
    WHERE concert_id = (SELECT concert_id FROM Tickets WHERE ticket_id = NEW.ticket_id);
END;
//

DELIMITER ;
```

#### Explanation:
- **Trigger Event**: `AFTER INSERT`
- **Table**: `Fans_Tickets`
- **Condition**: This trigger activates whenever a new ticket purchase (i.e., new entry in `Fans_Tickets`) is recorded.
- **Action**: Updates the `total_tickets` column in the `Concerts` table, incrementing it by 1 for the relevant concert based on `ticket_id`.

These triggers help ensure data integrity and maintain calculated fields within the database.

Here is a stored function that returns the total number of occupied seats for a given `concert_id`. This function will count the number of unique tickets associated with fans for the specified concert, which represents the total number of occupied seats.

# Stored Function Code

```sql
DELIMITER //

CREATE FUNCTION get_occupied_seats(concert_id INT)
RETURNS INT
DETERMINISTIC
BEGIN
    DECLARE total_seats INT;
    
    SELECT COUNT(DISTINCT ft.ticket_id) INTO total_seats
    FROM Fans_Tickets ft
    JOIN Tickets t ON ft.ticket_id = t.ticket_id
    WHERE t.concert_id = concert_id;
    
    RETURN total_seats;
END;
//

DELIMITER ;
```

### Explanation:

- **Parameters**: 
  - `concert_id` (INT): The ID of the concert for which we want to find the total number of occupied seats.

- **Local Variable**:
  - `total_seats`: This variable holds the total number of unique tickets (or occupied seats) for the specified concert.

- **Logic**:
  - We use a `SELECT` query to count distinct `ticket_id`s in the `Fans_Tickets` table, joined with the `Tickets` table to match the specified `concert_id`.
  - The `COUNT(DISTINCT ft.ticket_id)` ensures we only count unique tickets, giving us the total occupied seats for the concert.
  - Finally, we return `total_seats` as the result.

### Usage Example

```sql
SELECT get_occupied_seats(1);
```

This query would return the total number of occupied seats for the concert with `concert_id = 1`.

# Here’s a stored procedure that checks if a given `song_id` is associated with a specified `album_id`. If the association doesn’t exist, it inserts the relationship. Additionally, if the song’s release date is later than the album’s release date, it adjusts the song’s release date to match the album’s release date.

### Stored Procedure Code

```sql
DELIMITER //

CREATE PROCEDURE associate_song_with_album(
    IN song_id INT,
    IN album_id INT
)
BEGIN
    DECLARE song_exists INT DEFAULT 0;
    DECLARE album_release_date DATE;
    DECLARE song_release_date DATE;
    
    -- Check if the association already exists
    SELECT COUNT(*) INTO song_exists
    FROM Songs
    WHERE song_id = song_id AND album_id = album_id;
    
    -- If association doesn't exist, insert it
    IF song_exists = 0 THEN
        UPDATE Songs SET album_id = album_id WHERE song_id = song_id;
    END IF;
    
    -- Fetch album and song release dates
    SELECT release_date INTO album_release_date FROM Albums WHERE album_id = album_id;
    SELECT release_date INTO song_release_date FROM Songs WHERE song_id = song_id;

    -- Check if song's release date is later than album's, and adjust if needed
    IF song_release_date > album_release_date THEN
        UPDATE Songs
        SET release_date = album_release_date
        WHERE song_id = song_id;
    END IF;
END;
//

DELIMITER ;
```

### Explanation:

1. **Parameters**:
   - `song_id` (INT): The ID of the song to associate with the album.
   - `album_id` (INT): The ID of the album to associate with the song.

2. **Local Variables**:
   - `song_exists`: Used to check if the song is already associated with the album.
   - `album_release_date`: Stores the release date of the album.
   - `song_release_date`: Stores the release date of the song.

3. **Procedure Logic**:
   - First, the procedure checks if the song is already associated with the album by counting records in the `Songs` table with the given `song_id` and `album_id`.
   - If no such record exists (`song_exists = 0`), it updates the `album_id` for the song, associating it with the specified album.
   - Then, the procedure retrieves the release dates for the album and song.
   - If the song’s release date is later than the album’s release date, it updates the song’s release date to match the album’s release date.

This stored procedure ensures that the song is associated with the specified album and that its release date does not exceed the album’s release date.
