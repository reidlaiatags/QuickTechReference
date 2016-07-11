# Use SSH agent

## Start SSH agent

```
eval $(ssh-agent)
```

## Add public key to SSH agent

```
ssh-add 
```

## Import public key to host

```
ssh-copy-id "usenrame@hostname -p port"
```


## Connect to remote host
```
ssh -A -p port username@hostname
```