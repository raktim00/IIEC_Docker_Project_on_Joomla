# IIEC_Docker_Project_on_Joomla
Under IIEC-RISE 1.0 Campaign I learnt about Docker under the guidance of Vimal Daga Sir. This is my final project using Docker to set-up a WebApp called **Joomla**.
## I am going to explain the whole set-up process in this documentation.
## 1. Pre-configurations needed:
* I am using **RedHat Enterprise Linux**. Plus I have also installed Docker Software in it. You can use any OS and inside that OS you should have docker software installed. There might be a possibility that some Linux command might be different from other OS but I will explain what is the work of that command.
## 2. Setting up the required things:
* Disabling firewall:
  * Firewall might block some networking stuffs that's why I at first stopped the firewall.
  * Use `systemctl stop firewalld`.
* Starting the docker:
  * Use `systemctl start docker` to start Docker Service.
## 3. Downloading required images:
* Pulling MySQL Image:
  * Use `docker pull mysql:5.6` to download the **mysql version 5.6** image to use as a database server.
  * To know more about MySQL Image go to this page: https://hub.docker.com/_/mysql
* Pulling Joomla Image:
  * Use `docker pull joomla:3.9-php7.2-apache` to download the Joomla Image in which php and apache server is already preconfigured.
  * To know more about Joomla Image go to this page: https://hub.docker.com/_/joomla
  
![Docker Pull Commands](Screenshots/docker-pull.png)
## 4. Setting up MySQL:
* Use `docker run -it -e  MYSQL_ROOT_PASSWORD=(any password you like) -e MYSQL_USER=(any user name) -e MYSQL_PASSWORD=(any password(recommended not to use root password) -e MYSQL_DATABASE=(any database name) --name joomladb mysql:5.6` this code and it will create a user with a database inside Your MySQL Server.

![MySQL Server Setup](Screenshots/mysql-setup.png)

* Now if you want to see is your database created or not then you have to install **MySQL cilent software** in your base OS. For that use `yum install mysql`. Next thing check your database server ip address and use that ip while running the client software. For reference check the image below.

![MySQL client](Screenshots/mysql-client.png)

## 5. Docker-Compose:
  * Before using Docker-Compose you should install the software. For reference go to this website : https://docs.docker.com/compose/install/
  * You can create and edit this file using vim editor. For that use `vim docker-compose.yml`. Remember the file name should always be **docker-compose.yml**.
  * In the below picture you can see the composed file. Let me tell you how it's done.
![Docker Compose](Screenshots/yml-file.png)

### version:
   * In each version the style and syntax are different. I used version 3 cause it's easy to compose than other versions.
### services:
   * In docker compose we use the term services to rectify which things will run when we start the compose file.
### container name:
   * **joomlaos** and **joomladb** are the name of the containers which will be setup. Docker-compose automatically creates the name for the containers using our defined container name. We just only have to tell that these containers we are using.
### image and restart:
   * **image** and **restart** these two key is used to specify which image we want to use and due to any reason if any of the container stops docker-compose will again restart it.
### volumes:
   * In docker as soon as we terminate an container our whole data inside that container destroyed. But if we want to make our data permanent then we have to use **docker volume**. We know that MySQL and Joomla stores their data inside which folder. We simply make those folders permanent by using volumes. That means due to any reason if our container terminated our data will not loose.
### environment:
   * There are many images in Docker which needs some pre-defined environment variables to run. That's why we need to pass these variables. One small thing to notice that in **joomlaos** I used **joomladb:3306** as host cause Joomla use this port number to connect with the host.
### depends_on and ports:
   * As we know Joomla needs MySQL database server to store there files that's why we are using **depends_on**. Also we know that we have to expose our container(where joomla running) to a specific port otherwise from outside world we will not be able to access our WebApp.
   
## 6. Docker-compose up:
  * As per the below mentioned picture use `docker-compose up` to complete the setup.
![Docker Compose Up](Screenshots/Docker-compose-up.png)
## 7. Joomla Started:
  * Got to your browser and type `localhost:80` and done you will be able to see your Joomla WebApp. Now one small suggestion that you can use directly `localhost` without typing the port cause in http apache server our browser by default use the port 80. But if you want to use any other port then you have to mention it in your docker-compose file.
![Joomla Web Page](Screenshots/joomla-webpage.png)
## 8. Docker-compose start stop:
   * After using docker compose up now in one click you can stop your whole setup. Just use `docker-compose stop`. Again you want to start the service use `docker compose start`. 
![Docker-compose-start-stop](Screenshots/Docker-compose-start-stop.png)
## 9. Docker-compose down:
  * You can easily remove the containers using `docker compose down` command.
  
## Future possibilities:
   ### This whole setup is done in local machine. But exactly same thing we can do in cloud to setup a Joomla WebApp. We can use many cloud services like Google Cloud, Digital Ocean etc. for this.
   
## References:
  ### I learnt this technology totall free of cost in YouTube. What I learnt are mentioned in the below screenshots.
  Here is the YouTube playlist : https://www.youtube.com/playlist?list=PLAi9X1uG6jZ30QGz7FZ55A27jPeY8EwkE
### Session 1 Feedback: 
![Docker Session 1](Screenshots/Docker%20Session1.png)
### Session 2 Feedback: 
![Docker Session 2](Screenshots/Docker%20Session2.png)
### Session 3 Feedback: 
![Docker Session 3](Screenshots/Docker%20Session3.png)
### Session 4 Feedback: 
![Docker Session 4](Screenshots/Docker%20Session4.png)
### Session 5 Feedback: 
![Docker Session 5](Screenshots/Docker%20Session5.png)
### Session 6 Feedback: 
![Docker Session 6](Screenshots/Docker%20Session6.png)

## Lastly Thank you so much Vimal Daga Sir.
