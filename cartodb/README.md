CartoDB
=======

### Overview

[CartoDB](cartodb.com) Is an excellent map maker based on open source
technologies. They release their product as an open source project if you're
willing to host it yourself (it's basically just a website with a database).

It's not super fun to install, but luckily there are docker images available.
Here, we have a docker-compose.yml file, which allows you to run your own copy
using only the command `docker-compose up` when in this directory. Your own copy
will then be available by pointing your browser to localhost:3000 (or
127.0.0.1:3000).

Ideally, we will use a centralized copy, running on AWS or Azure.

### Data

Data is ephemeral by default in docker - if you don't say you want to keep it,
it disappears whenever you rebuild an image (and sometimes even more often).

In our docker-compose.yml file there is a 'volumes' section defined. This tells
docker to keep a persistent volume to store our database, mapping the
container's `/var/lib/postgres/9.3` (the postgres database) to docker's storage
location, in our case `/var/lib/docker/volumes/cartodb_db/_data`.

### Scripts

#### Creating new users

As of writing (2016-06-30), there is no way to create a new user from the web
frontend. Instead, you must run a script *within* the cartodb docker container.

You can run the script in a two-step process (update this if you find a better
way):

1) Copy it to the running container using `docker cp script/create_dev_user
cartodb_cartodb_1:/`. Make sure the last argument (`cartodb_cartodb_1`) is the
true name of the running container.
2) Run it using `docker exec -i -t sh /create_dev_user`.

The `script/create_dev_user` shell script creates a new 'dev-level' user. This
is taken directly from the CartoDB master branch as of 2016-06-30, and would
normally be included in the docker instance, but the version cloned + installed
is too old and is only good for creating a single user named 'dev'. This one
will prompt for two things:

1) A 'hostname'. This is your username.
2) A password. This is your password.
