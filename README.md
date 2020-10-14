# Create development certificates the easy way!

If you're a web developer and need to test your websites locally on HTTPs, you probably don't want to buy an SSL certificate for this.

Instead, you can **generate your own certificates!** 👍

However, working with the `openssl` CLI can be intimidating, and it's hard to remember the options. So I've put together these scripts and instructions to make your life easier!

## Download

Right click below, *Save Link As...*:

- [create-ca.sh](https://raw.githubusercontent.com/BenMorel/dev-certificates/main/create-ca.sh)
- [create-certificate.sh](https://raw.githubusercontent.com/BenMorel/dev-certificates/main/create-certificate.sh)

## Generate your *Certificate Authority*

The Certificate Authority is what will make your browser trust the certificates that you'll generate for your development domains. Your browser is bundled with a list of Certificate Autorities that it trusts by default, but because you'll be signing your certificates yourself, you need to instruct it to trust your own certificates.

Just run:

```
$ ./create-ca.sh 
```

![create-ca.sh](https://raw.githubusercontent.com/BenMorel/dev-certificates/main/create-ca.png)

You only need to perform this step **once**.

## Generate a certificate for your domain

To generate a certificate for `example.dev` and its subdomains, run:

```
./create-certificate.sh example.dev
```

![create-certificate.sh](https://raw.githubusercontent.com/BenMorel/dev-certificates/main/create-certificate.png)

You can now install the `.key` and `.crt` files in your web server, such as Apache or Nginx.

You only need to perform this step **once per domain name**.

## Import the CA in your browser

### In Chrome

- go to `chrome://settings/certificates`
- click the "Authorities" tab
- click "Import"
- select the `ca.crt` file
- check "Trust this certificate for identifying websites"
- click "OK"

### In Firefox

- go to `about:preferences#privacy`
- scroll down to "Certificates"
- click "View Certificates..."
- click "Import..."
- select the `ca.crt` file
- check "Trust this CA to identify websites"
- click "OK"

You only need to perform this step **once for each browser**.

## That's it!

You should now be greeted with:

![Chrome Secure](https://raw.githubusercontent.com/BenMorel/dev-certificates/main/secure.png)

If you need to create certificates for other domains, just run `create-certificate.sh` again.
No need to create or import the CA again!

Enjoy!

## Credits
 
These scripts have been created from the steps highlighted in [this StackOverflow answer](https://stackoverflow.com/a/60516812/759866).
