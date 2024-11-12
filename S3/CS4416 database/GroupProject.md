# SQL CREATE TABLE
```sql
-- 创建艺术家表
CREATE TABLE artists (
    artist_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);

-- 创建歌曲表
CREATE TABLE songs (
    song_id INT PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    release_date DATE
);

-- 创建专辑表
CREATE TABLE albums (
    album_id INT PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    release_date DATE
);

-- 创建演唱会表
CREATE TABLE concerts (
    concert_id INT PRIMARY KEY,
    concert_date DATE NOT NULL,
    location VARCHAR(100) NOT NULL
);

-- 创建粉丝表
CREATE TABLE fans (
    fan_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);

-- 创建门票表
CREATE TABLE tickets (
    ticket_id INT PRIMARY KEY,
    concert_id INT,
    FOREIGN KEY (concert_id) REFERENCES concerts(concert_id)
);

-- 创建艺术家-专辑关联表，以支持多位艺术家参与同一专辑
CREATE TABLE artist_album (
    artist_id INT,
    album_id INT,
    PRIMARY KEY (artist_id, album_id),
    FOREIGN KEY (artist_id) REFERENCES artists(artist_id),
    FOREIGN KEY (album_id) REFERENCES albums(album_id)
);

-- 创建艺术家-歌曲关联表，以支持多位艺术家参与同一歌曲
CREATE TABLE artist_song (
    artist_id INT,
    song_id INT,
    PRIMARY KEY (artist_id, song_id),
    FOREIGN KEY (artist_id) REFERENCES artists(artist_id),
    FOREIGN KEY (song_id) REFERENCES songs(song_id)
);

-- 创建艺术家-演唱会关联表，以支持多位艺术家参与同一演唱会
CREATE TABLE artist_concert (
    artist_id INT,
    concert_id INT,
    PRIMARY KEY (artist_id, concert_id),
    FOREIGN KEY (artist_id) REFERENCES artists(artist_id),
    FOREIGN KEY (concert_id) REFERENCES concerts(concert_id)
);

-- 创建粉丝-最喜欢的艺术家关联表，以支持每个粉丝有多个最喜欢的艺术家
CREATE TABLE fan_favorite_artist (
    fan_id INT,
    artist_id INT,
    PRIMARY KEY (fan_id, artist_id),
    FOREIGN KEY (fan_id) REFERENCES fans(fan_id),
    FOREIGN KEY (artist_id) REFERENCES artists(artist_id)
);

-- 创建门票-粉丝关联表，以支持每张票可以由多个粉丝共享
CREATE TABLE fan_ticket (
    fan_id INT,
    ticket_id INT,
    PRIMARY KEY (fan_id, ticket_id),
    FOREIGN KEY (fan_id) REFERENCES fans(fan_id),
    FOREIGN KEY (ticket_id) REFERENCES tickets(ticket_id)
);

-- 创建专辑-歌曲关联表，以支持相同版本的歌曲可以出现在多个专辑中
CREATE TABLE album_song (
    album_id INT,
    song_id INT,
    PRIMARY KEY (album_id, song_id),
    FOREIGN KEY (album_id) REFERENCES albums(album_id),
    FOREIGN KEY (song_id) REFERENCES songs(song_id)
);
```

# INSERT
```sql
-- 插入艺术家数据
INSERT INTO artists (artist_id, name) VALUES (1, 'Artist A');
INSERT INTO artists (artist_id, name) VALUES (2, 'Artist B');

-- 插入歌曲数据
INSERT INTO songs (song_id, title, release_date) VALUES (1, 'Song X', '2023-01-15');
INSERT INTO songs (song_id, title, release_date) VALUES (2, 'Song Y', '2023-02-20');

-- 插入专辑数据
INSERT INTO albums (album_id, title, release_date) VALUES (1, 'Album Alpha', '2023-03-10');
INSERT INTO albums (album_id, title, release_date) VALUES (2, 'Album Beta', '2023-04-05');

-- 插入演唱会数据
INSERT INTO concerts (concert_id, concert_date, location) VALUES (1, '2023-05-12', 'Stadium X');
INSERT INTO concerts (concert_id, concert_date, location) VALUES (2, '2023-06-18', 'Arena Y');

-- 插入粉丝数据
INSERT INTO fans (fan_id, name) VALUES (1, 'Fan John');
INSERT INTO fans (fan_id, name) VALUES (2, 'Fan Alice');

-- 插入门票数据
INSERT INTO tickets (ticket_id, concert_id) VALUES (1, 1);
INSERT INTO tickets (ticket_id, concert_id) VALUES (2, 2);

-- 插入艺术家-专辑关联数据（支持一个专辑包含多个艺术家）
INSERT INTO artist_album (artist_id, album_id) VALUES (1, 1);
INSERT INTO artist_album (artist_id, album_id) VALUES (2, 1);
INSERT INTO artist_album (artist_id, album_id) VALUES (1, 2);

-- 插入艺术家-歌曲关联数据（支持一个歌曲包含多个艺术家）
INSERT INTO artist_song (artist_id, song_id) VALUES (1, 1);
INSERT INTO artist_song (artist_id, song_id) VALUES (2, 1);
INSERT INTO artist_song (artist_id, song_id) VALUES (2, 2);

-- 插入艺术家-演唱会关联数据（支持一个演唱会包含多个艺术家）
INSERT INTO artist_concert (artist_id, concert_id) VALUES (1, 1);
INSERT INTO artist_concert (artist_id, concert_id) VALUES (2, 1);
INSERT INTO artist_concert (artist_id, concert_id) VALUES (1, 2);

-- 插入粉丝-最喜欢的艺术家关联数据（支持每个粉丝有多个最喜欢的艺术家）
INSERT INTO fan_favorite_artist (fan_id, artist_id) VALUES (1, 1);
INSERT INTO fan_favorite_artist (fan_id, artist_id) VALUES (1, 2);
INSERT INTO fan_favorite_artist (fan_id, artist_id) VALUES (2, 1);

-- 插入门票-粉丝关联数据（支持多位粉丝共享同一张票）
INSERT INTO fan_ticket (fan_id, ticket_id) VALUES (1, 1);
INSERT INTO fan_ticket (fan_id, ticket_id) VALUES (2, 1);
INSERT INTO fan_ticket (fan_id, ticket_id) VALUES (2, 2);

-- 插入专辑-歌曲关联数据（支持相同的歌曲出现在多个专辑中）
INSERT INTO album_song (album_id, song_id) VALUES (1, 1);
INSERT INTO album_song (album_id, song_id) VALUES (1, 2);
INSERT INTO album_song (album_id, song_id) VALUES (2, 1);
```

# EDR

<img width="1118" alt="image" src="https://github.com/user-attachments/assets/c119d9ed-009b-4ded-9223-ab9cf3d92b7b">

