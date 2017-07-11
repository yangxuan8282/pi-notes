```
sudo fallocate -l 1024M /swapfile &&
sudo chmod 600 /swapfile &&
sudo mkswap /swapfile &&
sudo swapon /swapfile &&
echo "/swapfile none swap defaults 0 0" | sudo tee --append /etc/fstab
```