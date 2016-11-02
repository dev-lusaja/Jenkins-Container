Jenkins Container
=================

** Create a directory for jenkins's data **

~~~~
$ mkdir /jenkins
~~~~

** Change user or group (optional) ** 
~~~~
$ chown user:group /jenkins
~~~~

** Creating file for logging **

~~~~
$ cat > /jenkins/log.properties <<EOF
handlers=java.util.logging.ConsoleHandler
jenkins.level=FINEST
java.util.logging.ConsoleHandler.level=FINEST
EOF
~~~~

** Create jenkins user on the Host **
~~~
$ useradd jenkins
~~~

** Add the jenkins user to the group for directory (optional) **
~~~~
$ groupadd jenkins <group>
~~~~

** Search is jenkins's uid **
~~~~
$ id -u jenkins
~~~~

** Create the container **
~~~~
$ docker run -d -u <user|uid> --name jenkins -p 8081:8080 -p 50000:50000 --env JAVA_OPTS="-Djava.util.logging.config.file=/var/jenkins_home/log.properties" -v /jenkins:/var/jenkins_home jenkins
~~~~

** Test and be happy **
~~~~
http://localhost:8081/
~~~~