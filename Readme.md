# Create fully trusted certificates

On the mac, you can create a certificate that's fully trusted by Chrome and Safari, at the system level by doing the following

## create a root authority cert

```bash
./create_root_cert_and_key.sh
```

## create a wildcard cert for mysite.com

```bash
./create_certificate_for_domain.sh mysite.com
```
## or create a cert for www.mysite.com, no wildcards

```bash
./create_certificate_for_domain.sh www.mysite.com www.mysite.com
```
The above uses the following scripts, and a supporting file v3.ext, to avoid subject alternative name missing errors

If you want to create a new self signed cert that's fully trusted using your own root authority, you can do it using these scripts.

## One more step - How to make the self signed certs fully trusted in Chrome/Safari

To allow the self signed certificates to be FULLY trusted in Chrome and Safari, you need to import a new certificate authority into your Mac. To do so follow these instructions, or the more detailed instructions on this general process on the mitmproxy website:

1. Open Keychain Access
1. Choose "System" in the "Keychains" list
1. Choose "Certificates" in the "Category" list
1. Choose "File | Import Items..."
1. Browse to the file created above, "rootCA.pem", select it, and click "Open"
1. Select your newly imported certificate in the "Certificates" list.
1. Click the "i" button, or right click on your certificate, and choose "Get Info"
1. Expand the "Trust" option
1. Change "When using this certificate" to "Always Trust"
1. Close the dialog, and you'll be prompted for your password.
1. Close and reopen any tabs that are using your target domain, and it'll be loaded securely!

and as a bonus, if you need java clients to trust the certificates, you can do so by importing your certs into the java keystore. Note this will remove the cert from the keystore if it already exists, as it needs to to update it in case things change. It of course only does this for the certs being imported.