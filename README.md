Implementations CNE 370 Real world final project.
this is the reall world projet builed an app in docker-compose that se up a sharded database using Maxscale server that runing in two master server Maxscale_maser_1 and  Maxscale_maser_2

## Ubuntu terminal and installing the docker community edition

sudo apt update

 sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg |sudo apt-key add -


sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"

 sudo apt update
 
 sudo apt install docker-ce



## check docker status with should enalbe 

sudo systemctl status docker.

## configured  Docker Compose, MariaDB
 sudo apt install docker-compose.
 
 sudo apt install MariaDB-client.


#### docker-compose up -d
khalid@ubuntu0:~/reall_world/maxscale-docker/maxscale$ sudo docker-compose up

Creating network "maxscale_default" with the default driver

Pulling master (mariadb:10.3)...

10.3: Pulling from library/mariadb

5544ebdc0c7b: Pull complete


##Set up and clone maxscale-docker repository 
khalid@ubuntu0:~/reall_world$     git clone https://github.com/Zohan/maxscale-docker.git

Cloning into 'maxscale-docker'...

remote: Enumerating objects: 222, done.

remote: Counting objects: 100% (3/3), done.

remote: Compressing objects: 100% (3/3), done.

remote: Total 222 (delta 0), reused 1 (delta 0), pack-reused 219

Receiving objects: 100% (222/222), 40.51 KiB | 505.00 KiB/s, done.

Resolving deltas: 100% (113/113), done.

### to run the docker-compose up you must be in right directory "maxscale-docker/maxscale"
docker-compose up -d
Starting maxscale_master_1 ... done
Starting maxscale_master2_1 ... done
Starting maxscale_maxscale_1 ... done




### show the status is up 
 khalid@ubuntu0:~/reall_world/maxscale-docker/maxscale$ sudo docker-compose up -d

maxscale_master_1 is up-to-date

maxscale_slave2_1 is up-to-date

maxscale_slave1_1 is up-to-date

maxscale_maxscale_1 is up-to-date







## Now edit the docker-compose.yml in maxscale directory

nano docker-compose.yml

Edit the example.cnf file inside the maxscale.cnf.d file

nano example.cnf

once the example.cnf file edited, create SQL shard files inside the master directory

/maxscale/maxscale-docker/maxscale/sql/master#

Use the following command to list the servers

$ docker-compose exec maxscale maxctrl list servers
┌─────────┬─────────┬──────┬─────────────┬─────────────────┬──────────┐
│ Server  │ Address │ Port │ Connections │ State           │ GTID     │
├─────────┼─────────┼──────┼─────────────┼─────────────────┼──────────┤
│ server1 │ master  │ 3306 │ 0           │ Master, Running │ 0-3000-5 │
├─────────┼─────────┼──────┼─────────────┼─────────────────┼──────────┤
│ server2 │ slave1  │ 3306 │ 0           │ Slave, Running  │ 0-3000-5 │
├─────────┼─────────┼──────┼─────────────┼─────────────────┼──────────┤
│ server3 │ slave2  │ 3306 │ 0           │ Running         │ 0-3000-5 │
└─────────┴─────────┴──────┴─────────────┴─────────────────┴──────────┘


 the bellow command to access databases:

mariadb -umaxuser -pmaxpwd -h 127.0.0.1 -P 4000

Refrences Dr. Zak recoded videos https://rtc.instructure.com/courses/2311463/modules/items/70372910 

https://docs.docker.com/compose/install/

https://github.com/Zohan/maxscale-docker

https://mariadb.com/kb/en/mariadb-maxscale-25-simple-sharding-with-two-servers/


