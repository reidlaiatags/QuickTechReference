# Run multiple processes and services in docker container

When designing a Docker container, you're supposed to build it such that there is only one process running; additionally, that process should run in the foreground.

So when you start background services in docker, container will immediately stop after completed.

Supervisor can help to solve problem of starting background service and multple processes.

## Create supervisord.conf file

```
[supervisord]
nodaemon=true

[program:sshd]
command=/usr/sbin/sshd -D

[program:apache2]
command=/bin/bash -c "source /etc/apache2/envvars && exec /usr/sbin/apache2 -DFOREGROUND"
```

You can replace sshd and apache2 with other service or programs depends on your need

## Install and set up supervisord in Dockerfile

```
RUN apt-get install supervisor -y
RUN mkdir -p /var/log/supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
CMD ["/usr/bin/supervisord"]

```


