# Create development certificates the easy way!

<img src="https://raw.githubusercontent.com/BenMorel/dev-certificates/main/images/logo.svg" alt="" align="left" height="150">

If you're a web developer and need to test your websites locally on HTTPs, you probably don't want to buy an SSL certificate for this.

Instead, you want to **generate your own certificates**! 💪

However, working with the `openssl` CLI can be intimidating. Options are hard to remember. So I've put together these scripts and instructions to make my life, and yours, easier!

## Download

Right click below, *Save Link As...*:

- [create-ca.sh](https://raw.githubusercontent.com/BenMorel/dev-certificates/main/create-ca.sh)
- [create-certificate.sh](https://raw.githubusercontent.com/BenMorel/dev-certificates/main/create-certificate.sh)

## Generate your own Certificate Authority

The *Certificate Authority* is what will make your browser trust the certificates that you'll generate for your development domains. Your browser is bundled with a list of Certificate Autorities that it trusts by default, but because you'll be signing your certificates yourself, you need to instruct it to trust your own certificates.

Just run:

```
create-ca.sh 
```

![create-ca.sh](https://raw.githubusercontent.com/BenMorel/dev-certificates/main/images/create-ca.png)

You only need to perform this step **once**.

## Generate a certificate for your domain

To generate a certificate for `example.dev` and its subdomains, run:

```
create-certificate.sh example.dev
```

![create-certificate.sh](https://raw.githubusercontent.com/BenMorel/dev-certificates/main/images/create-certificate.png)

You can now install the `.key` and `.crt` files in your web server, such as Apache or Nginx.

Repeat this step if you need certificates for other domain names.

## Import the CA in your browser

You only need to perform this step **once** for each browser, whatever the number of certificates you'll generate.

### <img src="https://raw.githubusercontent.com/BenMorel/dev-certificates/main/images/windows.svg" alt="" align="center" height="24"> Edge & Chrome on Windows 10

- open `certmgr.msc`
- expand "Trusted Root Certification Authorities"
- right-click on "Certificates", then "All Tasks" > "Import..."
- click "Next"
- choose the `ca.crt` file
- click "Next" then "Finish"

### <img src="https://raw.githubusercontent.com/BenMorel/dev-certificates/main/images/chrome.svg" alt="" align="center" height="24"> Chrome on Linux

- go to `chrome://settings/certificates`
- click the "Authorities" tab
- click "Import"
- select the `ca.crt` file
- check "Trust this certificate for identifying websites"
- click "OK"

### <img src="https://raw.githubusercontent.com/BenMorel/dev-certificates/main/images/firefox.svg" alt="" align="center" height="24"> Firefox on Windows & Linux

- go to `about:preferences#privacy`
- scroll down to "Certificates"
- click "View Certificates..."
- click "Import..."
- select the `ca.crt` file
- check "Trust this CA to identify websites"
- click "OK"

### <img src="https://raw.githubusercontent.com/BenMorel/dev-certificates/main/images/safari.svg" alt="" align="center" height="24"> Safari on macOS

No instructions yet. [Pull request](https://github.com/BenMorel/dev-certificates/pulls) welcome!

## That's it!

You should now be greeted with:

![Chrome Secure](https://raw.githubusercontent.com/BenMorel/dev-certificates/main/images/secure.png)

If you need to create certificates for other domains, just run `create-certificate.sh` again.
**No need to create or import the CA again!**

Enjoy! 👋

## Credits

These scripts have been created from the steps highlighted in [this StackOverflow answer](https://stackoverflow.com/a/60516812/759866) by [@entrity](https://github.com/entrity).

Icons by [Pixel perfect](https://www.flaticon.com/authors/pixel-perfect).
