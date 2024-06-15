
### Title: Recon meghodology
Tags: #methodology  #recon 
Related to: 
See also: 
Previous:

### Body
#### **Summary**: 
Should be short, no prose

#### **Notes**:

### Automated recon:
#### subdomain enum:
1. amass and subfinder
2. froggy
3. reconizer
   
```sh
froggy and reconizer stores more than subdomains.
```

#### Live domains
1. use `httpx` tool to find the live subdomains
#### Portscan:
1. masscan
2. nmap 
3. nabu
4. rustscan
   
```

create a script that scans with these scanners [except nmap]. use nmap manually.
scan both live and non-live subdomain's ports.
```

#### Urls
1. waybackurls
2. waymore
3. gospider
4. hakcrawler
5. katana

#### content discovery:
1. ffuf
2. dirsearch
3. dirb

#### Js files
1. `cat urls.txt | grep '.js$'` use this command to get only js files
2. `katana -u https://test.com -jc -d 2 | grep ".js$" | uniq | sort > js.txt` alternative 
3. find secret keys: `cat js.txt | while read url; do python3 SecretFinder.py -i $url -o cli >> secrets.txt; done`
4. there are some nuclei template for js secret finding also watch them.
5. use the api keys in : `keyhacks`
   
```
This methodology will change
```

#### Parameter
1. arjun
2. x8 
3. paraminer
4. Paramspider


### Manual Recon
1. goto cert.sh find some acquasations
2. go to shodan 
3. find more domains
4. find ports using nmaps
5. Github recon 
   
```
Learn github recon in mobile
```
### References
- [[]]




