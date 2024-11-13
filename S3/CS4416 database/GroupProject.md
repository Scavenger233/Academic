# Modified_schma
```sql

-- Artists table
CREATE TABLE artists (
  artist_id INTEGER(10) PRIMARY KEY,
  artist_name VARCHAR(128),
  genre VARCHAR(64),
  debut_year YEAR
);

-- Albums table
CREATE TABLE albums (
  album_id INTEGER(10) PRIMARY KEY,
  artist_id INTEGER(10),
  album_title VARCHAR(256),
  release_date DATE,
  FOREIGN KEY (artist_id) REFERENCES artists(artist_id)
);

-- Songs table
CREATE TABLE songs (
  song_id INTEGER(10) PRIMARY KEY,
  album_id INTEGER(10),
  song_title VARCHAR(128),
  length REAL,
  release_date DATE,
  FOREIGN KEY (album_id) REFERENCES albums(album_id)
);

-- Concerts table
CREATE TABLE concerts (
  concert_id INTEGER(10) PRIMARY KEY,
  artist_id INTEGER(10),
  concert_title VARCHAR(256),
  location VARCHAR(256),
  date_of_concert DATE,
  FOREIGN KEY (artist_id) REFERENCES artists(artist_id)
);

-- !!!Multiple artists per album
CREATE TABLE album_artists (
  album_id INTEGER(10),
  artist_id INTEGER(10),
  PRIMARY KEY (album_id, artist_id),
  FOREIGN KEY (album_id) REFERENCES albums(album_id),
  FOREIGN KEY (artist_id) REFERENCES artists(artist_id)
);

-- !!!Multiple artists per song
CREATE TABLE song_artists (
  song_id INTEGER(10),
  artist_id INTEGER(10),
  PRIMARY KEY (song_id, artist_id),
  FOREIGN KEY (song_id) REFERENCES songs(song_id),
  FOREIGN KEY (artist_id) REFERENCES artists(artist_id)
);

-- !!!Multiple artists per concert
CREATE TABLE concert_artists (
  concert_id INTEGER(10),
  artist_id INTEGER(10),
  PRIMARY KEY (concert_id, artist_id),
  FOREIGN KEY (concert_id) REFERENCES concerts(concert_id),
  FOREIGN KEY (artist_id) REFERENCES artists(artist_id)
);

-- Fans table
CREATE TABLE fans (
  fan_id INTEGER(10) PRIMARY KEY,
  fan_name VARCHAR(128),
  fan_email VARCHAR(128),
  age TINYINT(3)
);

-- Concert tickets table (store only fan_id to maintain consistency)
CREATE TABLE concert_tickets (
  ticket_id INTEGER(10) PRIMARY KEY,
  concert_id INTEGER(10),
  fan_id INTEGER(10),
  favourite_artist_id INTEGER(10),
  purchase_date DATE,
  ticket_price DOUBLE,
  seat_zone VARCHAR(16),
  seat_number VARCHAR(16),
  FOREIGN KEY (concert_id) REFERENCES concerts(concert_id),
  FOREIGN KEY (fan_id) REFERENCES fans(fan_id),
  FOREIGN KEY (favourite_artist_id) REFERENCES artists(artist_id)
);

-- !!!Multiple fans per ticket (many-to-many relationship)
CREATE TABLE ticket_fans (
  ticket_id INTEGER(10),
  fan_id INTEGER(10),
  PRIMARY KEY (ticket_id, fan_id),
  FOREIGN KEY (ticket_id) REFERENCES concert_tickets(ticket_id),
  FOREIGN KEY (fan_id) REFERENCES fans(fan_id)
);

-- !!!Multiple favorite artists per fan
CREATE TABLE fan_favorite_artists (
  fan_id INTEGER(10),
  artist_id INTEGER(10),
  PRIMARY KEY (fan_id, artist_id),
  FOREIGN KEY (fan_id) REFERENCES fans(fan_id),
  FOREIGN KEY (artist_id) REFERENCES artists(artist_id)
);

-- Songs performed in concerts
CREATE TABLE concert_songs (
  concert_id INTEGER(10),
  song_id INTEGER(10),
  order_performance TINYINT(4),
  FOREIGN KEY (concert_id) REFERENCES concerts(concert_id),
  FOREIGN KEY (song_id) REFERENCES songs(song_id)
);

```

# data.sql

```sql

-- Insert data for artists
INSERT INTO artists (artist_id, artist_name, genre, debut_year) VALUES
(1001, 'The Beatles', 'Rock', 1960),
(1002, 'Beyoncé', 'Pop', 1997);

-- Insert data for albums
INSERT INTO albums (album_id, artist_id, album_title, release_date) VALUES
(2001, 1001, 'Abbey Road', '1969-09-26'),
(2002, 1002, 'Lemonade', '2016-04-23');

-- Insert data for songs
INSERT INTO songs (song_id, album_id, song_title, length, release_date) VALUES
(3001, 2001, 'Come Together', 4.20, '1969-09-26'),
(3002, 2002, 'Formation', 3.26, '2016-04-23');

-- Insert data for concerts
INSERT INTO concerts (concert_id, artist_id, concert_title, location, date_of_concert) VALUES
(4001, 1001, 'The Beatles Live at Shea Stadium', 'New York', '1965-08-15'),
(4002, 1002, 'Beyoncé Formation World Tour', 'London', '2016-07-02');

-- Insert data for fans
INSERT INTO fans (fan_id, fan_name, fan_email, age) VALUES
(5001, 'Alice Smith', 'alice.smith@example.com', 28),
(5002, 'Bob Johnson', 'bob.johnson@example.com', 34);

-- Insert data for concert tickets
INSERT INTO concert_tickets (ticket_id, concert_id, fan_id, favourite_artist_id, purchase_date, ticket_price, seat_zone, seat_number) VALUES
(6001, 4001, 5001, 1001, '1965-08-01', 15.00, 'A', '12'),
(6002, 4002, 5002, 1002, '2016-06-20', 200.00, 'B', '45');

-- Insert data for ticket_fans (many-to-many relationship if needed)
INSERT INTO ticket_fans (ticket_id, fan_id) VALUES
(6001, 5001),
(6002, 5002);

-- Insert data for fan_favorite_artists (multiple favorite artists per fan)
INSERT INTO fan_favorite_artists (fan_id, artist_id) VALUES
(5001, 1001),
(5002, 1002);

-- Insert data for album_artists (multiple artists per album if needed)
INSERT INTO album_artists (album_id, artist_id) VALUES
(2001, 1001),
(2002, 1002);

-- Insert data for concert_artists (multiple artists per concert if needed)
INSERT INTO concert_artists (concert_id, artist_id) VALUES
(4001, 1001),
(4002, 1002);

-- Insert data for song_artists (multiple artists per song if needed)
INSERT INTO song_artists (song_id, artist_id) VALUES
(3001, 1001),
(3002, 1002);

-- Insert data for concert_songs (songs performed in concerts)
INSERT INTO concert_songs (concert_id, song_id, order_performance) VALUES
(4001, 3001, 1),
(4002, 3002, 1);

```
