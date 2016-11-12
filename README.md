# ansible-exoscale
Some ansible playbooks to manage the things

## How to get started
1. Generate your first instance at exoscale.ch (I use debian Linux)
2. Login with you SSH Keypair, as root
3. execute the following commands :

### Update your machine and allow unattended upgrades
`apt-get update && apt-get dist-upgrade -y`

```
dpkg-reconfigure --priority=low unattended-upgrades
service unattended-upgrades restart
```

### Install git, ntp and fail2ban
`apt-get install git ntp fail2ban -y`

### Configure your time zone
`echo "Europe/Zurich" | tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata`

### Configure git
```
git config --global user.email <insert your email address here
git config --global user.name "<insert your full name here>"
```

### Clone the repo with the .dot_files and some configuration
`git clone git@github.com:SebastienPittet/config-files.git`

### Apply the configuration needed
```sh
cd config-files
cp .bash* ~
cp ./etc/ssh/* /etc/ssh/
cp ./etc/fail2ban/* /etc/fail2ban/
cp ./etc/ntp.conf /etc/

service sshd restart
service fail2ban restart
service ntp restart
```

# Install ansible
```sh
easy_install pip
pip install ansible
```

### Clone the current repo
```sh
git clone git@github.com:SebastienPittet/ansible-exoscale.git
cd ansible-exoscale
ansible-playbook create-web-server
```





