# Solr

## Installation

1) Download the Apache Solr source (solr-6.6.X.tgz).

2) Extract it and change directory:

```
> tar xf solr-6.6.X.tgz
> cd solr-6.6.X/
```

I will refer to this directory as ```${SOLR_DIR}```

## Configuration

We will need to create a Solr *core* for Nutch to index results to.

1) Create resources for a new nutch solr core:

```
> cp -r ${SOLR_DIR}/server/solr/configsets/basic_configs ${SOLR_DIR}/server/solr/configsets/nutch
```

2) Copy the Nutch Schema into the Solr ```conf``` directory

```
> cp ${NUTCH_DIR}/conf/schema.xml ${SOLR_DIR}/server/solr/configsets/nutch/conf
```

3) Remove the ```managed-schema```:

```
> rm ${SOLR_DIR}/server/solr/configsets/nutch/conf/managed-schema
```

4) Start the Solr server:

```
> ${SOLR_DIR}bin/solr start
```

5) Create the Nutch core in Solr

```
> ${SOLR_DIR}/bin/solr create -c nutch -d server/solr/configsets/nutch/conf/
```

6) Verify installation by going to the following URL in your browser:

```
http://localhost:8983/solr/#/nutch
```

NOTE: The browser URL ```http://localhost:8983/solr/#/nutch ``` is different from the URL we will provide to the Nutch command line ```http://localhost:8983/solr/nutch```