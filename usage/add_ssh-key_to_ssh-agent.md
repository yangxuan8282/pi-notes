```
echo "eval $(ssh-agent -s)
ssh-add ~/.ssh/id_rsa" | tee --append ~/.bashrc
```

```
chmod 600 ssh-add ~/.ssh/id_rsa
```