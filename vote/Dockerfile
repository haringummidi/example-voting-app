# Using official python runtime base image
FROM schoolofdevops/voteapp-python:v0.1.0

# Set the application directory
WORKDIR /app

# Adding variables as arg
ARG user=app

ARG group=app

ARG uid=1000

ARG gid=1000

# Creating and adding user/userGroup
RUN addgroup -g ${gid} ${group} \
	&& adduser -u ${uid} -G ${group} -s /bin/sh -D ${user} \
	&& chown -R ${user}:${group} /app

# Install our requirements.txt
ADD requirements.txt /app/requirements.txt
RUN pip install -r requirements.txt

# Copy our code from the current folder to /app inside the container
ADD . /app

# Make port 8080 available for links and/or publish
EXPOSE 8080

# Changing user to new user
USER ${user}

# Define our command to be run when launching the container
CMD ["gunicorn", "app:app", "-b", "0.0.0.0:8080", "--log-file", "-", "--access-logfile", "-", "--workers", "4", "--keep-alive", "0"]
