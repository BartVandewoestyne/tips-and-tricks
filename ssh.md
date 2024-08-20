
# SSH

## Cool commands

To run a script that you have locally on a remote machine:

```text
cat /path/to/local/script | ssh username@remote_host 'bash -s'
```

## Cool configurations

To proxyjump:

```text
Host Texans_jump
   HostName 172.17.221.5
   User root

Host Texans_modem
   ProxyJump Texans_jump
   HostName 192.168.1.96
   User root
```

## Troubleshooting

In case of authentication problems, try

```text
ssh -t -vvv git@bitbucket.org
```

to further diagnose why authentication failed.  See also <https://confluence.atlassian.com/bbkb/permission-denied-publickey-302811860.html>
