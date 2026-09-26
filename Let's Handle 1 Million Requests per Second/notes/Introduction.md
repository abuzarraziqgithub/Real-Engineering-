We will simulate being one of the busiest routes in the world and handle more than a million http requests per second 

- We are talking scale of Uber, Netflix and even parts of Apple and Google.
- AWS busiest service is the IAM( A security guard for all our application in AWS environment), this is the busiest site we got in the world.
- The same service(IAM) a few years ago handling 400 million requests per second (we don't have routes that handles trillions of requests and we don't have it right now but this is something humanity has accomplished)

- In this journey we are gonna see how close to this we can get by launching a powerful infrastructure with hundreds of CPU cores and dozens of computers that costs hundreds of thousands of dollars a year to run and simulate having millions and millions of users using service at the same time 
- We are gonna be on some insane scale moving terabytes and terabytes of data per minute. 

- You are gonna see that things are very different when you're in such an extreme environment. For example, you see a lot of people that say the database is always the main bottleneck but not here, you don't even want your database to be your main bottleneck because the costs are just going to be absolutely unbelievable.

- At this scale a simple mistake is absolutely detrimental.
- A simple mistake here would cost your company tens of thousands of dollars and a mistake here is not a bug. Having a bug is  Incomprehensible, you don't even want to go anywhere close to having a chance of having a bug.
- By mistake here mean going with a solution that is for example O(n) instead of O(log n), The concept of "code that just works is good enough" is ridiculous in such a high stake environment and that mentality could cost a company literally millions of dollars over very short period of time(so no room for error)
- You got to really think like an engineer in this environment.
- The mindset of I'm just a programmer or just a C or a Java developer is not gonna work here, you shouldn't shy away from math, something that has a probability of one over million to happen here has a chance of happening every minute. So thinking just like a programmer is not gonna work, You wont even survive more than a few minutes, but you'll learn, but also it's a lot of fun, scary but also thrilling, kind of like roller coaster type scary but with the difference that you can actually crash. 
- It takes a lot of engineering, a whole a lot of effort, and only very few companies in the world would ever get to this scale of 1 million requests per second.