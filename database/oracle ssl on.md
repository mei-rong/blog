# Oracle ssl on(windows)
[Official document](https://docs.oracle.com/cd/B28359_01/network.111/b28530/asossl.htm#i1006119)

## Use "Wallet Manager" to create "Wallet" and create certificate request file
### 1. Create "Wallet"
```
Wallet Manager > Wallet > new
```
### 2. Create certificate request file
```
You'll get a promote after you create "wallet"  
or select the wallet and add one
```
### 3. Export the request file as user.csr(It'll be signed by ca)
### 4. Save the wallet created(**Save it under the default folder or you'll get error when used**)
### 5. Make "Wallet" auto login(Or you'll get error when connect to the DB)
```
Check the checkbox under the wallet tab
```
## Make certificate with openssl
```
openssl genrsa -des3 -out ca.key 2048  
openssl rsa -in ca.key -out ca.key  
openssl req -new -x509 -key ca.key -out ca.crt -days 3650

openssl x509 -req -days 3650 -in user.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out user.crt  
```
[more info about self-signed certificate](https://meirongding.github.io/notes/certs/self-signed%20crt%20based%20on%20openssl)

## Import the trusted certificates and user certificate
```
Wallet Manager  
Import the ca.crt in the trusted certificates  
Import the user.crt in the user certificate  
Now you can see "Ready" at the end of the user certificate title  
Save the wallet
```
## Configure ssl profile
```
Net Manager > Oracle Net configuration > local > profile > choose "network security" > SSL  
choose file system as the configuration method  
select Wallet location  
configure ssl for server  
save network configuration
```
##### Now you can check sqlnet.ora and listener.ora：  
```
WALLET_LOCATION =  
   (SOURCE =  
     (METHOD = FILE)  
     (METHOD_DATA =  
       (DIRECTORY = d:\oracle\WALLETS)  
     )  
   )
```
### Create ssl listener
```
Net Manager > Oracle Net configuration > local > listeners > LISTENER > choose SSL的TCP/IP with SSL and recommend use 2482
```
**Now you can check listener.ora:**
```
LISTENER =
   (DESCRIPTION =
       (ADDRESS = (PROTOCOL = TCPS)(HOST = zhoujunhe)(PORT = 2484))
   )
```
and sqlnet.ora：
```
SQLNET.AUTHENTICATION_SERVICES= (BEQ, **TCPS**, NTS)
```
### Configure static listener service for database(because PMON may not register the ssl port 2484)
```
Net Manager > Oracle Net configuration > local > listeners > LISTENER > databse service > add  > edit and save
```
**Now you can check listener.ora：**
```  
SID_LIST_LISTENER =
   (SID_LIST =
       (SID_DESC =
           (GLOBAL_DBNAME = ora10g.unimassystem.com)
           (ORACLE_HOME = D:\oracle\product\10.2.0\db_1)
           (SID_NAME = ora10g)
       )
   )
```
### Restart listener

## Now you can use oracle on ssl
