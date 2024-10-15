# Configuring Multiple Tendermint Nodes in Cosmos

Cosmos uses Tendermint as its consensus algorithm, which is resistant to malicious behavior. When running multiple Tendermint nodes, you may encounter port conflicts, causing the second and subsequent nodes to fail.

## Default Ports

By default, the following ports are used:
- 26656
- 26657
- 6060
- 26658
- 26660
- 9090
- 9091
- and others

It is not recommended to set up a large number of nodes on a single server—do so at your own risk!

### Configuration Files Overview

#### `config.toml`

```toml
proxy_app = "tcp://127.0.0.1:26658"
rpc laddr = "tcp://127.0.0.1:26657"
pprof_laddr = "localhost:6060"
p2p laddr = "tcp://0.0.0.0:26656"
prometheus_listen_addr = ":26660"
```

#### `app.toml`

```toml
api address = "tcp://0.0.0.0:1317"
grpc address = "0.0.0.0:9090"
grpc-web address = "0.0.0.0:9091"
```

#### `client.toml`

```toml
node = "tcp://localhost:26657"
```

For the second and subsequent nodes, these ports need to be changed to avoid conflicts. You can manually modify `$HOME/.defund/config/config.toml` or use the following commands:

## Setting Environment Variables

```bash
# Set working directory
work_dir=.cosmos
```

### `config.toml` Modifications

For each node, adjust the port settings as follows:

```bash
# for 2 node
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:36658\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:36657\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:6061\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:36656\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":36660\"%" $HOME/$work_dir/config/config.toml

# for 3 node
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:46658\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:46657\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:6062\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:46656\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":46660\"%" $HOME/$work_dir/config/config.toml

# for 4 node
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:56658\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:56657\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:6063\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:56656\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":56660\"%" $HOME/$work_dir/config/config.toml

# for 5 node
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:60558\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:60557\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:6064\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:60556\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":60560\"%" $HOME/$work_dir/config/config.toml

# for 6 node
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:60658\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:60657\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:6065\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:60656\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":60660\"%" $HOME/$work_dir/config/config.toml

# for 7 node
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:60758\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:60757\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:6066\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:60756\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":60760\"%" $HOME/$work_dir/config/config.toml

# for 8 node
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:60858\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:60857\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:6067\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:60856\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":60860\"%" $HOME/$work_dir/config/config.toml

# for 9 node
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:60958\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:60957\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:6068\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:60956\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":60960\"%" $HOME/$work_dir/config/config.toml

# for 10 node
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:61058\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:61057\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:6069\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:61056\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":61060\"%" $HOME/$work_dir/config/config.toml

# for 11 node
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:61158\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:61157\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:6070\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:61156\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":61160\"%" $HOME/$work_dir/config/config.toml

# for 12 node
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:61258\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:61257\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:6071\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:61256\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":61260\"%" $HOME/$work_dir/config/config.toml

# for 13 node
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:61358\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:61357\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:6072\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:61356\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":61360\"%" $HOME/$work_dir/config/config.toml

# for 14 node
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:61458\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:61457\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:6073\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:61456\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":61460\"%" $HOME/$work_dir/config/config.toml

# for 15 node
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:61558\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:61557\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:6074\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:61556\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":61560\"%" $HOME/$work_dir/config/config.toml
```

Repeat similar modifications for subsequent nodes, incrementing ports accordingly.

### `app.toml` Modifications

For each node, adjust the API and gRPC port settings as follows:


```bash
# for 2 node
sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:9190\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:9191\"%; s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:1327\"%" $HOME/$work_dir/config/app.toml

# for 3 node
sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:9290\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:9291\"%; s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:1337\"%" $HOME/$work_dir/config/app.toml

# for 4 node
sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:9390\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:9391\"%; s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:1347\"%" $HOME/$work_dir/config/app.toml

# for 5 node
sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:9490\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:9491\"%; s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:1357\"%" $HOME/$work_dir/config/app.toml

# for 6 node
sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:9590\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:9591\"%; s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:1367\"%" $HOME/$work_dir/config/app.toml

# for 7 node
sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:9690\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:9691\"%; s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:1377\"%" $HOME/$work_dir/config/app.toml

# for 8 node
sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:9790\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:9791\"%; s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:1387\"%" $HOME/$work_dir/config/app.toml

# for 9 node
sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:9890\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:9891\"%; s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:1397\"%" $HOME/$work_dir/config/app.toml

# for 10 node
sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:9990\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:9991\"%; s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:1407\"%" $HOME/$work_dir/config/app.toml

# for 11 node
sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:9900\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:9901\"%; s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:1417\"%" $HOME/$work_dir/config/app.toml

# for 12 node
sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:9910\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:9911\"%; s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:1427\"%" $HOME/$work_dir/config/app.toml

# for 13 node
sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:9920\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:9921\"%; s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:1437\"%" $HOME/$work_dir/config/app.toml

# for 14 node
sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:9930\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:9931\"%; s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:1447\"%" $HOME/$work_dir/config/app.toml

# for 15 node
sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:9940\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:9941\"%; s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:1457\"%" $HOME/$work_dir/config/app.toml
```

### `client.toml` Modifications

For each node, adjust the node address as follows:

```bash
# for 2 node
sed -i.bak -e "s%^node = \"tcp://localhost:26657\"%node = \"tcp://localhost:36657\"%" $HOME/$work_dir/config/client.toml

# for 3 node
sed -i.bak -e "s%^node = \"tcp://localhost:26657\"%node = \"tcp://localhost:46657\"%" $HOME/$work_dir/config/client.toml

# for 4 node
sed -i.bak -e "s%^node = \"tcp://localhost:26657\"%node = \"tcp://localhost:56657\"%" $HOME/$work_dir/config/client.toml

# for 5 node
sed -i.bak -e "s%^node = \"tcp://localhost:26657\"%node = \"tcp://localhost:60557\"%" $HOME/$work_dir/config/client.toml

# for 6 node
sed -i.bak -e "s%^node = \"tcp://localhost:26657\"%node = \"tcp://localhost:60657\"%" $HOME/$work_dir/config/client.toml

# for 7 node
sed -i.bak -e "s%^node = \"tcp://localhost:26657\"%node = \"tcp://localhost:60757\"%" $HOME/$work_dir/config/client.toml

# for 8 node
sed -i.bak -e "s%^node = \"tcp://localhost:26657\"%node = \"tcp://localhost:60857\"%" $HOME/$work_dir/config/client.toml

# for 9 node
sed -i.bak -e "s%^node = \"tcp://localhost:26657\"%node = \"tcp://localhost:60957\"%" $HOME/$work_dir/config/client.toml

# for 10 node
sed -i.bak -e "s%^node = \"tcp://localhost:26657\"%node = \"tcp://localhost:61057\"%" $HOME/$work_dir/config/client.toml

# for 11 node
sed -i.bak -e "s%^node = \"tcp://localhost:26657\"%node = \"tcp://localhost:61157\"%" $HOME/$work_dir/config/client.toml

# for 12 node
sed -i.bak -e "s%^node = \"tcp://localhost:26657\"%node = \"tcp://localhost:61257\"%" $HOME/$work_dir/config/client.toml

# for 13 node
sed -i.bak -e "s%^node = \"tcp://localhost:26657\"%node = \"tcp://localhost:61357\"%" $HOME/$work_dir/config/client.toml

# для 14 node
sed -i.bak -e "s%^node = \"tcp://localhost:26657\"%node = \"tcp://localhost:61457\"%" $HOME/$work_dir/config/client.toml

# for 15 node
sed -i.bak -e "s%^node = \"tcp://localhost:26657\"%node = \"tcp://localhost:61557\"%" $HOME/$work_dir/config/client.toml
```

### Updating `external_address`

After making the above changes, update `external_address` external_address=$(wget -qO- eth0.me) as follows:

```bash
# for 2 node
sed -i.bak -e "s/^external_address *=.*/external_address = \"$external_address:36656\"/" $HOME/$work_dir/config/config.toml

# for 3 node
sed -i.bak -e "s/^external_address *=.*/external_address = \"$external_address:46656\"/" $HOME/$work_dir/config/config.toml

# for 4 node
sed -i.bak -e "s/^external_address *=.*/external_address = \"$external_address:56656\"/" $HOME/$work_dir/config/config.toml

# for 5 node
sed -i.bak -e "s/^external_address *=.*/external_address = \"$external_address:60556\"/" $HOME/$work_dir/config/config.toml

# for 6 node
sed -i.bak -e "s/^external_address *=.*/external_address = \"$external_address:60656\"/" $HOME/$work_dir/config/config.toml

# for 7 node
sed -i.bak -e "s/^external_address *=.*/external_address = \"$external_address:60756\"/" $HOME/$work_dir/config/config.toml

# for 8 node
sed -i.bak -e "s/^external_address *=.*/external_address = \"$external_address:60856\"/" $HOME/$work_dir/config/config.toml

# for 9 node
sed -i.bak -e "s/^external_address *=.*/external_address = \"$external_address:60956\"/" $HOME/$work_dir/config/config.toml

# for 10 node
sed -i.bak -e "s/^external_address *=.*/external_address = \"$external_address:61056\"/" $HOME/$work_dir/config/config.toml

# for 11 node
sed -i.bak -e "s/^external_address *=.*/external_address = \"$external_address:61156\"/" $HOME/$work_dir/config/config.toml

# for 12 node
sed -i.bak -e "s/^external_address *=.*/external_address = \"$external_address:61256\"/" $HOME/$work_dir/config/config.toml

# for 13 ноды
sed -i.bak -e "s/^external_address *=.*/external_address = \"$external_address:61356\"/" $HOME/$work_dir/config/config.toml

# for 14 node
sed -i.bak -e "s/^external_address *=.*/external_address = \"$external_address:61456\"/" $HOME/$work_dir/config/config.toml

# for 15 node
sed -i.bak -e "s/^external_address *=.*/external_address = \"$external_address:61556\"/" $HOME/$work_dir/config/config.toml
```

### Restart Node After Changes

After all the necessary modifications, restart the node:

```bash
sudo systemctl restart cosmos && sudo journalctl -u cosmos -f -o cat
```
