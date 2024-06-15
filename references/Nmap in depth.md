### Title: Nmap in depth
Tags: #recon  #nmap #port-scanning
Author:
Reference: youtube:nmap in depth

#### Notes
**Summary**: 1-2 sentence overview
**Notes**:
IP -> Port -> scan type -> scan timings -> output types
- IP
```sh
command: nmap -sn[optional] <IP-address>
1. Single IP => 1.2.3.4
2. subnet range => 1.2.3.4/8
3. Ip range => 1.2.3.4-8
4. Specific IPs => 1.2.3.4 5.6.7.8
5. text file => nmap -iL host.txt
6. Domain => nmap a.com
```

- Ports
```sh
nmap <IP_address> -p<opt>
```

| Port              | Example       |
| ----------------- | ------------- |
| single            | -p80          |
| seq               | -p20-30       |
| distributed       | -p80,22,111   |
| service specific  | -p http       |
| protocol specific | -p T:22, U:53 |
| all ports         | -p-           |
| top ports         | --top-ports   |
- <mark class="hltr-cyan">Scan techniques:</mark> need go deep in this watch this video again and also it has some video series about this.
- Scan status:
  - open: A--syn-->B, B--syn+ack-->A
  - closed: A--syn-->B, B--res+ack-->A