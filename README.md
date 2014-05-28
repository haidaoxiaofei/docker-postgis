# docker-postgis

A simple docker container that runs PostGIS

**Note:** We recommend using ``apt-cacher-ng`` to speed up package fetching -
you should configure the host for it in the provided 71-apt-cacher-ng file.

## Build

To build the image without apt-cacher do:

```
docker build -t kartoza/postgis git://github.com/timlinux/docker-postgis
```

To build with apt-cache do you need to clone this repo locally first and 
modify the contents of 71-apt-cacher-ng to match your cacher host. Then 
build using a local url instead of directly from github.

```
git clone git://github.com/timlinux/docker-postgis
```

Now edit ``71-apt-cacher-ng`` then do:

```
docker build -t kartoza/postgis .
```

## Run


To create a running container do:

```
sudo docker run --name "postgis" -p 2222:22 -p 25432:5432 -d -t kartoza/postgis
```

## Connect via psql

To log in to your container do:

Connect with psql (make sure you first install postgresql client tools on your
host / client):


```
psql -h localhost -U docker -p 25432 -l
```

**Note:** Default postgresql user is 'docker' with password 'docker'.

You can then go on to use any normal postgresql commands against the container.

Under ubuntu 14.04 the postgresql client can be installed like this:

```
sudo apt-get install postgresql-client-9.3
```


## Storing data on the host rather than the container.


Docker volumes can be used to persist your data.

```
mkdir -p ~/postgres_data
docker run -d -v $HOME/postgres_data:/var/lib/postgresql kartoza/postgis`
```

You need to ensure the ``postgres_data`` directory has sufficinet permissions
for the docker process to read / write it.



## Connect via ssh

To log into your container do:

```
ssh root@localhost -p 2222
```

Default ssh password is 'postgis'


## Credits

Tim Sutton (tim@linfiniti.com)
May 2014
