[[Cryptocurrency]] [[Bitcoin]]

# Setting up
The miner requires a pool, we could use a public pool but this is risky according to some blog posts, so we are going to create our own. 

some dependencies 

`sudo apt update
`sudo apt install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils git screen yasm libzmq3-dev`
`
and also installing [monit](https://mmonit.com/monit/documentation/monit.html) for monitoring 

## monit config file
we are telling monit what to track 
```
nano bitcoin-pool

check process bitcoind with pidfile /var/run/bitcoind.pid
   start program = "/app/bitcoin/service.sh start"
   stop  program = "/app/bitcoin/service.sh stop"

check process ckpool with pidfile /tmp/ckpool/main.pid
   start program = "/app/ckpool/service.sh start"
   stop  program = "/app/ckpool/service.sh stop"

# check that network is always reachable
check host internet with address 1.1.1.1
    if failed ping 3 times within 30 cycles then exec "/usr/sbin/reboot"

# optional; only if you want to mine with your raspberry as well
check process cpuminer with pidfile /var/run/cpuminer.pid
   start program = "/app/cpuminer-multi/service.sh start"
   stop  program = "/app/cpuminer-multi/service.sh stop"
```


## Creating a pool

monitoring process of sync 
`bitcoin-cli -conf=/etc/bitcoin.conf getblockchaininf`



---
### Sources
https://blog.veeso.dev/blog/en/how-to-setup-a-bitcoin-solo-mining-pool/