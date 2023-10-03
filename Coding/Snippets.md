
## Find broken symlinks
```bash
find . -xtype l
```

## Fix Docker `iptables`  NAT error #docker
### Error message
```
failed to start daemon: Error initializing network controller: error obtaining controller instance: failed to create NAT chain DOCKER: iptables failed: iptables -t nat -N DOCKER: iptables v1.8.7 (nf_tables): Could not fetch rule set generation id: Invalid argumen
```
### Solution
```
# On the orin
sudo update-alternatives --set iptables /usr/sbin/iptables-legacy
sudo reboot
```

## Commit with a specific date
```
GIT_COMMITTER_DATE="Mon 20 Aug 2018 20:19:19 BST" git commit --amend --no-edit --date "Mon 20 Aug 2018 20:19:19 BST"
```

# Fixing diamond inheritance #cpp

https://www.scaler.com/topics/cpp/multiple-inheritance-in-cpp/