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
