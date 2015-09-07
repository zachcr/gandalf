# Gandalf
---

### Curio Schedule Task System
Curio's schedule task system, include crontab, schedule. Support request type: http, nsq.

### dockerfiles
```
# Pull base image.
FROM ubuntu:14.04

# Copy sources.list
COPY ./sources.list /etc/apt/sources.list

# Install Python.
RUN \
  apt-get update && \
  apt-get install -y vim python python-dev python-pip python-virtualenv && \
  rm -rf /var/lib/apt/lists/*

# Install requirements
RUN pip install pymongo -i http://pypi.douban.com/simple
RUN pip install tornado -i http://pypi.douban.com/simple
RUN pip insatll requests -i http://pypi.douban.com/simple
RUN pip install raven -i http://pypi.douban.com/simple

# Define default command.
CMD ["/python/"]
```

### docker build

```
docker run -t \
-v /home/vagrant/shared/codes/src/git.curio.im/hacker/gandalf:/python/git.curio.im/hacker/gandalf:rw \
--name gandalf -i \
-p 80:8888 \
--link gandalf-mongo:mongo-rs \
-d gandalf /bin/bash

```