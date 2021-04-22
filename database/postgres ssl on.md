## Postgres 9.6 windows connected by client on windows
[Official document](http://www.postgres.cn/docs/9.4/ssl-tcp.html)  
[Reference URL](https://postgresrocks.enterprisedb.com/t5/EDB-Guides/How-to-setup-SSL-authentication/ba-p/1647)

### To use ssl, you need following configuration:

1.The server will listen for both normal and SSL connections when:
> postgresql.conf >> ssl = on  
> pg_hba.conf >> hostssl all all 0.0.0.0/0 md5

2.Create following file under data folder
> (Create private key file with password)openssl genrsa -des3 -out server.key 1024  
> (Delete password)openssl rsa -in server.key -out server.key  
> (Create server cetificate)openssl req -new -key server.key -days 3650 -out server.crt -x509

[More operation about certificate](https://meirongding.github.io/notes/certs/self-signed%20crt%20based%20on%20openssl)

3.Configure ssl_ca_file
> (Create root certificate)copy server.crt root.crt  
> postgresql.conf >> ssl_ca_file = 'root.crt'

4.Restart postgresql service with ssl but no certificate required(Task Manager >> services)

**Now ssl postgres prepared!**

### To connect to the ssl postgres, certificate maybe required from client.

Connect in verify-ca mode:  
> Copy the root.crt from server to the client  
> postgresql://${DATABASE_HOST}:${DATABASE_PORT}/postgres?ssl=true&sslmode=verify-ca&sslrootcert=${DATABASE_CERTIFICATE}"

Connect in verify-full mode:
Here I make certificates on the server side and pass it to the client

1.Create the private key postgresql.key and remove the passphrase:
> openssl genrsa -des3 -out /tmp/postgresql.key 1024

2.Create the sign request file postgresql.csr
> openssl req -new -key /tmp/postgresql.key -out /tmp/postgresql.csr

3.Sign it using the trusted root certificate(copy the root.crt and server.key from server)
> openssl x509 -req -in /tmp/postgresql.csr -CA root.crt -CAkey server.key -out  /tmp/postgresql.crt -CAcreateserial

4.Copy the postgresql.key, postgresql.crt and root.crt to the client machine and connect to postgres with these three

### JDBC connect to the ssl with keystore
> keytool -noprompt -importcert -file ${dbcert} -alias ${dbcertAlias} -keystore ${JAVA_HOME}/jre/lib/security/cacerts -storepass $SSL_TRUST_STORE_PASSWORD
