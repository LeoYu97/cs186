**CS186 Week 3 Discussion Worksheet**
***SQL Joins***

Songs (song_id,  song_name,  album_num, weeks_in_top_40)Artists(artist_id, artist_name, first_year_active)Albums (album_id, album_name, artist_num, year_released, genre)
**Write SQL expressions for the following queries:**
**1.**	**The name of all songs with the genre “country” which have spent more than 2 weeks in the top 40.**

select s.song_name from Songs s, Albums a

where s.album_num = a.album_id and a.genre == "country" and s.weeks_in_top_40 >2;



**2.**	**For each song, its name, the name of its album, and the name of its artist.**

select s.song_name, al.album_name, ar.artist_name from Song s, Albums al, Artists ar

where  s.album_num = al.album_id and al.artist_num = ar.artist_id;



**3.**	**The number of albums released by each artist.**

select ar.artist_name, count(1) from Artists ar, Albums al

where ar.artists_id = al.artist_num 

group by ar.artist_id

***Join Algorithms***

**4.**	**So far in class, we’ve studied the chunk nested loops, hash, and sort-merge joins. Give a scenario in which a:**
	**Chunk-nested loops join is the best.**

​	When not use an equality predicate.

​         

​	**Sort-merge join is the best.**

​    Small memory size

​    When you want sorted output/have sorted input

​    

​    **Hash-join is the best**

​	small table will be in memory.

​	cost of 2-pass hash join:

   $cost =3( [R] + [S]) + [output]$

**5.**	**We have 12 pages of memory, and we want to join two tables [R] and [S] where [R] is 100 pages and [S] is 50 pages.** 
	**How many disk reads are needed to perform Chunk Nested Loops Join?**

$[R] + ([R]/(12 - 2))\cdot[S] = 50 + 5 * 100 = 550$



​	**How about a Hash Join? (Assume no recursive partitioning)**

$([R] + [S])\cdot(1 + 1) = 300$



***Heap Files***

**6.**	**What are the advantages and disadvantages of using slotted pages or bitmaps over just tightly packing records together?**

allow movement of records without changing record ID



This method is inefficient for large databases.



**7.**	**You have a slotted page with 80 bytes of free space, and it costs 4 bytes to store a directory entry.** 

**What’s the size of the largest record you can insert?**

80 - 4 = 76 bytes



**At most, how many 1-byte large records can you insert?**

space = 1 + 4 = 5 bytes

80 / 5 = 16 records