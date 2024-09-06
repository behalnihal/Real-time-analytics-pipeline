## DBT-Flink-Adapter

### Prerequisites
- Python 3.10 or less
- Dbt-core version 1.3.7
- Git

### Installation

- Create a virtual environment in your desired directory
```bash
python -m venv dbt-env
```
- Install dbt-flink-adapter
```bash
python -m pip install dbt-flink-adapter
```
this command will install dbt-core and all the required dependencies


Once installation is completed we can create a **dbt** project, you can use default values when prompted.

```bash
$  dbt init
Enter a name for your project (letters, digits, underscore): example1
Which database would you like to use?
[1] flink

Enter a number: 1
host (Flink SQL Gateway host) [localhost]:
port [8083]:
session_name [test_session]:
database (Flink catalog) [default_catalog]:
schema (Flink database) [default_database]:
threads (1 or more) [1]:
```

We also need an Apache **Flink** instance with SQL Gateway and for the purpose of this tutorial a one node instance of **Apache Kafka**. 

```bash
$ curl -o docker-compose.yml https://raw.githubusercontent.com/gliter/dbt-flink-adapter-example/main/docker-compose.yml
```

Now download the flink-sql-connector-kafka jar file from maven OR [Download from here](https://repo1.maven.org/maven2/org/apache/flink/flink-sql-connector-kafka/1.16.0/flink-sql-connector-kafka-1.16.0.jar) and go to the same directory as the docker-compose file, create a folder named flink-lib and move this file in the 'flink-lib' folder.

Now run the compose file by the command 

```bash
$ docker-compose up
```

Create `clickstream`, `init-balance`, `trx, high-loan`, `joined-data`, `daily-spending` topics in **Kafka**

```bash
$ curl -o recreate-topics.sh https://raw.githubusercontent.com/gliter/dbt-flink-adapter-example/main/recreate-topics.sh
```

run the command 
```bash
docker ps
```

this will display the docker container names , copy the name of the kafka instance , then run the command 
```bash
docker exec [kafka instance name] chmod +x recreate-topics.sh
docker exec [kafka instance name] ./recreate-topics.sh
```

after this you should have all the required docker containers , and the kakfa topics.
you can also see the kafka topics by running the command , 
```bash
docker exec [kafka instance name] kafka-topics --bootstrap-server localhost:9092 --list
```
You can also open [http://localhost:8081](http://localhost:8081/) in your browser to see running **Apache Flink** instance

Now, make the models given in the models folder. and run the model by, 
```bash
dbt run
```
We can now open **Flink** UI [http://localhost:8081/](http://localhost:8081/) and we should see 3 jobs deployed.

![image](https://github.com/user-attachments/assets/4b146feb-ce8e-432d-a1b3-ced3714d780f)

### Input

dbt supports seed functionality that allows for loading data stored in csv into tables. In our case this will use the Flink Kafka connector to load data into Kafka topics.


### Using the starter project

Try running the following commands:
- dbt run
- dbt test


### Resources:
- Learn more about dbt [in the docs](https://docs.getdbt.com/docs/introduction)
- Check out [Discourse](https://discourse.getdbt.com/) for commonly asked questions and answers
- Join the [chat](https://community.getdbt.com/) on Slack for live discussions and support
- Find [dbt events](https://events.getdbt.com) near you
- Check out [the blog](https://blog.getdbt.com/) for the latest news on dbt's development and best practices
