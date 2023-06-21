# Enum Basics

## nmap -sC -sV -oA nmap/target ip
  1. A           Enable OS detection, version detection, script scanning, and traceroute
  2. i           nmap -iL targets.txt	Scan targets from a file
  3. top-ports   nmap 192.168.1.1 -p-65535	Leaving off initial port in range makes the scan start at port 1
  
  ### Examples
  
  1. Scan for web servers and grep to show which IPs are running web servers
    nmap -p80 -sV -oG - -open 192.168.1.1/24 | grep open
  2. Generate a list of the IPs of live hosts
    nmap -iR 10 -n -oX out.xml | grep "Nmap" | cut -d " " -f5 > live-hosts.txt	
  3. Append IP to the list of live hosts
    nmap -iR 10 -n -oX out2.xml | grep "Nmap" | cut -d " " -f5 >> live-hosts.txt	
  4. Compare output from nmap using the ndif
    ndiff scanl.xml scan2.xml
  5. Convert nmap xml files to html files
    xsltproc nmap.xml -o nmap.html	
  6. Reverse sorted list of how often ports turn up
    grep " open " results.nmap | sed -r ‘s/ +/ /g’ | sort | uniq -c | sort -rn | less
