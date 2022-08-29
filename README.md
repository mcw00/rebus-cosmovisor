![alt text](https://user-images.githubusercontent.com/101149671/182340706-3eef17b5-f22c-4239-8867-e9f571ba6cac.png)
# rebus-cosmovisor

# Cosmovisor Kurulumu:

>```git clone https://github.com/cosmos/cosmos-sdk
>cd cosmos-sdk
>git checkout v0.42.7
>make cosmovisor
>cp cosmovisor/cosmovisor $GOPATH/bin/cosmovisor
>cd $HOME

--------------------------
>```export DAEMON_NAME=rebusd
>```export DAEMON_HOME=$HOME/.rebus
-------------------------
>```source ~/.profile
>```echo $DAEMON_NAME
------------------------------------
>```mkdir -p $DAEMON_HOME/cosmovisor/genesis/bin
>```mkdir -p $DAEMON_HOME/cosmovisor/upgrades
-------------------------------------------------------
>```cp $HOME/go/bin/rebusd $DAEMON_HOME/cosmovisor/genesis/bin
--------------------------------------------------------
# Servis dosyasını güncelliyoruz

>```sudo nano /etc/systemd/system/rebusd.service
>
>[Unit]
>Description=Rebus Daemon (cosmovisor)
>After=network-online.target
>
>[Service]
>User=root
>ExecStart=/home/root/go/bin/cosmovisor start
>Restart=always
>RestartSec=3
>LimitNOFILE=4096
>Environment="DAEMON_NAME=rebusd"
>Environment="DAEMON_HOME=/root/go/bin/rebusd"
>Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=false"
>Environment="DAEMON_RESTART_AFTER_UPGRADE=true"
>Environment="DAEMON_LOG_BUFFER_SIZE=512"
>
>[Install]
>WantedBy=multi-user.target

-------------------------------------------
>sudo -S systemctl daemon-reload
>sudo -S systemctl enable rebusd
>sudo systemctl start rebusd
--------------------------------

>sudo systemctl status junod

>journalctl -fu rebusd
