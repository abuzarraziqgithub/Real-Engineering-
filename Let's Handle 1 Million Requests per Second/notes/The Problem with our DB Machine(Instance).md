The IOPS(Input-Output-Per-Second) is only 3000 but we wanna trying a million times so this should be way higher than this but it would too much costly so what's the solution then?(but cododev modified the instance by increasing the storage to 500GB and 12000IOPS) and with that we actually got a little higher average of writing to the database with -c 300 -p 100 --workers 120.
![[Pasted image 20260927004109.png]]
![[Pasted image 20260927004057.png]]

So with this modification we still got only ~66k that is way lower than 1 million and also the cost is so high
![[Pasted image 20260927004301.png]]

So what to do instead?

**Let's explain the solution** : what you gotta do instead is to save the data(into c8i.32xlarge instance[power server]) and  through batch processing save that data to the database over time and that's a much much more cost effective way than that

Database scaling is a massive thing, we can surely keep on adding more databases adding more powerful dbs but our cost is going to skyrocket 

- If you're handling a million requests per second you at least have 10 million records in your database(at least)

**The Interesting part** :
- The creator actually wrote 10 million data into the database using seed -r(with r flag) 
- But when we start sending about a million requests/second the db got crashed
- The reason for a single request taking so much time is because of `ORDER BY RANDOM()` and this Big O(n) -- Full Table Scan
  meaning it scans the whole database with this RANDOM and just pick one and when you have 10 million records this is not going to work and it would take to eternity 
- Instead in ***V2*** route we first counted the data and generated random id between 1 and count and fetch the record with that id **But that also didn't work because SELECT COUNT(x(asterik))  is also O(n), the db has to scan to see how many record we have got**

- In ***V3*** where we are getting our maxId(so we are ordering by id) and we are generating an id that's between 1 and maxId and this isn't actually Big O(n) and fortunately it did work but we got an average about ~206k with 4158k request sent in 20s with ~3GB read but we are still so far away from getting into a million/second, so if we can increase our performance maybe 5x we should be able to technically hit a million per second  
- **V4** :![[Pasted image 20260927014058.png]]
  but it also never crossed the line


![[Pasted image 20260927032328.png]]
we could go upto 1 million with this but only with read and not actually write that gonna cost us more