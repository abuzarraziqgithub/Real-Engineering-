We modified and scaled the database instance to reach to the point of handling 1 million requests per second and also got our db crashed at one point when writing to it with huge amount of data and even reading the data, the reason for reading that data that took so much time because of the use of RANDOM method in our SQL that scan the entire 10 million records just to give us one which was definitely insane, we changed that and moved to V2 where we generated randomID from one to that counted records from the database but still not achieved our results because we were still doing Big O(n) operation by scanning all the records in order to count but then we got to v3 but even still not achieved that milestone.

## **BUT WE STILL HAVE HOPE** :
 The solution that won't cost us a massive amount of money **and this is where Redis comes into play** 

We should know that the Read and Write speed of our memory is about ~6 - 10x faster than our disk and in Postgres whenever you do a Write or Read you're reaching to your Hard Drive, the data is setting on our hard-drive and our hard-drive could be the fastest possible ssd and its still not gonna cut it **and the Access Time of Ram is usually ~1000 Times faster than disk** 

***What usually happens in these companies that handle such a massive amount of traffic is that they use Redis which is an in-memory database storage and it's a very easy one to deal with.***

So now moving from the Postgres routes to the new one that would do the exact same operation that we would do in post routes code but it will write it to the Redis instead of Postgres

If we're saving them to memory, then we're losing out on all the cool operations that we can do in SQL(all the joins, looking for all of our data in very clean ways) and we can't do that with Redis
**BUT**
We are saving the id's to a queue `sync_queue` and then the sync(a file script) would read from that queue in our memory(because it sits inside our memory) and gradually writing them to the database and we can do this operation overnight maybe it would take a couple of hours but we actually don't care.... This is a real world thing this is what Uber and some of these companies with such insane amount of traffic do **for example if you were getting a lots of locations from your drivers and you wanna keep track of all the locations then you're probably hitting that route millions of times per second, It'd be crazy to try to save all of them to disk-based SQL database(Some SQL databases can be, and are designed to be run in memory, like SAP  HANA and SQLite).** 
what you wanna do is to do just like what we have there(Redis) and its save them to your memory probably by using Redis or another memory storage and then sync in a background process 

You might also be wondering what about all the data that we've got in our database?(we got 11 million records in our database which is ~16GB of data) now what if we move the whole thing into our memory? can't we do that? (The creator has an instance machine that has ~247 GB of memory) so he could move the complete database from the disk over to the memory and only read from that or write to that and that would way faster and cheaper compared to the other solution of trying to scale up our database   
so `migrate.js` migrate the data from Postgres(disk) to Redis(memory) in batches.

With writing to postgres we could only handle 40 to 50,000 requests per second but trying it with Redis and we got around ~150k which at least 3x more than the postgres write, so if the cost was 30 grand a month now with this we can cut it down to 10 grand a month. If we keep saving like this and then we migrate the data  over(but still not million) and **the reason we're still not at a million even though we're just in our memory and we have a huge amount of idle cpu is because a single Redis instance is limited to only about 100k requests(reads and writes) per second, we got to scale up, we need to run more instances of redis  to be able to handle more than 100k( A single Redis instance is not going to cut it here for us)** 

You can move your complete Postgres or MySQL database in your memory if you have enough ram 

We should know the importance of Redis that how much it could save us money for a heavy route. It could be a gamechanger that now instead of having to drop thousands and probably millions of dollars on our storagebased database, with this we can cut that down to something that's a fraction of that and we can easily migrate and we could only migrate what we know is going to hit quite a lot.

