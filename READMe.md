## Sensu playground

* read -s user
* read -s pw
* user=$user pw=$pw docker-compose up -d
    * starts your sensu playground, available at http://localhost:3000
* docker-compose -f docker-compose-cli.yaml build --build-arg user=$user --build-arg pw=$pw
* alias sensuctl="docker run -it sensu-cli sensuctl" 
    * runs sensuctl from within a separate container, no need for local install