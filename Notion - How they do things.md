2025-04-15
Tags: [[Programming]] [[Business]]

Notion is an online software, this is a good and bad thing. 

Every page has blocks, each block has its own unique id that reference the block it belongs to
- Stored in Json

2021 -> They used a single [[Postgres db]]

[[Sharding]] After things got out of control with the Postgres db, they needed a solution. Usually you can buff a computer so that it can handle the load. But with Sharding, you have multiple computers attacking the same problem. 
- Similar to clusters
- Sharding based on blocks

[[Data Lake]] -> Centralized repository for a huge amount of data. Developers use this to dump a bunch of data that they want to use later.
You can dump any type of data. 
- Much cheaper as well 

Notion was doubling number of blocks being created every 6 to 12 months. The system being used was an issue. Also, as mentioned on the video, think about how you use text files, you write something, then you fix it, they you write again and you might delete. These are thousands of updates to the data blocks per second. A data lake like snowflake is good at handling new rows, but not updating existing rows. 

After this, Notion decided to create their own data lake capabale of handling updates to existing rows.

The pipeline looks like this:
![[Pasted image 20250415100813.png]]

Most of this is open sourced.

Postgres is the goat here. They also used Pgbouncer to distribute data accordingly between shards. 










---
### Reference

[Video](https://www.youtube.com/watch?v=NwZ26lxl8wU)