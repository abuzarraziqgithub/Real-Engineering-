## Core Utilization: Getting core utilization
 - A single core utilization formula: 
 - **Total Time  -(minus)  Total Idle Time / Total Time x 100**
 - Total Time (any span of time, e.g, the last 30 minutes)
 - Total Idle time (throughout that last 30 minutes, how long the core was absolutely doing nothing, so each core can either do something or not do anything, it would add 2 numbers or checking if something is true or some basic stuff)
For example the total idle time of a particular core was 30 minutes in the last 1 hour(total time), by that you get 50% (60 - 30 / 60 x 100), meaning that that core was utilized 50% of the time throughout the last 1 hour 
## CPU Utilization: Your CPU has got multiple cores
 - Take each core utilization and add them all up together or you can also divide it by total number pf cores (the division is optional, some systems do or not)
## Two different methods to display CPU utilization
![[Pasted image 20260922031254.png]]
