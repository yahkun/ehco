# ehco

ehco is a network relay tool and a typo :)

## 主要功能

* tcp/udp relay
* tcp/udp relay over wss
* 从配置文件启动
* 从远程启动
* benchmark


## TODO

* 热重载配置


## BenchMark

iperf:


```sh
# run iperf server on 5201
iperf3 -s

# run relay server listen 1234 to 9001 (raw)
go run cmd/main.go -l 0.0.0.0:1234 -r 0.0.0.0:5201

# listen 1234 relay over wss to 1236
go run cmd/main.go -l 0.0.0.0:1234  -r wss://0.0.0.0:1236 -tt wss

# listen 1236 through wss relay to 5201
go run cmd/main.go -l 0.0.0.0:1236 -lt wss -r 0.0.0.0:5201

# benchmark tcp
iperf3 -c 0.0.0.0 -p 1234

# benchmark upd
iperf3 -c 0.0.0.0 -p 1234 -u -b 1G --length 1024

```

| iperf | raw | relay(raw) | relay(wss) |
| ---- | ----  | ---- | ---- |
| tcp  | 62.6 Gbits/sec | 23.9 Gbits/sec | 2.77 Gbits/sec |
| udp  | 2.2 Gbits/sec | 2.2 Gbits/sec | xx  |
