This is a docker image with jruby and rails environment.<br>
It's important to set the environment variable for local user to access the host filesystem in a consistent manner.
In the commands below it is assumed that your git repository is located under the git folder in your home direcoty.
If this is not the case, then you have to change it.
You can link to another docker container with database, below in the command a PostgreSQL container is assumed.



# Commands

build:

    docker build -t alpine-jruby --rm=true .

debug:
    
    docker run -p 3000:3000 -e LOCAL_USER_ID=`id -u $USER` --name jruby_instance -i -t -v ~/git:/home/user/git --link postgres_instance:postgres --entrypoint=sh alpine-jruby

run:

    docker run -p 3000:3000 -e LOCAL_USER_ID=`id -u $USER` --name jruby_instance -v ~/git:/home/user/git --link postgres_instance:postgres -i -P alpine-jruby


login:

    docker exec -i -t -u user jruby_instance /bin/bash


logout:

    exit