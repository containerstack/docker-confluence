

# Atlassian Confluence in a Docker container

This is a containerized installation of Atlassian Confluence with Docker.
The aim of this image is to keep the installation easy and as straight forward as possible.

It's possible to clone this repo and build the image on you're own machine, but if you think that's a waste of time ;-) there's a Automated Build in the Docker Hub that's based on this repo.

* [Docker Hub - Automated Build](https://hub.docker.com/r/containerstack/confluence/)
* [Atlassian Confluence latest build](https://confluence.atlassian.com/doc/confluence-release-notes-327.html)
* [Oracle MySQL Connector J latest build](http://dev.mysql.com/downloads/connector/j/)
* [Atlassian Confluence](https://www.atlassian.com/software/confluence)

## Git repos
* [Atlassian Bitbucket](https://bitbucket.org/containerstack/docker-confluence)
* [GitLab](https://gitlab.com/containerstack/docker-confluence)
* [GitHub](https://github.com/containerstack/docker-confluence)

## Versions
Currently this repo have the following versions;
* 6.15.8 (latest - not yet tested)
* 6.15.7 (latest - tested)


Go to [Branches](https://github.com/containerstack/docker-confluence/branches) to see all different builds that are available.

## Use the Automated Build image for a TEST deployment;

To quickly get started running a Confluence instance, use the following command:
```bash
docker run --detach \
           --name confluence \
           --publish 8090:8090 \
           remonlam/confluence:latest
```

Once the image has been downloaded and container is fully started (this could take a few minutes), browse to `http://[dockerhost]:8090` to finish the configuration and enter your trail/license key.

NOTE: It's not recommended to run Confluence this way because it does NOT have persistent storage, once the container is removed everything is gone!!

### What does all these options do?;
detach          runs the container in the background
name            gives the container a more useful name
publish         publish a port from the container to the outside world (docker node [outside] / container [inside])


## Use the Automated Build image for a PRODUCTION deployment;

In order to make sure that what ever you or you're team is creating in Confluence is persistent even when the container is recreated it's useful to make the "/var/atlassian/confluence" directory persistent.
```bash
docker run --detach \
           --name confluence \
           --volume "/persistent/storage/atlassian/confluence:/var/atlassian/confluence" \
           --env "CATALINA_OPTS= -Xms512m -Xmx4g" \
           --publish 8090:8090 \
           remonlam/confluence:latest
```

Once the image has been downloaded and container is fully started (this could take a few minutes), browse to `http://[dockerhost]:8090` to finish the configuration and enter your trail/license key.

### What does all these options do?;
| Option| Description|
| :------------- |:-------------|
|detach|*runs the container in the background*|
|name|*gives the container a more useful name*|
|volume|*maps a directory from the docker host inside the container*|
|env|*sets environment variables (this case it's for setting the JVM minimum/maximum memory 512MB<->2GB)*|
|publish|*publish a port from the container to the outside world (dockernode [outside] / container [inside])*|



## Issues, PR's and discussion

If you see an issues please create an [issue](https://github.com/remonlam/docker-confluence/issues/new) or even better fix it and create an [PR](https://github.com/remonlam/docker-confluence/compare) :-)
