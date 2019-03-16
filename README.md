# [Bluecoin](https://www.bluecoin.de).  

Shell script to install a Bluecoin Masternode on a Linux server running Ubuntu 16.04. Use it on your own risk.
***

## VPS installation for version **1.1.0**
```
wget -N https://raw.githubusercontent.com/heindeep/bluecoin-installer/master/bluecoin-installer.sh
bash bluecoin-installer.sh
```
***

## Desktop wallet setup

After the Masternode is up and running, you need to configure the desktop wallet accordingly. Here are the steps:
1. Open the Bluecoin Desktop Wallet.
2. Go to RECEIVE and create a New Address: **MN1**
3. Send **10000** BLUE to **MN1**. You need to send all 10000 coins in one single transaction.
4. Wait for 15 confirmations.
5. Go to **Help -> "Debug Window - Console"**
6. Type the following command: **masternode outputs**
7. Type the following command: **masternode genkey**
8. Go to  **Tools -> "Open Masternode Configuration File"**
9. Add the following entry:
```
[Alias] [IPAddress] [Privkey] [TxHash] [TxIndex]
```
* Alias: **MN1**
* Address: **VPS_IP:PORT**
* Privkey: **Masternode Private Key value from Step 7**
* TxHash: **First value from Step 6**
* TxIndex:  **Second value from Step 6**
9. Save and close the file.
10. Go to **Masternode Tab**. If you tab is not shown, please enable it from: **Settings - Options - Wallet - Show Masternodes Tab**
11. Click **Update status** to see your node. If it is not shown, close the wallet and start it again. Make sure the wallet is unlocked.
12. Select your MN and click **Start Alias** to start it.
13. Alternatively, open **Debug Console** and type:
```
startmasternode alias false MN1
```
14. Login to your VPS and check your masternode status by running the following command to confirm your MN is running:
```
bluecoin-cli masternode status
```
***

## Usage:
```
bluecoin-cli masternode status
bluecoin-cli getinfo
bluecoin-cli mnsync status
```
Also, if you want to check/start/stop **Bluecoin**, run one of the following commands as **root**:

```
systemctl status BLUE #To check if Bluecoin service is running
systemctl start BLUE #To start Bluecoin service
systemctl stop BLUE #To stop Bluecoin service
systemctl is-enabled BLUE #To check if Bluecoin service is enabled on boot
```
***

## Masternode update:
In order to update your Snodecoin Masternode to version 1.0.0, please run the following commands:
```
# stop service
systemctl stop BLUE

# create backup
cp -r ~/.bluecoin ~/.bluecoin.bakup

# remove data from old wallet
rm -rf ~/.bluecoin/*

# copy the wallet and config files back
cp ~/.bluecoin.bakup/wallet.dat ~/.bluecoin.bakup/bluecoin.conf ~/.bluecoin.bakup/masternode.conf ~/.bluecoin

# download new wallet 
cd /tmp
wget -N https://github.com/heindeep/bluecoin/releases/download/V1.0.0/bluecoin-1.0.0-linux64.tar.gz
tar xvzf bluecoin-1.0.0-linux64.tar.gz --strip 2
chmod +x bluecoind bluecoin-cli
mv bluecoind bluecoin-cli /usr/local/bin

#start it
systemctl start BLUE
rm bluecoin-1.0.0-linux64.tar.gz

snodecoin-cli getinfo
```
Open your desktop wallet and start the node from there.
***

## Donations
Any donation is highly appreciated


