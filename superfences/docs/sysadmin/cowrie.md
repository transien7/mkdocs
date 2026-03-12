# Cowrie Honeypot

## General usage
The below commands assume the pwd is the cowrie project folder

```
bin/cowrie start                         # start cowrie
ss -ltr                                  # view ports with listening services
bin/cowrie stop                          # stop cowrie
vim etc/cowrie.cfg.dist                  # modify the cowrie config
virtualenv --python=python3 cowrie-env   # create a virtual environment for cowrie
source cowrie-env/bin/activate           # spawn the virtual env in the current shell
deactivate                               # exit the virtual env
cat var/log/cowrie/cowrie.log            # view wthe log file
```

## Remote access
```
ssh root@192.168.50.93 -p2222      # remote ssh on port 2222 (no pass)
telnet 192.168.50.93 2223          # remote telnet on port 2223 (login: root; no pass)
```