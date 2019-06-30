## 로컬에서 Kafka 실행해보기 

### 기본 환경

- python 2.7

- pip



### Ansible을 이용한 kafka Setting

python version 확인.

```bash
python --version
Python 2.7.10
```



pip version 확인.

```bash
pip --version
pip 18.1 from /Library/Python/2.7/site-packages/pip-18.1-py2.7.egg/pip (python 2.7)
```



만약 pip가 Python 3.6을 사용할 경우, pip를 재설치.

 distribute_setup.py를 curl을 이용해서 다운 받은 후, 해당 파일을 실행. 

실행 후에는 필요없으므로 지워준다.

pip easy_install을 수행.

```
pip 19.1.1 from /Users/minkyojung/Library/Python/3.6/lib/python/site-packages/pip (python 3.6)

# 재설치
curl -O http://python-distribute.org/distribute_setup.py
sudo python distribute_setup.py
sudo rm distribute_setup.py
sudo easy_install pip
```



정상적으로 수행이 된 경우,

```bash
pip2 --version
pip 18.1 from /Library/Python/2.7/site-packages/pip-18.1-py2.7.egg/pip (python 2.7)
```

위와 같이 나오게 된다.



pip로 docker, ansible 등 필요한 것들을 다운 받도록 한다.

```bash
sudo -H pip2 install docker==2.2.1 ansible==2.5.2 jinja2==2.9.6 httplib2==0.9.2 requests==2.10.0
```



위와 같은 문제가 생기지 않는 경우, 

```bash
sudo easy_install pip
sudo -H pip install docker==2.2.1 ansible==2.5.2 jinja2==2.9.6  httplib2==0.9.2 requests==2.10.0
```

명령어를 수행 하면 된다.



Ip alias 추가. alias 하는 이유는

- linux에서는 docker ethernet의 ip가 172.17.0.1
- mac에서는 **light한 vm에 docker가 구동되는 방식**이기 때문에 **172.17.0.1 ip의 docker ethernet으로 접근이 불가능함**
- `lo0`에 `172.17.0.1/24` 대역 ip들을 바인딩 시켜서 `172.17.0.1/24`로 요청하는 패킷들을 localhost로 향하게함
- 즉 `127.0.0.1` == `172.17.0.1`로 만드는 것
- docker 컨테이너에서 host로 포트포워딩을 해놨다면, `172.17.0.1/24`로의 요청들이 docker 컨테이너로 향하게됨

```bash
sudo ifconfig lo0 alias 172.17.0.1/24  
```

```bash
$ ifconfig
lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
	options=1203<RXCSUM,TXCSUM,TXSTATUS,SW_TIMESTAMP>
	inet 127.0.0.1 netmask 0xff000000
	inet6 ::1 prefixlen 128
	inet6 fe80::1%lo0 prefixlen 64 scopeid 0x1
	inet 172.17.0.1 netmask 0xffffff00 # 127.0.0.1과 같음
	nd6 options=201<PERFORMNUD,DAD>
```





ansible script 수행.

```bash
ansible-playbook -i environments/local/hosts setup.yml
ansible-playbook -i environments/local kafka.yml -e mode=deploy
```



수행 중, **Failed to import docker-py** 에러가 발생시,

```bash
mkdir -p ~/Library/Python/2.7/lib/python/site-packages
echo '/usr/local/lib/python2.7/site-packages' > ~/Library/Python/2.7/lib/python/site-packages/homebrew.pth
```

해당 부분 수행.



모든 과정이 끝나면, 

```
docker ps
CONTAINER ID        IMAGE                           COMMAND                  CREATED              STATUS              PORTS                                                                    NAMES
f2b90f4d308f        wurstmeister/kafka:2.12-2.2.1   "start-kafka.sh"         18 seconds ago       Up 16 seconds       0.0.0.0:9072->9072/tcp, 0.0.0.0:9093->9093/tcp                           kafka0
1e93254204b8        zookeeper:3.4                   "/docker-entrypoint.…"   About a minute ago   Up About a minute   0.0.0.0:2181->2181/tcp, 0.0.0.0:2888->2888/tcp, 0.0.0.0:3888->3888/tcp   zookeeper0
```

이런 식으로 kafka와 zookeeper가 생성된다.



##### kafka TEST

https://kafka.apache.org/quickstart에 접속해서, kafka version 2.12-2.2.1 binary파일을 다운로드 후,

bin 폴더 아래에서 다음 명령어를 수행.



##### topic 생성

Kafka topic을 testTopic이름으로 생성.

```bash
cd kafka_2.12-2.2.0/bin
./kafka-topics.sh --bootstrap-server 172.17.0.1:9093 --topic testTopic --create --partitions 1 --replication-factor 1
```



##### producer test

 producer test script 수행.

```bash
./kafka-producer-perf-test.sh --topic testTopic --throughput 500--record-size 2000 --num-records 200000 --producer-props bootstrap.servers=172.17.0.1:9093

2502 records sent, 500.3 records/sec (0.95 MB/sec), 7.1 ms avg latency, 247.0 ms max latency.
2510 records sent, 501.8 records/sec (0.96 MB/sec), 1.6 ms avg latency, 21.0 ms max latency.
2501 records sent, 500.2 records/sec (0.95 MB/sec), 3.1 ms avg latency, 100.0 ms max latency.
2501 records sent, 500.2 records/sec (0.95 MB/sec), 1.4 ms avg latency, 12.0 ms max latency.
2500 records sent, 500.0 records/sec (0.95 MB/sec), 3.9 ms avg latency, 105.0 ms max latency.
2501 records sent, 500.2 records/sec (0.95 MB/sec), 2.0 ms avg latency, 29.0 ms max latency.
2501 records sent, 500.1 records/sec (0.95 MB/sec), 1.6 ms avg latency, 32.0 ms max latency.
```

위와 같이 나오면 정상적으로 수행이 된 것.



##### consumer test

```bash
./kafka-consumer-perf-test.sh --broker-list 172.17.0.1:9093 --topic testTopic --messages 20000
```

해당 명령어 수행시, 에러가 아닌 로그가 출력되면 정상적으로 테스트 된 것.





