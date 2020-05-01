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

![screenshot](https://github.com/asks1012/Docker-Project/blob/master/Screenshot%20(140).png)

🛑 Note: The above screenshot consisting login credentials is just a sample. It is highly recommended to edit the `docker-compose.yml` file and use your own personalised login and password. 🛑

```
If you get something like "ERROR CONNECTING TO DATABASE....", just stop the firewall and reload the page!
```

- After that, login with owncloud admin username and password **to enter your personal owncloud server** where you can share, upload the files on your pc. You can also connect to the server with the owncloud mobile app.

## Connecting to the database remotely :

- For this, you need to install `mysql` and `mariadb` software on the host o.s of docker.

  > **Note:** mysql and mariadb are conflicting packages. You need to enter `--allowerasing` option to overcome the issue.
  
- Run `docker inspect *CONTAINER ID of mariadb*` and find the IP address of mariadb container.

- Run `mysql -h *IP of mariadb* -u ***username of mariadb*** -p***password of mariadb***` to connect to the mariadb database remotely.

- Now you can run `mysql shell` commands.
