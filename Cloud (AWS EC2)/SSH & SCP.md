
### Connect to instance using SSH
```
ssh -i /path/key-pair-name.pem ubuntu@instance-public-dns-name
```

### Using SCP to transfer files between local and instance
1. Transfer a file to instance
```
scp -i /path/key-pair-name.pem /path/my-file.txt ubuntu@instance-public-dns-name:path/
```
2. Transfer a file from instance to local computer
```
scp -i /path/key-pair-name.pem ubuntu@instance-public-dns-name:path/my-file.txt local-path/my-file2.txt
```
