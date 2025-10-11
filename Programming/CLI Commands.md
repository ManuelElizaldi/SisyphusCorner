2025-03-24
Tags:# [[Programming]], [[Bash]]

Getting the type of linux distribution 
`lsb_release -a`

change owner:
`chown`

show file system disk space in human readable format (-h):
`df -h`


[SCP] Copy from host machine to remote or remote to host:
*remote to host*:
`scp ubuntu@192.168.1.50:/remote/machine/remote_file.txt ~/local/destination`
- if you are using this with a folder you need to add the -r flag for recursive 
*host to remote*
`scp user@remote:/path/to/remote_file.txt /local/destination/`

Doing this when there's a security key like in EC2s:
`scp -i /pem_key.pem -r user@ip.address:folder/location/remote local/path`

General rule -> first argument is the source & second argument is the destination

## Compiling Code C

linux -> `gcc name_of_script.c -o compiled_file_name`

mac -> `clang name_of_script.c -o compliled_file_name`

## Powershell ipconfig
Gives you ip information





---
### Reference