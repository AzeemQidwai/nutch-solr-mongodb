# BDA Final Project
## DataHarvest: Dockerized Web Crawling, Indexing, and Storage Solution

![](https://img.shields.io/badge/Docker-2496ED.svg?style=for-the-badge&logo=Docker&logoColor=white) ![](https://img.shields.io/badge/Python-3776AB.svg?style=for-the-badge&logo=Python&logoColor=white) ![](https://img.shields.io/badge/Apache%20Solr-D9411E.svg?style=for-the-badge&logo=Apache-Solr&logoColor=white) ![](https://img.shields.io/badge/MongoDB-47A248.svg?style=for-the-badge&logo=MongoDB&logoColor=white)

### :school: Team Members
- :student: Azeem Ahmed
- :student: Shaheryar Ahmed

### :page_facing_up: Project Description
DataHarvest is a cutting-edge web crawling, indexing, and storage solution implemented using Docker. It leverages the power of Docker's containerization to provide seamless deployment, scalability, and portability. With DataHarvest, organizations can efficiently extract and process data from the web, while storing it in a reliable and easily manageable manner. Empowered by Docker, DataHarvest simplifies the setup process, ensures scalability for handling large volumes of data, and offers flexibility across different environments. Experience advanced web crawling and storage with DataHarvest, the Dockerized solution for your data extraction needs.

### :computer: Technology Stack
Below mentioned technologies are used in this project:
| Docker | Apache Nutch | Apache Solr | MongoDB |
|-------|------|---------|-----------|
| <img src="./images/vertical-logo-monochromatic.png" width="174.25" height="149" alt="Docker"/> | <img src="./images/nutch.svg" width="180" height="75" alt="Nutch"/> | <img src="./images/solr.svg" width="180" height="100" alt="Solr"/> | <img src="./images/MongoDB_Fores-Green.svg" width="200" height="50.50" alt="MongoDB"/> |

Apache Nutch is a highly extensible and scalable web crawler written in Java. It is a part of the Apache Hadoop ecosystem and is used to extract and process data from the web. Apache Solr is an open-source enterprise search platform written in Java. It is used to index and search large volumes of data. MongoDB is a NoSQL database that is used to store data in a document-oriented manner. It is a highly scalable and flexible database that is used to store large volumes of data.

Apache Nutch and Apache Solr operate independently in their respective containers, enabling efficient and scalable web crawling and indexing. The containerized Python environment facilitates seamless data retrieval from the Apache Solr container, while securely storing the results in a cloud-hosted MongoDB database.

### :man_technologist: Project Setup
Setup free tier MongoDB Atlas by following the instructions below link:

[MongoDB Atlas Free Tier](https://www.mongodb.com/developer/products/atlas/free-atlas-cluster/)

Before running the project, make sure that you have Docker and Docker Compose installed on your system. If not, follow the instructions below to install them.

Install project specific dependencies using the following command:

```bash
sudo apt-get update && sudo apt-get upgrade -y
```
```bash
sudo apt-get install -y docker.io docker-compose
```
Clone the repository using the following command:
```bash
git clone https://github.com/AzeemQidwai/nutch-solr-mongodb.git
```
Navigate to the project directory using the following command:
```bash
cd nutch-solr-mongodb
```
Setup `auth.json` file in the `root` directory. This file contains the credentials for the MongoDB database. The file should be in the following format:

```json
{
    "user": "username",
    "password": "password"
}
```

Following `Dockerfile` is used to build the `python` image [^1].
```dockerfile
FROM python:latest

WORKDIR /usr/src/app

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY ./app.py .
COPY ./auth.json .

ENV PYTHONUNBUFFERED=1

CMD [ "python", "-u", "app.py" ]
```

Run the following command to start the project:
```bash
docker-compose up -d
```
This will create and start the following containers:
- nutch
- solr
- python

To access the `solr` container, go to the following URL in your browser:
```bash
http://localhost:8983/solr/
```

To stop the project, run the following command:
```bash
docker-compose down --rmi local
```

### :gear: Project Usage
The project can be used to crawl and index data from the web. The data can be retrieved from the MongoDB database using the Python container. The following sections describe the usage of the project in detail.

#### :one: Crawling
To configure the nutch container, simply set the target website in the `seed.txt` file located in the `nutch/urls` directory. Additionally, you can customize the crawling behavior by modifying the `regex-urlfilter.txt` file in the `nutch/conf` directory, allowing you to define specific regex patterns for data extraction.

#### :two: Indexing
You can customize the indexing behavior by modifying the `schema.xml` file in the `/opt/solr/server/solr/configsets/nutch/conf/` directory, allowing you to define specific fields for data indexing.

#### :three: Data Retrieval
To retrieve data from the `solr` container, python scripts are used. The `python` container is used to run `app.py` which retrieves data from the `solr` container and stores it in the MongoDB database.

## :tv: Project Video
Video of working project can be accessed from here [Link](https://youtu.be/vqmDYkfE3Jw)

[^1]: [Dockerfile Reference](https://hub.docker.com/_/python)
