# How to use PySpark with local data or from AWS S3


The original branch for docker Spark and all info about the docker used in this demo, updated versions, etc, can be found [here](https://github.com/gettyimages/docker-spark).


If you don't know how to use docker check section [sample commands](sample-commands), you will find a basic resume about docker commands.

    
# PySpark script configuration

## Start your server and test it
- docker-compose up --detached
- Test it - see command in `sample commands`

## Using local files
- Create a folder inside your server
- Copy your files to folder
- submit your job, for script sample check file: pyspark_scripts/script-local.py


## Using AWS S3a files
- Create a S3 bucket and upload your files there (or use an existing one)
- Create a file named `aws-credentials.cfg` with content below - add your aws credentials to this file
     
      [AWS]
     
      AWS_ACCESS_KEY_ID=__YOUR__ACCESS_KEY_ID__
     
      AWS_SECRET_ACCESS_KEY=__YOUR__AWS_SECRET_ACCESS_KEY__
      
      
- submit your job, for script sample check file: pyspark_scripts/script-aws.py



## [docker-compose](http://docs.docker.com/compose): #sample-commands

To create a standalone cluster

    docker-compose up --detach


To stop your server

    docker-compose stop


To start your server from last run

    docker-compose start


To stop and remove your server

    docker-compose down


To log into to spark server

    docker exec -it docker-spark_master_1 /bin/bash


The SparkUI will be running at `http://${YOUR_DOCKER_HOST}:8080` with one worker listed. To run `pyspark`, exec into a container:

    docker exec -it docker-spark_master_1 /bin/bash
    bin/pyspark


To run a test using PySpark

    echo -e "import pyspark\n\nprint(pyspark.SparkContext().parallelize(range(0, 10)).count())" > count.py
    docker run --rm -it -p 4040:4040 -v $(pwd)/count.py:/count.py gettyimages/spark bin/spark-submit /count.py


To run your script using PySpark (don't need to start docker before)

    docker run --rm -it -p 4040:4040 -v $(pwd)/script_name.py:/script_name.py gettyimages/spark bin/spark-submit /script_name.py
    

To copy files to server (start your server first)

    docker cp PATH/script_name.py docker-spark_master_1:/PATH/.
    

From inside the server you can run bash commands or any other command like spark-submit

    spark-submit PATH/script_name.py



## license

MIT
