![[Pasted image 20260923032514.png|309]]
`
`-c 6 -p 2 -w 2 `
- -c 6 connections: we are going to open up 6 connections to the server  
- -p 2 pipe-lining: How many requests we are going to send immediately at the same time  
- -w 2 worker: we are going to spawn 2 threads(we can do 2 things at the same time on our CPU) 
- -d (duration)
- -m (http method)
If you wanna know at any given microsecond(point of time) how many requests a server is handling you have to multiply -c with -p cxp, this means when we run autocannon, the server at any given point of time is handling 12 concurrent requests 
