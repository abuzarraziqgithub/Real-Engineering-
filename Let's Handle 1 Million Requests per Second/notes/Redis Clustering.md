with `redis.sh` script we can easily run many clusters of redis(redis standalone could handle ~100k requests per second), it is going to setup 30 clusters of redis(on the creator machine).
- A single redis instance is single threaded so it's not gonna be really able to scale that much. 

Redis with cluster mode can handle million requests per second without costing us millions of dollars

redis cluster + pm2 cpu full utilization + autocannon 


![[Pasted image 20260928060403.png]]
And that's how we achieved 1 million requests(reads and writes) and that's so exciting ( :

**BUT**
If we are getting a million request per second and we are saving it all to our memory we gotta quickly free it up(e.g, batching to postgres or write them to disk or something) and then handle it again(the speed of writing or reading requests to the redis is blazing fast, it took about an 1 hour just to write into postgres but redis is amazing)

- we created another route `/code-ultra-fast`, generated a 122 bit random UUID
- with redis we kinda match that after hashing it to a proper number to match with the id in the memory data and then return that data of that id


We can now see how intense it is to do one million requests per second and it's a no joke, a simple mistake here could be absolutely costly(like 10s of thousands of dollars).
we saw there with that SQL code that if we were go with version 1(v1) and we were under the impression that we need just to scale up the database instead of trying to speed up the code that's would've been a disaster 

It happens countless times in production that people don't try to worry about increasing the speed of the code and they would just try to do horizontal scaling or something like that. 