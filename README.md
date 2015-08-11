#CDH 5 pseudo-distributed cluster Docker image

Do you develop Hadoop mapreduce applications on top of Cloudera distribution? This docker image can help you. It contains basic CDH 5 setup with YARN. You can use it for developmeent and verification of your code in local environment without messing up your system with Hadoop instalation.

Docker image was prepared according to [Installing CDH 5 with YARN on a Single Linux Node in Pseudo-distributed mode](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CDH5/latest/CDH5-Quick-Start/cdh5qs_yarn_pseudo.html) with a few adjustments for Docker environment.

#####Installed services
* HDFS
* YARN
* JobHistoryServer
* Oozie
* Hue
* Spark (installation for execution on top of YARN)

###Execution
Get docker image

    docker pull yobibytes/cdh5-pseudo-distributed

Run image with specified port mapping

    docker run --name cdh -d -p 8020:8020 -p 50070:50070 -p 50010:50010 -p 50020:50020 -p 50075:50075 -p 8030:8030 -p 8031:8031 -p 8032:8032 -p 8033:8033 -p 8088:8088 -p 8040:8040 -p 8042:8042 -p 10020:10020 -p 19888:19888 -p 11000:11000 -p 8888:8888 -p 18080:18080 -p 9999:9999 chalimartines/cdh5-pseudo-distributed

 Or you can use docker-compose configuration: 
 
    docker-compose up -d
 
###web frontend entry points
Those urls consider port forwarding from docker host.
* name node - http://docker:50070
* resource manager - http://docker:8088
* job history server - http://docker:19888
* oozie console - http://docker:11000
* hue - http://docker:8888
* spark history server - http://docker:18080
(note: you can replace the boot2docker ip with a hostname like 'docker' in the hosts file.)

####Hue login
You will be asked to create account during the first login. You can pick your prefered username and password. It will create home folder on HDFS and it can be used as hadoop user.

####Custom port for your usecases
This image has exposed one port (9999). It is not used by any currently running service. It can be used by you for example when you need to attach debugger to running mapreduce job. So your mapreduce job can start debugging server on this port.
