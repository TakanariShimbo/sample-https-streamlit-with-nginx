## About

Streamlit with Nginx on Docker to enable SSL using a self-signed certificate

![about](/data/about.png)

## Usage

### STEP1: Build App Image

```sh
cd app

# Please add the username and tag correctly.
docker build -t sample-streamlit .
```

### STEP2: Generate Self-Signed Certificate

```sh
cd nginx

# generate private-key
openssl genpkey -out private-key.key -algorithm RSA -pkeyopt rsa_keygen_bits:2048

# generate certificate-request
# please set the certificate.cnf file before executing it.
openssl req -new -key private-key.key -out certificate-request.csr -config certificate.cnf

# generate certificate
openssl x509 -req -in certificate-request.csr -signkey private-key.key -out certificate.crt -days 3650 -extfile certificate.cnf -extensions v3_ca
```

### STEP3: Build Server

```sh
# Please set the .env file before executing it.
docker compose up -d
```

Check access here (https://XXX.XXX.XXX.XXX:HTTPS_PROT), after building server.
