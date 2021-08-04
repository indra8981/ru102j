# Idea for building a rate limiter using redis. Ex : Limiting user calls to 10 requests per min

    We can limit a user by using their ip address. For every 
    Ip address we will create a key and set it with expiration
    as 60 seconds and value 10. Then for every request we would
    decrease the value by 1 and if the value is less than 0
    we would throw an exception. 

For the 1st time this will be the commands
```
SETNX user_ip:PING limit_amount
EXPIRE user_ip:PING timeout
```

From the next requests
```
 GET user_ip:PING
 DECRBY user_ip:PING amount
```
