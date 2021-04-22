## Introduce self-signed certificate process with openssl

### "A self-signed certificate can be used for testing, but for production servers, use a certificate signed by a certificate authority (CA)"

CA(Certification Authority), one organization responsible for certificate release and management

### Difference between self-signed certificate and CA signed certificate:
Self-signed certificates have no revoke list, so they cannot be revoked. If someone gets your private key, he can pretend to be you to do the communication.

### The process to sign a certificate
1.Create ca.key and remove password
> openssl genrsa -des3 -out ca.key 2048  
> openssl rsa -in ca.key -out ca.key

2.Create ca.crt(self-signed)
> openssl req -new -x509 -key ca.key -out ca.crt -days 3650 

3.Create server.key and remove password
> openssl genrsa -des3 -out server.key 2048  
> openssl rsa -in server.key -out server.key  
or use ca.key  
> cp ca.key server.key  

4.Create csr(Certificate Signing Request) file
> openssl req -new -key server.key -out server.csr 

5.Sign the csr with private key and self ca.crt
> openssl x509 -req -days 3650 -in server.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out server.crt

server.key and server.crt are the ones will be used

You can merge them to PEM:
> cat server.key server.crt > server.pem

![](https://meirongding.github.io/notes/images/self%20signed%20crt.png)

