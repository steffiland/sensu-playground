## Sensu playground

```bash
# set admin user and pw for playground
read -s user
read -s pw

# start your sensu playground, will be available at http://localhost:3000
user=$user pw=$pw docker-compose up -d

# run sensuctl from within a separate container, no need for local install
user=$user pw=$pw docker-compose -f docker-compose-cli.yaml build
#----> OR set backendurl, default is http://host.docker.internal:8080
backendurl=http://sensu-backend:8080 user=$user pw=$pw docker-compose -f docker-compose-cli.yaml build
alias sensuctl="docker run -it sensu-cli sensuctl" 

# test connection
sensuctl cluster id
sensuctl cluster health

# start playin'
sensuctl asset add sensu/monitoring-plugins:2.2.0-1
sensuctl check create ntp --runtime-assets "sensu/monitoring-plugins" \
  --command "check_ntp_time -H time.nist.gov --warn 0.5 --critical 1.0" \
  --command "check_ntp_time -H time.nist.gov --warn 0.5 --critical 1.0" \
  --publish="true" --interval 30 --timeout 10 --subscriptions linux
```