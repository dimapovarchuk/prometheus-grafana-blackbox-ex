# Prometheus-Grafana-Blackbox-exporter
### Create install.sh script for deploy "Prometheus-Grafana-Blackbox-exporter"
        #!/bin/sh
        apt-get update

        if ! type "docker" > /dev/null; then
          echo "Installing Docker"
          apt-get -y install docker.io
          apt-get -y install docker-ce
        fi

        ADDRESS=$(ifconfig eth0 | grep 'inet addr:' | cut -d: -f2 | awk '{ print $1}')
        docker swarm init --advertise-addr="$ADDRESS"

        if ! type "git" > /dev/null; then
          echo "Installing Git"
          apt-get -y install git
        fi

        DIRECTORY="prometheus-grafana-alertmanager-example"
        if [ -d "$DIRECTORY" ]; then
          rm -rf "$DIRECTORY"
        fi
        echo "Cloning Project"
        git clone https://github.com/PagerTree/prometheus-grafana-alertmanager-example.git
        cd "$DIRECTORY"

        echo "Making Utility scripts executable"
        chmod +x ./util/*.sh

        echo "Starting Application"
        docker stack deploy -c docker-compose.yml prom

        echo "Waiting 5 seconds for services to come up"
        sleep 5

        while docker service ls | grep "0/1";  do sleep 3; echo "Waiting..."; done;

        echo "You can now access your Grafana dashboard at http://$ADDRESS:3000"

### Create EC2 instance for deploy "Prometheus-Grafana-Blackbox-exporter"
<img width="960" alt="image" src="https://user-images.githubusercontent.com/52627259/234774230-de6ce735-31d3-48f6-8be5-2ed9a3d2f084.png">

### Create Jenkins EC2 instance for deploy "Prometheus-Grafana-Blackbox-exporter"
<img width="960" alt="image" src="https://user-images.githubusercontent.com/52627259/234775626-515282fd-309f-4411-9590-f48c37d39a73.png">

### Create Jenkins pipeline for deploy "Prometheus-Grafana-Blackbox-exporter"
<img width="905" alt="image" src="https://user-images.githubusercontent.com/52627259/234776955-56f3a521-e31b-4e66-96b9-e8ad97f46a23.png">

### Run Jenkins pipeline for deploy "Prometheus-Grafana-Blackbox-exporter"
<img width="904" alt="image" src="https://user-images.githubusercontent.com/52627259/234777530-8f8f82d6-8a49-490f-a1fe-1310b25f32bd.png">
<img width="911" alt="image" src="https://user-images.githubusercontent.com/52627259/234777868-007b581d-314b-4bb2-ad6b-3626d9e6b219.png">

### Cheking Prometheus monitoring service
<img width="960" alt="image" src="https://user-images.githubusercontent.com/52627259/234778333-1173faa0-1b57-4d44-924a-b4d18752d5d1.png">

### Cheking Grafana dashboard service
<img width="960" alt="image" src="https://user-images.githubusercontent.com/52627259/234778427-c70c4265-9cb2-47b8-b88b-386324c23829.png">

### Cheking Blackbox Exporter service
<img width="960" alt="image" src="https://user-images.githubusercontent.com/52627259/234778901-b4a50d9e-608f-403b-95e0-6f3bb94e4f8d.png">

### Cheking Node Exporter service
<img width="956" alt="image" src="https://user-images.githubusercontent.com/52627259/234779092-456b9aee-1ed3-44c2-a901-29b161845dc3.png">

### Cheking Alertmanager service
<img width="960" alt="image" src="https://user-images.githubusercontent.com/52627259/234779144-97b9032f-f94d-4699-910b-ccd79e89d636.png">






