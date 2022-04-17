This is a list of useful commands/tricks using smbclient, enum4linux and nmap smb scripts - very useful on a pentesting
https://sharingsec.blogspot.com

 # List shares on a machine using NULL Session
 smbclient -L <target-IP>
 
 # List shares on a machine using a valid username + password
 smbclient -L \<target-IP\> -U username%password
 
 # Connect to a valid share with username + password
 smbclient //\<target\>/\<share$\> -U username%password
  
 # List files on a specific share
 smbclient //\<target\>/\<share$\> -c 'ls' password -U username
 
 # List files on a specific share folder inside the share
 smbclient //\<target\>/\<share$\> -c 'cd folder; ls' password -U username
 
 # Download a file from a specific share folder
 smbclient //\<target\>/\<share$\> -c 'cd folder;get desired_file_name' password -U username
  
 # Copy a file to a specific share folder
 smbclient //\<target\>/\<share$\> -c 'put /var/www/my_local_file.txt .\target_folder\target_file.txt' password -U username
 
 # Create a folder in a specific share folder
 smbclient //\<target\>/\<share$\> -c 'mkdir .\target_folder\new_folder' password -U username
 
 # Rename a file in a specific share folder
 smbclient //\<target\>/\<share$\> -c 'rename current_file.txt new_file.txt' password -U username
 
 # enum4linux - General enumeration - anonymous session 
 enum4linux -a \<target\>
 
 # enum4linux - General enumeration - authenticated session
 enum4linux -a \<target\> -u \<user\> -p \<pass\>
 
 # enum4linux - Users enumeration
 enum4linux -u \<user\> -p \<pass\> -U \<target\>
 
 # enum4linux - Group and members enumeration 
 enum4linux -u \<user\> -p \<pass\> -G \<target\>
 
 # enum4linux - Password policy
 enum4linux -u \<user\> -p \<pass\> -P \<target\>
 
 # nmap - Enum Users
 nmap -p 445 --script smb-enum-users \<target\> --script-args smbuser=username,smbpass=password,smbdomain=domain
 nmap -p 445 --script smb-enum-users \<target\> --script-args smbuser=username,smbhash=LM:NTLM,smbdomain=domain
   
 nmap --script smb-enum-users.nse --script-args smbusername=User1,smbpass=Pass@1234,smbdomain=workstation -p445 192.168.1.10
   
 nmap --script smb-enum-users.nse --script-args smbusername=User1,smbhash=aad3b435b51404eeaad3b435b51404ee:C318D62C8B3CA508DD753DDA8CC74028,smbdomain=mydomain -p445 192.168.1.10<br>
 
 # nmap - Enum Groups
 nmap -p 445 --script smb-enum-groups \<target\> --script-args smbuser=username,smbpass=password,smbdomain=domain
 nmap -p 445 --script smb-enum-groups \<target\> --script-args smbuser=username,smbhash=LM:NTLM,smbdomain=domain
 
 # nmap - Enum Shares
 nmap -p 445 --script smb-enum-shares \<target\> --script-args smbuser=username,smbpass=password,smbdomain=domain
 nmap -p 445 --script smb-enum-shares \<target\> --script-args smbuser=username,smbpass=LM:NTLM,smbdomain=domain
 
 # nmap - OS Discovery
 nmap -p 445 --script smb-os-discovery \<target\>
 
 # nmap - SMB Vulnerabilities on Windows
 nmap -p 445 --script smb-vuln-ms06-025 target-IP <br>
 nmap -p 445 --script smb-vuln-ms07-029 target-IP <br>
 nmap -p 445 --script smb-vuln-ms08-067 target-IP <br>
 nmap -p 445 --script smb-vuln-ms10-054 target-IP <br>
 nmap -p 445 --script smb-vuln-ms10-061 target-IP <br>
 nmap -p 445 --script smb-vuln-ms17-010 target-IP <br>
 nmap -p 445 --script smb-vuln-cve-2017-7494 target-IP <br>
 
 -- Always check for updated list on https://nmap.org/nsedoc/scripts/
 
 # map - Brute Force Accounts (be aware of account lockout!)
 nmap –p 445 --script smb-brute –script-args userdb=user-list.txt,passdb=pass-list.txt target-IP
