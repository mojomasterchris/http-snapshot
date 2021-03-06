# http-snapshot
NSE script for Nmap that attempts to take a snapshot of the remote host if it runs a web server.  Based on the original SpiderLabs http-screenshot.nse, with fixes included. Requires wkhtmltoimage to be installed and in your $PATH. The OSX wkhtmltoimage installer package is included in this repository.
## Installation
First, install the correct wkhtmltoimage binary for your OS, followed by:
```
wget https://raw.githubusercontent.com/v00d00sec/http-snapshot/master/http-snapshot.nse
cp http-snapshot.nse /usr/local/share/nmap/scripts/
nmap --script-updatedb
```
## Usage
```
nmap -sV --script=http-snapshot -p80,443 google.vn
```
## Sample Output
```
Starting Nmap 7.12 ( https://nmap.org ) at 2016-08-25 09:43 ICT
Nmap scan report for google.vn (216.58.199.3)
Host is up (0.00045s latency).
Other addresses for google.vn (not scanned): 2404:6800:4005:801::2003
rDNS record for 216.58.199.3: hkg12s02-in-f3.1e100.net
PORT    STATE SERVICE
80/tcp  open  http
| http-snapshot:
|_  Snapshot saved to snap-216.58.199.3:80.png
443/tcp open  https
| http-snapshot:
|_  Snapshot saved to snap-216.58.199.3:443.png

Nmap done: 1 IP address (1 host up) scanned in 5.05 seconds
```
##### Known Issues
- If the site redirects from HTTP to HTTPS or any 301 code is received, the captured snapshot will be blank. It is a known issue with wkhtmltoimage. 
- Sometimes the script loops forever, could possibly be fixed by using timeouts.

# http-snapshot-pjs
Requires phantomjs and screenshot.js by Pierre LALET <pierre.lalet@cea.fr> to be installed and in your $PATH.
## Installation
```
brew install phantomjs
wget https://raw.githubusercontent.com/v00d00sec/http-snapshot/master/screenshot.js
wget https://raw.githubusercontent.com/v00d00sec/http-snapshot/master/http-snapshot-pjs.nse
cp screenshot.js /usr/local/bin/
cp http-snapshot-pjs.nse /usr/local/share/nmap/scripts/
nmap --script-updatedb
```
## Usage
```
nmap -sV --script=http-snapshot-pjs -p80,443 google.vn
```
## Sample Output
```
Starting Nmap 7.12 ( https://nmap.org ) at 2016-08-25 11:53 ICT
Nmap scan report for google.vn (216.58.199.3)
Host is up (0.00055s latency).
Other addresses for google.vn (not scanned): 2404:6800:4005:802::2003
rDNS record for 216.58.199.3: hkg12s02-in-f3.1e100.net
PORT    STATE SERVICE
80/tcp  open  http
| http-snapshot-pjs:
|_  Snapshot saved to snap-216.58.199.3:80.png
443/tcp open  https
| http-snapshot-pjs:
|_  Snapshot saved to snap-216.58.199.3:443.png
```
##### Known Issues
- Sometimes the captured snapshot will be blank.

# http-snapshot-cc
Requires CutyCapt to be installed and in your $PATH.
## Installation
```
brew install Cuty_Capt
wget https://raw.githubusercontent.com/v00d00sec/http-snapshot/master/http-snapshot-cc.nse
cp http-snapshot-cc.nse /usr/local/share/nmap/scripts/
nmap --script-updatedb
```
## Usage
```
nmap -sV --script=http-snapshot-cc -p80,443 google.vn
```
## Sample Output
```
Starting Nmap 7.12 ( https://nmap.org ) at 2016-08-25 16:16 ICT
Nmap scan report for google.vn (216.58.199.3)
Host is up (0.00074s latency).
Other addresses for google.vn (not scanned): 2404:6800:4005:802::2003
rDNS record for 216.58.199.3: hkg12s02-in-f3.1e100.net
Not shown: 998 filtered ports
PORT    STATE SERVICE
80/tcp  open  http
| http-snapshot-cc:
|_  Snapshot saved to cc-snap-216.58.199.3:80.png
443/tcp open  https
| http-snapshot-cc:
|_  Completed with errors

Nmap done: 1 IP address (1 host up) scanned in 58.56 seconds
```
##### Known Issues
- Sometimes the script will hang on HTTPS ports (added --max-wait=15000)
