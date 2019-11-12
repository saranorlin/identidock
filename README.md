#identidock

Simple identicon server based on monsterid from Kevin Gaudin.

From "Using Docker" by Adrian Mouat.

To launch `identidock` using docker-compose (after completing Chapter 6):
1) `docker-compose build` for the DEV version of `docker-compose -f prod.yml up` for the PROD version
2) `docker-compose up`
3) To stop the container(s): `docker-compose stop


To launch `identidock` using the deploy.sh script with DigitalOcean
1) Export your DigitalOcean `TOKEN` in your bash profile
2) `docker-machine create --drive digitalocean --digitalocean-access-token $TOKEN identihost-do`
3) Run `docker-machine ip identihost-do` and replace the IP address in the deploy.sh script
4) Add an HTTP firewall inbound rule in the DigitalOcean GUI.
5) `docker-machine scp deploy.sh identihost-do:~/deploy.sh`
6) `docker-machine ssh identihost-do`
7) `chmod +x deploy.sh`
8) `./deploy.sh`


To set up Jenkins (after completing Chapter 8):
1) Navigate to the `identijenk` folder locally
2) Build the Jenkins container: `docker build -t identijenk .`
3) Run the container this way: `docker run --name jenkins-data identijenk echo "Jenkins Data Container"`
4) Then run the container this way: `docker run -d --name jenkins -p 8080:8080 --volumes-from jenkins-data -v /var/run/docker.sock:/var/run/docker.sock identijenk`
5) Navigate to http://localhost:8080
6) Set up a new Jenkins job that pulls Git source code from `https://github.com/saranorlin/identidock` (public repo, no authentication needed). Locally in the `identijenk` folder, open the .sh file starting with `jenkins`. Copy the full text in the .sh script container in the Jenkins job. Run the job.
7) To backup the latest Jenkins or to use the last backup, see pg 132.