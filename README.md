# Gitlab Boilerplate - Community Edition Setup

This instructions are designed to install Gitlab CE in your machine as fast as possible using Docker.
A docker compose configuration is provided, it requires to set the following environment variables:

```
export GITLAB_HOME=/srv/gitlab
export GITLAB_HOST=localhost
export GITLAB_ROOT_PASSWORD=password
export EXTERNAL_URL=http://localhost 
```

Note that `localhost` can be `example.com` (whatever domain you requires). `/srv/gitlab` will be the folder in your machine where all configuration will persist even if you kill docker containers.

The first step is to run the containers:
```
docker compose up -d
```

You can go now to `http://localhost` (Container last to load some minutes) and log with the root account:

USER: root
PASSWORD: GITLAB_ROOT_PASSWORD

For setting up a runner that will run your pipelines, run the following command:

```
docker compose exec runner gitlab-runner register --docker-privileged
```

For host: http://gitlab (internal host in docker network)

It will ask for a token, token can be obtained in the following route:

http://localhost/admin => Overvierw => Runners => Register an instance runner

Set the name as: `Shared runner`

Enter the tags associated with the runner, separated by commas. You can change this value later in the GitLab user interface. 

Provide the runner executor. Enter `docker`.

For default image: `ubuntu:focal`