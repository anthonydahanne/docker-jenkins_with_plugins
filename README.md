# Run jenkins with some plugins in a container

The plugins.txt content was filled from  [https://updates.jenkins-ci.org/download/plugins/](https://updates.jenkins-ci.org/download/plugins/)

    $ docker run -d -p 8000:8080 -p 50000:50000  --name=jenkins anthonydahanne/jenkins_with_plugins

Using socat to pipe the Docker Unix socket to a TCP port (to use the build step plugin for example, use http://socat:2375)

    $ docker run -v /var/run/docker.sock:/var/run/docker.sock -d  --name socat  anthonydahanne/docker-socat
    $ docker run -d -p 8000:8080 -p 50000:50000  --link socat:socat  --name=jenkins anthonydahanne/jenkins_with_plugins
