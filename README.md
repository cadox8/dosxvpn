<h1 align="center">dosxvpn</h1>

<h4 align="center">Easily deploy your own personal VPN server with DNS adblocking running on <a href="https://digitalocean.com)" target="_blank">DigitalOcean</a>.</h4>

---

![](/static/images/overview.gif?raw=true)

## Key Features
* Personal IPsec-based VPN ([strongSwan](https://strongswan.org/)).
* Ad blocking DNS setup by default ([Pi-hole](https://pi-hole.net/)).
* Generates profiles for sharing VPN with OSX/iPhone and Android.
* No additional software required for OSX/iPhone - uses native VPN client.
* Simple Web or CLI installation methods.
* Automated OS and VPN software updates.

## Web Installer (OSX) 
1. Download the latest pre-built app from the [GitHub Releases](https://github.com/dan-v/dosxvpn/releases) page.
2. Open the app and run through the web based installation wizard to setup a new VPN.

## CLI Usage (OSX)
1. Download the latest pre-built cli from the [GitHub Releases](https://github.com/dan-v/dosxvpn/releases) page.
2. Make the binary executable
  ```sh
  chmod +x dosxvpn
  ```
3. Create an API token (https://cloud.digitalocean.com/settings/api/tokens) and export it
  ```sh
  export DIGITALOCEAN_ACCESS_TOKEN=<token>
  ```
4. See help for all options
  ```sh
  ./dosxvpn -h
  ```

### CLI Examples
* Deploy a new VPN and configure for immediate use
  ```sh
  ./dosxvpn deploy --region sfo2 --auto-configure
  ```
* List dosxvpn VPN instances
  ```sh
  ./dosxvpn ls
  ```
* Remove dosxvpn VPN instance
  ```sh
  ./dosxvpn rm --name <name>
  ```

## FAQ
1. <b>Should I use dosxvpn?</b> That's up to you. Use at your own risk.
2. <b>Why is this better than using public VPN provider XYZ?</b> While most VPN providers will provide a secure connection to their endpoints, you may not be interested in putting blind faith in their claims that they will not log or track your activity online.
3. <b>How is this different than [algo](https://github.com/trailofbits/algo)?</b> 1) Installallation - is simple and has no additional system dependencies. 2) Updates: dosxvpn handles updates of both the OS and VPN. This means any critical security updates or bug fixes will automatically be applied for you.
4. <b>How much does this cost?</b> This launches a 512MB DigitalOcean droplet that costs $5/month currently.
5. <b>What is the bandwidth limit?</b> The 512MB DigitalOcean droplet has a 1TB bandwidth limit. This does not appear to be strictly enforced.
6. <b>Where does dosxvpn store VPN configuration files?</b> You can find all deployed VPN configuration files in your ~/.dosxvpn directory.
7. <b>Are you going to support other VPS providers?</b> Not right now.
8. <b>Will this make me completely anonymous?</b> No, absolutely not. All of your traffic is going through a VPS which could be traced back to your account. You can also be tracked still with [browser fingerprinting](https://panopticlick.eff.org/), etc. Your [IP address may still leak](https://ipleak.net/) due to WebRTC, Flash, etc.
9. <b>How do I uninstall this thing on OSX?</b> You can uninstall through the Web interface, which will also remove the running droplet in your DigitalOcean account. Alternatively go to System Preferences->Network, click on dosxvpn-* and click the '-' button in the bottom left to delete the VPN. Don't forget to also remove the droplet that is deployed in your DigitalOcean account.

# Powered By
* [strongSwan](https://strongswan.org/) - IPsec-based VPN software
* [CoreOS](https://coreos.com/) - used for running containers and automatic OS updates capabilities
* [Pi-hole](https://pi-hole.net/) - used for DNS adblocking
* [Platypus](http://www.sveinbjorn.org/platypus) - used to build the native OSX app 
* [godo](https://github.com/digitalocean/godo) - DigitalOcean Go API client

# Acknowledgements
* [trailofbits/algo](https://github.com/trailofbits/algo) - strongSwan configuration is borrowed from this project
* [jbowens/dochaincore](https://github.com/jbowens/dochaincore) - Deployment code is borrowed from this project
* [vimagick/strongswan](https://github.com/vimagick/dockerfiles/tree/master/strongswan) - Using a forked version of this docker image for VPN server

# Building Source
1. Install dependency [platypus cli](http://www.sveinbjorn.org/platypus)
  ```sh
  brew install platypus
  ```
  
2. Fetch the project with `go get`:
  ```sh
  go get github.com/dan-v/dosxvpn
  cd $GOPATH/src/github.com/dan-v/dosxvpn
  ```
  
2. Run make to build
  ```sh
  make
  ```
