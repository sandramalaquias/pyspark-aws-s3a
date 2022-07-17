# PySpark using data from local server and from AWS S3

The original branch for docker Spark and all info about this docker, updated versions, etc, can be found [here](https://github.com/gettyimages/docker-spark).


See below a resume about docker commands and after that the info of how to configure your scripts to load info from local server and from AWS S3.


## [docker-compose](http://docs.docker.com/compose): sample commands

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
    

To copy files to server

    docker cp PATH/script_name.py docker-spark_master_1:/PATH/.
    

From inside the server you can run bash commands or any other command like spark-submit

    spark-submit PATH/script_name.py

    
# PySpark script configuration

## Using local files
- Create a folder inside your server
- Copy your files to folder
- check the file: pyspark_scripts/script-local.py

## Using AWS S3a files
- Create a S3 bucket and upload your files there (or use an existing one)
- check the file: pyspark_scripts/script-aws.py


## license

MIT
