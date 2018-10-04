# iowa-liquor
Iowa liquor data set configuration files for importing into Elasticsearch.  Based on webinar from Elastic on Logstash CSV import - https://www.elastic.co/webinars/csv-logstash-ingestion

## Download Iowa Liquor data
Go to https://data.iowa.gov/Economy/Iowa-Liquor-Sales/m3tr-qhgy and download the CSV file for Iowa Liquor sales.

## Setup iowa-liquor mapping in Kibana

Add a mappings to the iowa-liquor index for just the one field that can’t be autodetected by entering the following in the developer console in Kibana:

```
PUT iowa-liquor
{
  "settings": {
    "index": {
      "number_of_shards": "2"
    }
  },
  "mappings": {
    "_doc": {
      "properties": {
        "location": {
          "type": "geo_point"
        }
      }
    }
  }
}
```

## Use Logstash to import into Elasticsearch

Change username and password in iowa.conf file in output section

Run Logstash with iowa.conf configuration file for each month - for example:

```
tail -n +2 /path/to/data/Iowa_Liquor_Sales.csv | /path/to/logstash/bin/logstash -f /path/to/iowa.conf
```

Go to Kibana, under Management create an index pattern called 'iowa-liquor'

## Import Kibana visualizations

In Kibana, Managmenet, Saved Objects, Import iowa.json file
