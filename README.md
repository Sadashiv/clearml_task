Docker and Docker-cmpose should be installed already

sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

echo "vm.max_map_count=262144" > /tmp/99-clearml.conf
sudo mv /tmp/99-clearml.conf /etc/sysctl.d/99-clearml.conf
sudo sysctl -w vm.max_map_count=262144
sudo service docker restart

sudo mkdir -p /opt/clearml/data/elastic_7
sudo mkdir -p /opt/clearml/data/mongo/db
sudo mkdir -p /opt/clearml/data/mongo/configdb
sudo mkdir -p /opt/clearml/data/redis
sudo mkdir -p /opt/clearml/logs
sudo mkdir -p /opt/clearml/config
sudo mkdir -p /opt/clearml/data/fileserver

sudo chown -R 1000:1000 /opt/clearml


sudo curl https://raw.githubusercontent.com/allegroai/clearml-server/master/docker/docker-compose.yml -o /opt/clearml/docker-compose.yml

export CLEARML_HOST_IP=192.168.0.102
export CLEARML_AGENT_GIT_USER=
export CLEARML_AGENT_GIT_PASS=
sudo  docker-compose -f /opt/clearml/docker-compose.yml up -d
docker image ls
docker container ls
