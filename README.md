# Nutch Settings. 

## Introduction

Apache Nutch is a popular web crawler used by many websites to index their pages. Since the tutorial on the official [website][1] is barebones, I'm writing this detailed tutorial on customizing your Nutch Crawler.

This tutorial will be tailored to crawl on the [UMD Libraries website][2].

## Installation

### Requirements

* Unix environment (This was tested on Ubuntu Server 16.04)
* Java Runtime/Development Environment (JDK 1.8/Java 8)
* Apache Ant: http://ant.apache.org/

### Nutch

1) Download the Apache Nutch source (apache-nutch-1.X-src.zip).

2) Extract it and change directory:

```
> tar xf apache-nutch-1.X-src.zip
> cd apache-nutch-1.X/
```

3) Run ant:

```
> ant
```

4) [OPTIONAL] Setup permissions and JAVA_DIR:

```
> chmod +x bin/nutch
> export JAVA_DIR=$(readlink -f /usr/bin/java | sed "s:bin/java::")
```

5) Our Nutch build is now ready at:

```
> cd runtime/local
```

I will refer to this directory as ```${NUTCH_DIR}```

### Solr

1) Download the Apache Solr source (solr-6.X.X.tgz).

2) Extract it and change directory:

```
> tar xf solr-6.X.X.tgz
> cd solr-6.X.X/
```

I will refer to this directory as ```${SOLR_DIR}```

3) Create resources for a new nutch solr core:

```
> cp -r ${SOLR_DIR}/server/solr/configsets/basic_configs ${SOLR_DIR}/server/solr/configsets/nutch
```

4) Copy the Nutch Schema into the Solr ```conf``` directory

```
> cp ${NUTCH_DIR}/conf/schema.xml ${SOLR_DIR}/server/solr/configsets/nutch/conf
```

5) Remove the ```managed-schema```:

```
> rm ${SOLR_DIR}/server/solr/configsets/nutch/conf/managed-schema
```

6) Start the Solr server:

```
> ${SOLR_DIR}bin/solr start
```

7) Create the Nutch core in Solr

```
> ${SOLR_DIR}/bin/solr create -c nutch -d server/solr/configsets/nutch/conf/
```

8) Verify installation by going to the following URL in your browser:

```
http://localhost:8983/solr/#/nutch
```

NOTE: The browser URL ```http://localhost:8983/solr/#/nutch ``` is different from the URL we will provide to the command line ```http://localhost:8983/solr/nutch```


## Configuration

We need to customize three properties at minimum to crawl our first website.

### Crawl Properties

The default nutch properties are found on ```${NUTCH_DIR}/conf/nutch-default.xml``` and we can override them by ```${NUTCH_DIR}/conf/nutch-site.xml```. We will need to add one property to ```conf/nutch-site.xml``` to initiate the search.

```
<property>
 <name>http.agent.name</name>
 <value>My Nutch Spider</value>
</property>
```

### Initial seed list

A URL seed list includes a list of websites, one-per-line, which nutch will look to crawl. We can create this list by using the following commands and adding the seed urls:

```
mkdir -p ${NUTCH_DIR}/urls
cd ${NUTCH_DIR}/urls
vi seed.txt
```

### Regular Expression Filters

Edit the file ```${NUTCH_DIR}/conf/regex-urlfilter.txt``` and replace it with the regular expression for your website. 

```
+^https?://(www\.)*lib\.umd\.edu
```

Your searcher configurations are ready now.


## Crawling

In order to crawl the website, you will need to run the following command from 
```${NUTCH_DIR}```:

```
bin/crawl -i -D solr.server.url=http://localhost:8983/solr/nutch urls/ LibCrawl/  10
```

This will generate the seed list from files in the ```urls``` directory, index the results on the Solr URL ```http://localhost:8983/solr/nutch```, generate the databases in the ```LibCrawl``` directory, and run this search upto depth ```10```.

[1]: https://www.apache.org/dyn/closer.cgi/nutch/
[2]: https://www.lib.umd.edu/