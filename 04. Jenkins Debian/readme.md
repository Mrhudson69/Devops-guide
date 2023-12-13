# jenkins-debian
How to install jenkis on debian container proxmox

```
sudo apt update
sudo apt install fontconfig openjdk-17-jre
java -version
openjdk version "17.0.8" 2023-07-18
OpenJDK Runtime Environment (build 17.0.8+7-Debian-1deb12u1)
OpenJDK 64-Bit Server VM (build 17.0.8+7-Debian-1deb12u1, mixed mode, sharing)
```

```
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

```
systemctl edit jenkins
```

Add below lines

> [Service]
> 
> #Arguments for the Jenkins JVM
> 
> Environment="JAVA_OPTS=-Xmx2048M -Djava.awt.headless=true"

```
systemctl daemon-reload
sudo nano /etc/default/jenkins
```

Add below line (Allocate RAM according to your needs)

> JAVA_ARGS="-Djava.awt.headless=true -Xmx2048m -Xms2048m"

## Done that's all for setting up jenkins on a debian container


