# democa
Demo CA support files

All passwords are: password

# Create demo CA and client certs

```
# Grab example CA config
curl -O https://raw.githubusercontent.com/lucaspnw/democa/master/ca.cnf

# Generate CA cert+key
openssl req -new -x509 -days 9999 -config ca.cnf -keyout ca-key.pem -out ca-crt.pem

# Generate client key
openssl genrsa -out client-key.pem 4096

# Grab client config file
curl -O https://raw.githubusercontent.com/lucaspnw/democa/master/client.cnf

# Client signing request
openssl req -new -config client.cnf -key client-key.pem -out client-csr.pem

# Sign client key
openssl x509 -req -extfile client.cnf -days 999 -passin "pass:password" -in client-csr.pem -CA ca-crt.pem -CAkey ca-key.pem -CAcreateserial -out client-crt.pem

# Export PFX for windows
openssl pkcs12 -export -out client.pfx -inkey client-key.pem -in client-crt.pem

```
