# assetfinder
#!/bin/bash
echo "finding subdomains...."
read -p "enter domain name:" domain
echo "Finding subdomains using assetfinder is time consuming please wait"
if [[ $domain != "" ]]; then
	#echo "collecting the subdomains using  assetfinder subs-only it may take some time please wait"
	touch subdomain_subs.txt subdomain_alive.txt subdomain_sorted.txt
	assetfinder --subs-only $domain > subdomain_subs.txt
	#echo "collecting the subdomains using  httprobe it may take some time please wait"
	cat subdomain_subs.txt | httprobe > subdomain_alive.txt
 	cat subdomain_alive.txt | sort -u > subdomain_sorted.txt
    cat subdomain_sorted.txt
 	count=$( wc -l < subdomain_sorted.txt )
 	echo "The total number of subdomains of $domain is $count"
 else
 	echo "please enter a domain name"
 fi
 echo "--------------------------------------------------------"
 rm subdomain_subs.txt
 rm subdomain_alive.txt
