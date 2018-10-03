# iowa-liquor
Iowa liquor data set configuration files for importing into Elasticsearch

## Download Iowa Liquor data
Go to https://data.iowa.gov/Economy/Iowa-Liquor-Sales/m3tr-qhgy and download the CSV file for Iowa Liquor sales.

## Use Logstash to import into Elasticsearch

Change username and password in iowa.conf file in output section

Run Logstash with iowa.conf configuration file for each month - for example:

```
tail -n +2 /path/to/data/Iowa_Liquor_Sales.csv | /path/to/logstash/bin/logstash -f /path/to/iowa.conf
```

Go to Kibana, under Management create an index pattern called 'iowa-liquor'

## Import Kibana visualizations

In Kibana, Managmenet, Saved Objects, Import iowa.json file
