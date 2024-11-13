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
