Chose c8i.32xlarge with 128 CPU Cores, 256GB Memory(RAM) 50 Gb/s Network Performance (6.25 GB/s) cost 5000 usd/month

Cododev used one machine for just installing autocannon to generate traffic and one machine(the server) for handling heavy traffic

cododev started 128 instances(cluster) of node on the c8i.32xlarge using pm2 after ssh and that's crazy
## **Started our application(node) cluster using pm2** :
![[Pasted image 20260926030755.png]]

## **Copying the Public DNS address for ssh and sending requests**:  
![[Pasted image 20260926031011.png]]
![[Pasted image 20260926031107.png]]

## **Monitoring Power Server CPU Core Usage** 
![[Pasted image 20260926031549.png]]

## **Power Tester Usage**
![[Pasted image 20260926031641.png]]

## Handled ~6 million requests/second with 130218k requests in 20s
**But this is just a simple get request we wanna achieve this on patch or post**
![[Pasted image 20260926031707.png]]

## **Autocannon PATCH Request**:
![[Pasted image 20260926032006.png]]

## **It actually handled only ~173k requests/ the bottleneck was network speed but also we were generating/creating an array of length 100 and more and that generated a huge amount of data(30KB/request) across the network, we could reduce that array number but it's not the point, we can try that to achieve the 1 million milestone**:
![[Pasted image 20260926032112.png]]
- The reason we got handled ~173k requests is because if we divide 119GB by 20seconds we were actually moving across ~6GBs data per second and that is so huge and we also know that our machine(c8i) network speed was around 6.5 GBs so our main bottelneck was network speed not the cores and that's why it's not gonna allow us to accept more traffic

## **checking High speed network performance system**
![[Pasted image 20260926033056.png]]


![[Pasted image 20260926033228.png]]

![[Pasted image 20260926033309.png]]

## **The P5.48Xlarge actually cost ~30,000 usd each month
![[Pasted image 20260926033342.png]]

The point he is trying to make is if you wanna go this far and make sure you can make 1 million requests per second with this API then the cost is gonna be astronomical

## **Estimation if Open Weather API hit 1 million/second milestone**
```
 the creator calculates the theoretical cost of using the *OpenWeather* API by applying the following logic:
1. **Traffic Volume:** He assumes a rate of **1 million requests per second**.
2. **Timeframe:** He identifies that there are approximately **2.6 million seconds in a month**.
3. **Calculation:** By multiplying the 1 million requests per second by the total seconds in a month, he arrives at the massive scale of traffic. He then multiplies this by a hypothetical cost-per-request model typical of commercial APIs, ultimately projecting a theoretical monthly cost of roughly **$3.8 billion**.

He uses this example to illustrate the astronomical scale of handling 1 million requests per second and to emphasize why building custom, cost-effective infrastructure is essential for such high-traffic requirements compared to relying on standard third-party APIs.

AMAZON API GATEWAY:

The creator discusses *Amazon API Gateway* (or *IAM*, which acts as the security guard for services) early in the video to provide context on the scale of massive web infrastructure (0:23 - 0:43). 

He uses *Amazon's* service as a prime example of a "busiest route" in the world, noting that a few years ago, it was already handling **more than 400 million requests per second** globally. He brings this up to highlight that while his goal of **1 million requests per second** is an immense challenge for a single developer or small setup, it is a proven, achievable scale in the real world by major tech companies like *Amazon*, *Google*, and *Netflix*.
```

![[Pasted image 20260926035252.png]]