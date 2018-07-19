# EOS-Sync

Quickly set up the EOS main network data synchronization to the mongodb database, operating steps:

[点击查看中文](README_CN.md)

## Install Dependencies

- [Docker](https://docs.docker.com) Docker 17.05 or higher is required
- [docker-compose](https://docs.docker.com/compose/) version >= 1.10.0

## Clone project

```
git clone git@github.com:EOSpace/eos-sync.git
cd eos-sync
```

## Setup in 5 seconds using the shell

```
./run.sh
```

## Setup manually in 1 minute

The first step, create the desired directory:

```
mkdir -p /data/eos/nodeos-data-volume/nodeos-data-mainnet/mongo
mkdir -p /data/eos/nodeos-data-volume/nodeos-data-mainnet/data
```

The second step is to prepare the configuration file:

```
cp -r config /data/eos/nodeos-data-volume/nodeos-data-mainnet
```

The third step, start synchronizing data:

```
docker-compose -f docker-compose-mainnet-init.yaml up -d
```

## View synchronized data

Enter mongo to view synchronized data:

```
docker-compose -f docker-compose-mainnet-init.yaml exec mongo /bin/bash
mongo admin -u root -p 111222
```

The synchronization result is as follows:

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

## Stop/Restart/Replay syncing

To stop the syncing process:

```
docker-compose -f docker-compose-mainnet.yaml down
```

To restart the syncing process:

```
docker-compose -f docker-compose-mainnet.yaml down
docker-compose -f docker-compose-mainnet.yaml up -d
```

To replay the blockchain:

```
docker-compose -f docker-compose-mainnet-replay.yaml down
docker-compose -f docker-compose-mainnet-replay.yaml up -d
```
