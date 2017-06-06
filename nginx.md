# NGINX

### 1) Generate Certificate Signing Request (CSR) to get TSL/HTTPS certificate

Check that OpenSSL is installed:
```sh
dpkg -l |grep openssl
```

If `libgnutls-openssl27:amd64` and `openssl` is missing, then install openssl
```sh
sudo apt install openssl
```

#### Generate RSA key

You should use 4096 private key length, but this may take a while to generate
```sh
mkdir ~/domain.com.ssl/
cd ~/domain.com.ssl/
openssl genrsa -out ~/domain.com.ssl/domain.com.key 4096
```

#### Create CSR with the RSA private key

```sh
openssl req -new -sha256 -key ~/domain.com.ssl/domain.com.key -out ~/domain.com.ssl/domain.com.csr
```

When prompted, enter the necessary information for creating a CSR such as Common Name, Organization Name, City, State, Country, etc.


#### Verify the CSR
```sh
openssl req -noout -text -in ~/domain.com.ssl/domain.com.csr
```
Double check the output especially the Commom Name (CN) value on the 4th line to ensure it matches your domain name.


#### Now submit the CSR to the certificate authority to obtain TLS certificate.
