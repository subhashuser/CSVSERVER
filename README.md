# CSVSERVER
1) Create a solutions directory: 
  mkdir solutions
  cd solutions/
2) Check if docker and docker-compose are installed:
  docker version
  docker-compose version
3) Pull the specified docker images:
  docker pull infracloudio/csserver:latest
  docker pull prom/prometheus:v2.22.0
4) Clone the specified repo:
  git clone https://github.com/infracloudio/csvserver.git
5) List the pulled docker images:
  docker images
6) Run the docker container:
  docker run -d -i infracloudio/csvserver:latest
7) Check if the docker container is running or not:
  docker ps
8) If the docker container is not running, check the status:
  docker ps -a
9)Check the logs and see what is the error
10) Write a shell script gencsv to generate csv content and write it to inputFile file:
  #!/bin/bash
  for i in {0..9}
  do
  echo "$i,$RANDOM" >> inputFile
  done
11) Run the cotainer by mouting the inputfile path:
   docker run -d -i -v /root/solutions/inputFile:/csvserver/inputdata infracloudio/csvserver:latest
12) Login to the container:
  docker exec -it <container-id> bash
13) Check the port:
  netstat -tulnp
14) Stop the running container:
  docker stop <container-id>
15) Run the container and provide the port mapping:
  docker run -d -i -v /root/solutions/inputFile:/csvserver/inputdata -p 9393:9300 infracloudio/csvserver:latest
16) Stop the container:
  docker stop <container-id>
17) Run again by specifying the environment variable:
  docker run -d -i -v /root/solutions/inputFile:/csvserver/inputdata -p 9393:9300 -e CSVSERVER_BORDER='Orange' infracloudio/csvserver:latest
18) Commit and push the changes to your repository on GitHub. And then Add a docker-compose.yaml file
19) Copy inputFile to inputdata at /csvserver/inputdata by mounting it as a volume
20) Add services for csvapp and prometheus
21) Copy prometheus config to /etc/prometheus/ directory by mounting it as a volume
22) Run docker-compose up (make sure to run it in the directory where docker-compose.yaml is available)
23) open solutions directory and run the curl wget -o ./part-1-output http://localhost:9393/raw
24) In the same directory, run docker logs command to get csvapp container's logs docker logs [container_id] >& part-1-logs
25) Commit and push the changes to your repository on GitHub
26) Delete any containers running
27) Add Prometheus container (`prom/prometheus:v2.22.0`) to the docker-compose.yaml 
28) Make sure that Prometheus is accessible at http://localhost:9090 on the host.
29) Type `csvserver_records` in the query box of Prometheus. Click on Execute and then switch to the Graph tab.
30) The Prometheus instance should be accessible at http://localhost:9090, and it should show a straight line graph with value 10.
