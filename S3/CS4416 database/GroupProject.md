# Modified_schma
```sql

-- for multiple artists per album
CREATE TABLE album_artists (
  album_id INTEGER(10),
  artist_id INTEGER(10),
  PRIMARY KEY (album_id, artist_id),
  FOREIGN KEY (album_id) REFERENCES albums(album_id),
  FOREIGN KEY (artist_id) REFERENCES artists(artist_id)
);

-- for multiple artists per song
CREATE TABLE song_artists (
  song_id INTEGER(10),
  artist_id INTEGER(10),
  PRIMARY KEY (song_id, artist_id),
  FOREIGN KEY (song_id) REFERENCES songs(song_id),
  FOREIGN KEY (artist_id) REFERENCES artists(artist_id)
);

-- for multiple artists per concert
CREATE TABLE concert_artists (
  concert_id INTEGER(10),
  artist_id INTEGER(10),
  PRIMARY KEY (concert_id, artist_id),
  FOREIGN KEY (concert_id) REFERENCES concerts(concert_id),
  FOREIGN KEY (artist_id) REFERENCES artists(artist_id)
);

-- for multiple favorite artists per fan
CREATE TABLE fan_favorite_artists (
  fan_id INTEGER(10),
  artist_id INTEGER(10),
  PRIMARY KEY (fan_id, artist_id),
  FOREIGN KEY (fan_id) REFERENCES concert_tickets(fan_id),
  FOREIGN KEY (artist_id) REFERENCES artists(artist_id)
);

-- for multiple fans per ticket_id
-- Create fan table
CREATE TABLE fans (
  fan_id INTEGER(10) PRIMARY KEY,
  fan_name VARCHAR(128),
  fan_email VARCHAR(128),
  age TINYINT(3)
);
-- make fans and tickets many to many
CREATE TABLE ticket_fans (
  ticket_id INTEGER(10),
  fan_id INTEGER(10),
  PRIMARY KEY (ticket_id, fan_id),
  FOREIGN KEY (ticket_id) REFERENCES concert_tickets(ticket_id),
  FOREIGN KEY (fan_id) REFERENCES fans(fan_id)
);
-- make per ticket_id to many fans
CREATE TABLE concert_tickets (
  ticket_id INTEGER(10) PRIMARY KEY,
  concert_id INTEGER(10),
  purchase_date DATE,
  ticket_price DOUBLE,
  seat_zone  VARCHAR(16),
  seat_number VARCHAR(16),
  FOREIGN KEY (concert_id) REFERENCES concerts(concert_id)
);
```

# data.sql

```sql

-- Insert data into artists table
INSERT INTO artists (artist_id, artist_name, genre, debut_year) VALUES
(1001, 'Taylor Swift', 'Pop', 2006),
(1002, 'Ed Sheeran', 'Pop', 2011);

-- Insert data into albums table
INSERT INTO albums (album_id, artist_id, album_title, release_date) VALUES
(2001, 1001, '1989', '2014-10-27'),
(2002, 1002, 'Divide', '2017-03-03');

-- Insert data into songs table
INSERT INTO songs (song_id, album_id, song_title, length, release_date) VALUES
(3001, 2001, 'Shake It Off', 3.39, '2014-08-18'),
(3002, 2001, 'Blank Space', 3.51, '2014-11-10'),
(3003, 2002, 'Shape of You', 3.54, '2017-01-06'),
(3004, 2002, 'Perfect', 4.23, '2017-03-03');

-- Insert data into concerts table
INSERT INTO concerts (concert_id, artist_id, concert_title, location, date_of_concert) VALUES
(4001, 1001, 'Reputation Stadium Tour', 'Atlanta', '2018-08-10'),
(4002, 1002, 'Divide World Tour', 'New York', '2018-09-05');

-- Insert data into concert_songs table
INSERT INTO concert_songs (concert_id, song_id, order_performance) VALUES
(4001, 3001, 1),
(4001, 3002, 2),
(4002, 3003, 1),
(4002, 3004, 2);

-- Insert data into fans table
INSERT INTO fans (fan_id, fan_name, fan_email, age) VALUES
(5001, 'Alice Johnson', 'alice.johnson@example.com', 25),
(5002, 'Bob Smith', 'bob.smith@example.com', 30);

-- Insert data into concert_tickets table
INSERT INTO concert_tickets (ticket_id, concert_id, purchase_date, ticket_price, seat_zone, seat_number) VALUES
(60001, 4001, '2018-07-01', 150.00, 'A', '12'),
(60002, 4002, '2018-08-20', 120.00, 'B', '8');

-- Insert data into ticket_fans table to reflect multiple fans per ticket
INSERT INTO ticket_fans (ticket_id, fan_id) VALUES
(60001, 5001),
(60001, 5002),
(60002, 5002);

-- Insert data into album_artists table for multiple artists per album
INSERT INTO album_artists (album_id, artist_id) VALUES
(2001, 1001),
(2002, 1002);

-- Insert data into song_artists table for multiple artists per song
INSERT INTO song_artists (song_id, artist_id) VALUES
(3001, 1001),
(3003, 1002);

-- Insert data into concert_artists table for multiple artists per concert
INSERT INTO concert_artists (concert_id, artist_id) VALUES
(4001, 1001),
(4002, 1002);

-- Insert data into fan_favorite_artists table for multiple favorite artists per fan
INSERT INTO fan_favorite_artists (fan_id, artist_id) VALUES
(5001, 1001),
(5001, 1002),
(5002, 1002);
```
