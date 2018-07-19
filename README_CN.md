# EOS-Sync

快速搭建将EOS主网数据同步至mongodb数据库, 操作步骤:

[View in English](README.md)

## 安装docker

- [Docker](https://docs.docker.com) Docker版本 >= 17.05
- [docker-compose](https://docs.docker.com/compose/) 版本 >= 1.10.0

## 克隆项目

```
git clone git@github.com:EOSpace/eos-sync.git
cd eos-sync
```

## 5秒脚本搭建方法

```
./run.sh
```

## 1分钟手工搭建方法

第一步，创建所需目录:

```
mkdir -p /data/eos/nodeos-data-volume/nodeos-data-mainnet/mongo
mkdir -p /data/eos/nodeos-data-volume/nodeos-data-mainnet/data
```

第二步，准备配置文件:

```
cp -r config /data/eos/nodeos-data-volume/nodeos-data-mainnet
```

第三步，开始同步数据:

```
docker-compose -f docker-compose-mainnet-init.yaml up -d
```

## 查看同步的数据

进入mongo查看同步的数据:

```
docker-compose -f docker-compose-mainnet-init.yaml exec mongo /bin/bash
mongo admin -u root -p 111222
```

同步结果如下:

```
> use EOS;
switched to db EOS
> show tables;
accounts
actions
block_states
blocks
transaction_traces
transactions
```

## 停止/重启 同步

停止数据同步:

```
docker-compose -f docker-compose-mainnet.yaml down
```

重启数据同步:

```
docker-compose -f docker-compose-mainnet.yaml down
docker-compose -f docker-compose-mainnet.yaml up -d
```

Replay区块:

```
docker-compose -f docker-compose-mainnet-replay.yaml down
docker-compose -f docker-compose-mainnet-replay.yaml up -d
```
