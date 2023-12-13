# elastic-debian
Setting up elastic on Debian 12

Normal debian updates , user creation and ssh enable

```
apt install gnupg
sudo apt-get install apt-transport-https
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
sudo apt-get update && sudo apt-get install elasticsearch
nano /etc/elasticsearch/jvm.options
```
Add below lines or according to your needs 
> node.name: Coolr-Demo
> 
> network.host: 0.0.0.0
> 
> http.port: 9200
> 
> bootstrap.memory_lock: true
> 
> discovery.type: single-node

```
nano /etc/elasticsearch/elasticsearch.yml
```
Uncheck the below lines and set limit according to your needs 

> -Xms4g
> 
> -Xmx4g




