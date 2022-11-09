# AspNetCoreWithKubernetes

How to test locally

1. Open the project in visual studio
2. Run the project 
3. Then access it using this link
   http://localhost:5295/WeatherForecast

How to test using docker

Preparation for using Docker and Kubernetes

1. Create an account in docker hub (https://hub.docker.com/)
2. build your own docker image
  docker build -t [name of your image:v1.0.0]

3. link your newly build docker image to your dockerhubimage
   docker tag [name-of-your-image:v1.0.0] [yourdockerhub/name-of-your-image:v1.0.0]

4. push your new docker image to your docker hub 
   docker push [yourdockerhub/name-of-your-image:v1.0.0]

Testing Docker

1. open the command line
2. Run it using docker command
   docker run -it --rm -p 8080:80 [yourdockerhub/name-of-your-image:v1.0.0]
3. Access it using this link
   http://localhost:8080/WeatherForecast
4.  docker ps, then docker stop the running image

Testing Kubernetes

1. make sure no one is using port 8080 to make this work

Check if 8080 port is in used in windows
  netstat -aon | findstr 8080
  
kill the process who use it
  taskkill /f /pid [id of process]

2. Replace the docker image in Deployment.yml with your Docker image [yourdockerhub/name-of-your-image:v1.0.0]

3. open command line in the root project run this command
   kubectl apply -f Deployment.yml

4. run this command
   kubectl apply -f Service.yml
   
5. access the api using this url
   http://localhost:8080/WeatherForecast
