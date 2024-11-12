# SQL
```sql
-- Table for Artists
CREATE TABLE artists (
    artist_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);

-- Table for Albums
CREATE TABLE albums (
    album_id INT PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    release_date DATE,
    artist_id INT NOT NULL,
    FOREIGN KEY (artist_id) REFERENCES artists(artist_id) ON DELETE CASCADE
);

-- Table for Songs
CREATE TABLE songs (
    song_id INT PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    duration TIME,
    album_id INT NOT NULL,
    artist_id INT NOT NULL,
    FOREIGN KEY (album_id) REFERENCES albums(album_id) ON DELETE CASCADE,
    FOREIGN KEY (artist_id) REFERENCES artists(artist_id) ON DELETE CASCADE
);

-- Table for Concerts
CREATE TABLE concerts (
    concert_id INT PRIMARY KEY,
    concert_date DATE NOT NULL,
    location VARCHAR(100) NOT NULL,
    artist_id INT NOT NULL,
    FOREIGN KEY (artist_id) REFERENCES artists(artist_id) ON DELETE CASCADE
);

-- Table for Fans
CREATE TABLE fans (
    fan_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);

-- Table for Tickets (now containing fan_id to create one-to-many relationship)
CREATE TABLE tickets (
    ticket_id INT PRIMARY KEY,
    concert_id INT NOT NULL,
    fan_id INT NOT NULL,
    FOREIGN KEY (concert_id) REFERENCES concerts(concert_id) ON DELETE CASCADE,
    FOREIGN KEY (fan_id) REFERENCES fans(fan_id) ON DELETE CASCADE
);

-- Table for Favorite Artists per Fan (allowing multiple favorite artists per fan)
CREATE TABLE fan_fav_artist (
    fan_id INT,
    artist_id INT,
    PRIMARY KEY (fan_id, artist_id),
    FOREIGN KEY (fan_id) REFERENCES fans(fan_id) ON DELETE CASCADE,
    FOREIGN KEY (artist_id) REFERENCES artists(artist_id) ON DELETE CASCADE
);
```
