# Data Import from InfluxDB to Tableau
# InfluxDB

InfluxDB is an open-source database built specifically for storing time-series data. It is optimised for high-availability storage and retrieval of data in areas like Internet Of Things (IOT) sensor data, mobile and web application metrics and real-time analytics.

# Tableau
Tableau is an extremely essential tool used for data visualisation. It helps professionals like data or business analysts in transforming data into an understandable format to achieve valuable insights. These insights later can help in taking decisions to improve the business growth.

# Installation
## Requirements

* Python 3.7
* Windows 64-Bit (Recommended)
* pip3 install -r requirements.txt

# Steps:
## 1. Setting Up the InfluxDB (Windows 32-bit/64-bit)
* Go to the link for downloading [InfluxDB Package](https://portal.influxdata.com/downloads/)
* Click the lastest version (For e.g. v 1.8.0) of the package.
* On the next screen, download the **zip** file on your local system based on the specifications (32/64-bit). 
* After extracting, you'll find a number of executable files in the extracted folder.
* Firstly run the **influxd.exe** (source server) file followed by **influx.exe** (influx client) file.
* The influx server by default is running on port **8086**.
* If there is no error, means the setup is successful!!.

## 2. Creating database in InfluxDB
Go to the "Importing CSV Data to InfluxDB Measurement.ipynb" notebook in the repository and follow the python code for creating database, measurement and inserting data into the influxdb.

## 3. Verifying the Data Stored in InfluxDB

On the InfluxDB client, execute the following commands in sequence to verify the creation of database, measurements and also the data insertion.
* Database Creation

![Image1](https://github.com/umer-saleem/influxdb-tableau/blob/master/images/databases%20creation.PNG)

* Use Database

![Image2](https://github.com/umer-saleem/influxdb-tableau/blob/master/images/use%20database.PNG)

* Show Measurement

![Image3](https://github.com/umer-saleem/influxdb-tableau/blob/master/images/show%20measurements.PNG)

* Inserted Data 

![Image4](https://github.com/umer-saleem/influxdb-tableau/blob/master/images/inserted%20data.PNG)



# Web Data Connector

Web Data Connector (WDC) is the bridge that connects the influxDB data with Tableau. The main purpose of WDC is to connect to the data that is accessible over the HTTP but lacks a connector. The WDC must be hosted on a web server running locally on your system, on a web server in your domain or on a third-party web server.

## 4. Setting Up WDC for InfluxDB to Tableau Connection

You can visit the link below regarding step by step guidance for setup and connection of WDC with Tableau: 
* https://tableau.github.io/webdataconnector/docs/index.html#get-the-wdc-sdk.

After downloading the wdc sdk from the link above, in the “webconnector/Examples/js/earthquakeUSGS.js” file under the “getData” function , replace the existing url with the influxdb api (http://localhost:8086/query?pretty=true&db=fourthdb&q=SELECT%20*%20from%20measure_1) to query the influxdb database. Here, “db” is the existing database in influxdb, “q” allows you to query the measurement as per your requirement.

![Image5](https://github.com/umer-saleem/influxdb-tableau/blob/master/images/influxdb%20api%20request.PNG)

## 5. Designing Data Schema

As per the required variables, we can design the schema of the data to be mapped onto one or more tables in Tableau. The mapping can be perfoemed using the “getSchema” function in the “webconnector/Examples/js/earthquakeUSGS.js” file. 

## 6. Importing InfluxDB Data to Tableau

After making the above changes, open Tableau Desktop and Under "Connect", click on "Web Data Connector".Enter the WDC URL in the space below and press Enter.

![Image6](https://github.com/umer-saleem/influxdb-tableau/blob/master/images/Tableau%20WDC.png)

Tableau loads the WDC page where the user can provide any input. After that, tableau calls the WDC code, downloads the data from the web page containing the influxdb api response and displays it in the Data Source pane.
