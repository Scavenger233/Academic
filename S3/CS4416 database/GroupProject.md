### Schema: `modified_concerts_schema.sql`

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

### Sample Data: `data.sql`

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
