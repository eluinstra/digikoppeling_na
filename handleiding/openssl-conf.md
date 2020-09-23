---
sort: 7
---

# openssl.conf

```ini
oid_section = new_oids

[ new_oids ]
serialNumber = 2.5.4.5

[ req_distinguished_name ]
serialNumber = OIN

[ req ]
distinguished_name = req_distinguished_name

[ req_distinguished_name ]
serialNumber = Organisation Identification Number (OIN)

commonName = Common Name (e.g. server FQDN or YOUR name)
commonName_max = 64

organizationalUnitName = Organizational Unit Name (eg, section)

0.organizationName = Organization Name (eg, company)

localityName = Locality Name (eg, city)

stateOrProvinceName = State or Province Name (full name)

countryName = Country Name (2 letter code)
countryName_default = NL
countryName_min = 2
countryName_max = 2

emailAddress = Email Address
emailAddress_max = 64
```
