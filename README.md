# Docker-Project
**docker-compose file (two-tier architecture) : ownCloud+MariaDB**

> [ownCloud](https://owncloud.org/) is a file sharing server that puts the control and security of your own data back into your hands. It allows you to run a personal cloud file storage service. It has features that are comparable to other cloud storage services such as Dropbox.

> [MariaDB](https://mariadb.org/https://mariadb.org/) is a community-developed fork of MySQL intended to remain free under the GNU GPL. MariaDB Server is one of the most popular open source relational databases. It’s made by the original developers of MySQL and guaranteed to stay open source. It is part of most cloud offerings and the default in most Linux distributions.

## Getting Started 

Get ready with the following stuff before diving into **docker-compose.yml** file.

## Installing software :

- **Installing docker:**

  - Add the following link to your local repository
 
    `https://download.docker.com/linux/centos/7/x86_64/stable/`

  - run `yum install docker-ce --nobest` to download and install docker community edition (NOTE: If your O.S is RHEL).
  
  - `start` the docker services and `enable` it if docker is required after boot.
  
- **Download MariaDB image:**

  - To download the MariaDB docker image, run:
  
    `docker pull mariadb`
    
- **Download owncloud image:**

  - To download the owncloud docker image, run:
    
    `docker pull owncloud`
    
(Tip: You can run `docker images` to see all the downloded docker images)

- **Installing docker-compose:**

  - Head to the [link](https://docs.docker.com/compose/install/). It will guide you to download and install docker-compose.

- **Installing httpd**

  - Go to the following [link](http://httpd.apache.org/docs/2.4/install.html) to download and install httpd. You can configure `httpd.conf` file.
  
## Running the docker-compose :

Create a directory and paste the given `docker-compose.yml` file into the directory. In the Terminal, head to the directory and run:

> `docker-compose up -d`

❗ Here `-d` is an option to run docker in background. You can omit it if not required. ❗

## Initial Setup :

- Go to browser and enter the link: `http://0.0.0.0:8080` or `http://ServerName:8080`. You will be directed to owncloud-web-server.

- Enter the credentials as in the below screenshot :

![screenshot](https://github.com/asks1012/Docker-Project/blob/master/images/Screenshot%20from%202020-05-02%2011-48-38.png)

🛑 Note: The above screenshot consisting login credentials is just a sample. It is highly recommended to edit the `docker-compose.yml` file and use your own personalised login and password. 🛑

```
If you get something like "ERROR CONNECTING TO DATABASE....", just stop the firewall and reload the page!
```

- After that, login with owncloud admin username and password **to enter your personal owncloud server** where you can share, upload the files on your pc. You can also connect to the server with the owncloud mobile app.

- Screenshot of login page :

![login page](https://github.com/asks1012/Docker-Project/blob/master/images/Screenshot%20from%202020-05-02%2011-50-25.png)

- Finally, you will be redirected to the home page of owncloud server as in the below image :

![home page](https://github.com/asks1012/Docker-Project/blob/master/images/Screenshot%20from%202020-05-02%2011-50-52.png)

## Connecting to the database remotely from host :

- For this, you need to install `mysql` and `mariadb` software on the host o.s of docker.

  > **Note:** mysql and mariadb are conflicting packages. You need to enter `--allowerasing` option to overcome the issue.
  
- Run the following and find the IP address of mariadb container:

  > docker inspect `CONTAINER ID of mariadb`

- Run the following to connect to the mariadb database remotely :

  > mysql -h `IP of mariadb` -u `username of mariadb` -p`password of mariadb`

- If your mariadb is correctly working, you will be redirected to `mariadb shell` and you can run sql commands like `show databases;`, `show tables;`, `exit;`  etc.,

### Screenshot of MariaDB shell:

![MariaDB shell](https://github.com/asks1012/Docker-Project/blob/master/images/Screenshot%20from%202020-05-02%2010-57-19.png)

## Alternative :
If you don't want to use `docker-compose`, you can run the following two commands to get your owncloud server :

> docker run -dit -e MYSQL_ROOT_PASSWORD=10122001 -e MYSQL_USER=username -e MYSQL_PASSWORD=password -e MYSQL_DATABASE=mydb -v mysql_volume:/var/lib/mysql --name dbos mariadb:latest

> docker run -dit -e OWNCLOUD_DOMAIN=sagardomain -e OWNCLOUD_DB_TYPE=mysql -e OWNCLOUD_DB_NAME=mydb -e OWNCLOUD_DB_USERNAME=username -e OWNCLOUD_DB_PASSWORD=password -e OWNCLOUD_DB_HOST=dbos -e OWNCLOUD_ADMIN_USERNAME=username -e OWNCLOUD_ADMIN_PASSWORD=password -v owncloud_volume:/var/www/html/owncloud --name owncloud_os -p8080:80 --link dbos:owncloud-db owncloud:latest

## Author :

  > A.Sri Krishna Sagar
  
  > Gmail: asks1012@gmail.com
  
  > https://www.linkedin.com/in/akurathi-sri-krishna-sagar-5aa653190?lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_contact_details%3B0QCHt6GHT8yDSIOHr590Vg%3D%3D


💯𝓨𝓸𝓾 𝓐𝓻𝓮 𝓓𝓸𝓷𝓮
