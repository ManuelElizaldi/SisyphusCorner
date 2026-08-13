[[SSH]] [[SysAdmin]] [[DevOps]]

Basic connection
ssh manu@100.118.68.64
 
# SSH Keys
Key pairs - public and private keys

public - gets shared

private - your eyes only

*challenge response authentication* -> you use the public key to the server, the server holds the private key and sends back a 'puzzle' that is solved by the private key without exposing the private key 
- this is an over simplification of the process
- this is immune to brute force attacks 

To get the public key and private key you use the command:
```
ssh-keygen
```

![[Pasted image 20250731195033.png]]




---
Source
https://www.youtube.com/watch?v=WwGRGfLy6q8