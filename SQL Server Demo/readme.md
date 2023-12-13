
# sql-server-ubuntu
Setting up SQL server 2022 on ubuntu

## RUn the below commands 

```
sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/20.04/mssql-server-2022.list)" 

sudo apt install software-properties-common

wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo tee /etc/apt/trusted.gpg.d/microsoft.asc

sudo apt update

sudo apt-get install mssql-server

sudo /opt/mssql/bin/mssql-conf setup
```

2 For developer edition (After selecting dev edition it will ask for pwd generate that pwd from passbolt(Any password generator app password must be strong and keep it somewhere safe) that password we will going to use to connect the database the default username/login will be sa)


## Also setup firwall

```
ufw enable

ufw allow 22

ufw allow 1433

ufw status
```

## create user for ssh and logins

```
useradd rohan_sirohi

<put your pwd>

<reagain type your pwd>

usermod -aG sudo rohan_sirohi (this command will add user in sudo be carefull before using this command)
```

### Try accessing the database from Server management studio or data azure studio default username will be sa








