# PySpark and AWS S3

The original branch for docker Spark and all info about docker I used can be found [here](https://github.com/gettyimages/docker-spark).


See below a resume about starting your docker and then the info of how to configure your script to load info from AWS S3.


## docker example

To run something using PySpark

    echo -e "import pyspark\n\nprint(pyspark.SparkContext().parallelize(range(0, 10)).count())" > count.py
    docker run --rm -it -p 4040:4040 -v $(pwd)/count.py:/count.py gettyimages/spark bin/spark-submit /count.py

## [docker-compose](http://docs.docker.com/compose): sample commands

To create a standalone cluster with

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





## license

MIT
