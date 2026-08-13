`ssh-keygen -t ed25519 -C "manuel-macbook"`

-C stands for comment 
ed25519 algorithm to generate secure keys  
-t stands for type. There are several types of key algorithms , rsa was another one that was used but ed25519 is the standard today 

save in default location -> /Users/manuelelizaldi/.ssh/id_ed25519

then asked for a passphrase -> this will protect the file itself. This is optional, for home use it is not necessary, for more advanced systems it is recommended 
- password for the encrypted file 

randomart image is generated -> successful build of key 
- the randomart image is -> pattern recognition for humans. 
- randomart image is a fingerprint of your key | visual representation 
- generated with the The Drunken Bishop algorithm 

##### Note -> if you want to see the randomart everytime you login you have to edit the nano ~/.ssh/config file to include:
```
Host * VisualHostKey yes
```
- Host * just makes is so that this applies to any server you login 




Then we copy the ssh id to the raspberrypi with the following command `ssh-copy-id <username>@<ip_address>`
- you create the ID when you run the ssh-keygen command 
	- - **The Private Key (`id_ed25519`):** This is your actual ID card. It stays on your Mac.
    
	- **The Public Key (`id_ed25519.pub`):** This is the public record of your ID. This is what you give to the server.
- the command `ssh-copy-id` is a script that saves you manual work of saving the public key in the raspberry pi  inside the folder .ssh and a folder inside that named authorized keys 


Doing `ls -l ~/.ssh` in the command line can show you both the id and public id 
-l is long format, which includes extra info like permissions, format, etc. 



