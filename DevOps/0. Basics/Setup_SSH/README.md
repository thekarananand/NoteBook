# How to Setup SSH on Remote Host

Install `openssh-server` on Remote Host
```
sudo dnf install openssh-server -y
```

Start & Enable `sshd.service`
```
sudo systemctl start sshd.service
sudo systemctl enable sshd.service
```
