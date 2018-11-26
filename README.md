This is a list of useful commands/tricks using smbclient and nmap smb scripts - very useful on a pentesting
https://sharingsec.blogspot.com

# List shares on a machine using NULL Session
 smbclient -L target-IP 
 
 # List shares on a machine using a valid username + password
 smbclient -L target-IP -U usernmame%password
 
 # List files on a specific share
 smbclient //target-IP/share$ -c 'ls' password -U username
 
 # List files on a specific share folder inside the share
 smbclient //target-IP/share$ -c 'cd folder; ls' password -U username
 
 # Download a file from a specific share folder
 smbclient //target-IP/share$ -c 'cd folder;get desired_file_name' password -U username
  
 # Copy a file to a specific share folder
 smbclient //target-IP/share$ -c 'put /var/www/my_local_file.txt .\target_folder\target_file.txt' password -U username
 
 # Create a folder in a specific share folder
 smbclient //target-IP/share$ -c 'mkdir .\target_folder\new_folder' password -U username
 
 # Rename a file in a specific share folder
 smbclient //target-IP/share$ -c 'rename current_file.txt new_file.txt' password -U username
 
 # nmap - Enum Users
 nmap -p 445 --script smb-enum-users target-IP --script-args smbuser=username,smbpass=password
 
 # nmap - Enum Groups
 nmap -p 445 --script smb-enum-groups target-IP --script-args smbuser=username,smbpass=password
 
 # nmap - Enum Shares
 nmap -p 445 --script smb-enum-shares target-IP --script-args smbuser=username,smbpass=password
 
 # nmap - OS Discovery
 nmap -p 445 --script smb-os-discovery target-IP
 
 # nmap - SMB Vulnerabilities on Windows
 nmap -p 445 --script smb-os-discovery target-IP smb-vuln-ms06-025<br>
 nmap -p 445 --script smb-os-discovery target-IP smb-vuln-ms07-029<br>
 nmap -p 445 --script smb-os-discovery target-IP smb-vuln-ms08-067<br>
 nmap -p 445 --script smb-os-discovery target-IP smb-vuln-ms10-054<br>
 nmap -p 445 --script smb-os-discovery target-IP smb-vuln-ms10-061<br>
 nmap -p 445 --script smb-os-discovery target-IP smb-vuln-ms17-010<br>
 -- Always check for updated list on https://nmap.org/nsedoc/scripts/
 
 # map - Brute Force Accounts (be aware of account lockout!)
 nmap –p 445 --script smb-brute –script-args userdb=user-list.txt,passdb=pass-list.txt target-IP
  
  
