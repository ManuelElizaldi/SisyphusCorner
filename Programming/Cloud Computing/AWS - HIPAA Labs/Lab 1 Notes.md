Had to install the new version of awscli, for this I had to remove it and then re install it. 

When checking the version of the software after installing I got this error:

```
manu  /tmp  aws --version
bash: /usr/bin/aws: No such file or directory

```

I had to add aws to the PATH, but that was not the fix, the fix was simpler, I only needed to clear the cache, because bash was still looking for the removed path. We had to reset the cache with:

`hash -r`

you can use \rm to bypass any aliases

We create an additional user inside the AWS account so that it has isolated permission. 
- one example of this is not granting it AWS management console. We only need CLI for this lab. 
- Also, we only grant Admin access (AdministratorAccess).


## Attaching policies directly 
We are only going to give this account the permissions it needs. 
- AdministratorAccess

We also create keys for this 


