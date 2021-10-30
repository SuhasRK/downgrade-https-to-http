
# Downgrading https-to-http

HTTPS stands for Hyper Text Transfer Protocol Secure.
HTTPS is highly advanced and secure version of HTTPS.So username and password grabbing from HTTPS websites becomes impossible.
So we use a method called [ssl-stripping](https://www.venafi.com/blog/what-are-ssl-stripping-attacks) and we downgrade https to http and then we can use a normal packet sniffer (like wireshark) to read information present in packets flowing in network.
So for ssl-stripping we use a tool called as [bettercap](https://www.kali.org/tools/bettercap/)





## Installation

Install bettercap with apt.I recommend to use version bettercap v2.23.
[click here to download bettercap v2.23](https://ufile.io/joxjzflg)

```bash
  bettercap
  caplets.show
```
And the list of caplets available appears on the screen.Search for hstshijack/hstshijack.
Packet which comes built-in with bettercap v2.23 will not work correctly.So I recommend to use modified hstshijack/hstshijack caplet.[Click on the link](https://www.mediafire.com/file/woc3tjfdyuwycp0/hstshijack.cap/file) to download it.Then replace the downloaded bettercap file with original hstshijack/hstshijack file present in directory /usr/share/bettercap/caplets/hstshijack/hstshijack.cap.
So now we are good to go.

    
## Demo

Before starting ssl-stripping the target needs to be arp spoofed.To carry out arp spoofing we use another caplet file [spoof.cap](https://www.mediafire.com/file/7q7vszdujqeydth/spoof.cap/file) and store it in our root directory.Open that caplet file with any editor and change the IP address present in it to Target's IP address.Then open the terminal in same root directory and enter the following commands.

To ssl-strip all the webpages the user browses,we need to run the following commands

```bash
  ifconfig
```
Above command shows you the name of your external ethernet adapter.Grab that name for further reference.

```bash
  bettercap -iface <name_of_eth_adapter> -caplet spoof.cap
```
Then type:
```bash
  hstshijack/hstshijack
```
This will break down the mentioned https hostnames in hstshijack caplet to http and any traffic flown will be unencrypted.So any packet sniffer can easily grab the credentials present in packets.








