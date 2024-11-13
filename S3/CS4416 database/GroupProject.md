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
CREATE TABLE ticket_fans (
  ticket_id INTEGER(10),
  fan_id INTEGER(10),
  PRIMARY KEY (ticket_id, fan_id),
  FOREIGN KEY (ticket_id) REFERENCES concert_tickets(ticket_id),
  FOREIGN KEY (fan_id) REFERENCES concert_tickets(fan_id)
);

```
