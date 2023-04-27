# Dymension
![1500x500](https://user-images.githubusercontent.com/91562185/234884978-f1a6b9f1-5939-422c-af5d-ca66a9feb758.jpg)

# sistem özellikleri
4cpu 8 ram
## ÖDÜLSÜZDÜR

# update ve kütüphane kuruyoruz
```
sudo apt update && sudo apt upgrade -y
sudo apt install curl git wget htop tmux build-essential jq make lz4 gcc unzip -y  
```
# go kuruyoruz
```
wget -O go_install.sh https://raw.githubusercontent.com/itrocket-team/testnet_guides/main/utils/go_install.sh && chmod +x go_install.sh && ./go_install.sh
source ~/.bash_profile
go version
```


# cüzdan adı ve node adını değiştirin.
```
echo "export WALLET="cüzdan-adı"" >> $HOME/.bash_profile
echo "export MONIKER="node-adı"" >> $HOME/.bash_profile
echo "export DYMENSION_CHAIN_ID="35-C"" >> $HOME/.bash_profile
echo "export DYMENSION_PORT="32"" >> $HOME/.bash_profile
source $HOME/.bash_profile


cd $HOME
rm -rf dymension
git clone https://github.com/dymensionxyz/dymension.git --branch v0.2.0-beta
cd dymension
make install


dymd config node tcp://localhost:${DYMENSION_PORT}657
dymd config keyring-backend test
dymd config chain-id 35-C
dymd init molla202 --chain-id 35-C


wget -O $HOME/.dymension/config/genesis.json https://testnet-files.itrocket.net/dymension/genesis.json
wget -O $HOME/.dymension/config/addrbook.json https://testnet-files.itrocket.net/dymension/addrbook.json


SEEDS="c26dc8486e8c4817e154812462993ce562cda221@dymension-testnet-seed.itrocket.net:32656"
PEERS="adf394846dc942b1fd03f6e310eda60b5eda7848@dymension-testnet-peer.itrocket.net:32656"
sed -i -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.dymension/config/config.toml


sed -i.bak -e "s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:${DYMENSION_PORT}317\"%;
s%^address = \":8080\"%address = \":${DYMENSION_PORT}080\"%;
s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:${DYMENSION_PORT}090\"%; 
s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:${DYMENSION_PORT}091\"%; 
s%^address = \"0.0.0.0:8545\"%address = \"0.0.0.0:${DYMENSION_PORT}545\"%; 
s%^ws-address = \"0.0.0.0:8546\"%ws-address = \"0.0.0.0:${DYMENSION_PORT}546\"%" $HOME/.dymension/config/app.toml


sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:${DYMENSION_PORT}658\"%; 
s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://0.0.0.0:${DYMENSION_PORT}657\"%; 
s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:${DYMENSION_PORT}060\"%;
s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:${DYMENSION_PORT}656\"%;
s%^external_address = \"\"%external_address = \"$(wget -qO- eth0.me):${DYMENSION_PORT}656\"%;
s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":${DYMENSION_PORT}660\"%" $HOME/.dymension/config/config.toml


sed -i -e "s/^pruning *=.*/pruning = \"nothing\"/" $HOME/.dymension/config/app.toml
sed -i -e "s/^pruning-keep-recent *=.*/pruning-keep-recent = \"100\"/" $HOME/.dymension/config/app.toml
sed -i -e "s/^pruning-interval *=.*/pruning-interval = \"50\"/" $HOME/.dymension/config/app.toml


sed -i 's/minimum-gas-prices =.*/minimum-gas-prices = "0.0udym"/g' $HOME/.dymension/config/app.toml
sed -i -e "s/prometheus = false/prometheus = true/" $HOME/.dymension/config/config.toml
sed -i -e "s/^indexer *=.*/indexer = \"null\"/" $HOME/.dymension/config/config.toml


sudo tee /etc/systemd/system/dymd.service > /dev/null <<EOF
[Unit]
Description=Dymension node
After=network-online.target
[Service]
User=$USER
ExecStart=$(which dymd) start --home $HOME/.dymension
Restart=on-failure
RestartSec=3
LimitNOFILE=65535
[Install]
WantedBy=multi-user.target
EOF


dymd tendermint unsafe-reset-all --home $HOME/.dymension
curl https://testnet-files.itrocket.net/dymension/snap_dymension.tar.lz4 | lz4 -dc - | tar -xf - -C $HOME/.dymension


sudo systemctl daemon-reload
sudo systemctl enable dymd
sudo systemctl restart dymd && sudo journalctl -u dymd -f
```
# cüzdan olusturuyoruz yada import ediyoruz
```
dymd keys add cüzdan-adı 
```
```
dymd keys add cüzdan-adı --recover
```
# hiç bişi değiştirmiyoruz olduğu gibi en başta ayarladık zaten
```
dymd tx staking create-validator \
  --amount 1000000udym \
  --from $WALLET \
  --commission-max-change-rate "0.01" \
  --commission-max-rate "0.2"   --commission-rate "0.05" \
  --min-self-delegation "1" \
  --pubkey  $(dymd tendermint show-validator) \
  --moniker $MONIKER \
  --chain-id 35-C
  ```
