The IOPS(Input-Output-Per-Second) is only 3000 but we wanna trying a million times so this should be way higher than this but it would too much costly so what's the solution then?(but cododev modified the instance by increasing the storage to 500GB and 12000IOPS) and with that we actually got a little higher average of writing to the database with -c 300 -p 100 --workers 120.
![[Pasted image 20260927004109.png]]
![[Pasted image 20260927004057.png]]


![[Pasted image 20260927004301.png]]