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
