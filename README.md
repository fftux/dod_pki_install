# DOD PKI Install
This repo contains a simple playbook that can be used to help install DOD CA certs on a RHEL system.

## Automated Install
`ansible-playbook dod_pki_install.yml`

## Manual steps
1. Pull the certs
`curl https://dl.dod.cyber.mil/wp-content/uploads/pki-pke/zip/certificates_pkcs7_DoD.zip -o DoD_PKI.zip`

2. Unzip archive
`unzip DoD_PKI.zip`

3. Create pem of all certs (copied from included README)
`openssl pkcs7 -in Certificates_PKCS7_*_DoD/Certificates_PKCS7_*_DoD.pem.p7b -print_certs -out DoD_CAs.pem`

4. Copy pem to anchors directory
`sudo cp DoD_CAs.pem /etc/pki/ca-trust/source/anchors/`

5. Update trusted CA db.
`sudo update-ca-trust`
