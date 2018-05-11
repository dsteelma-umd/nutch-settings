# Nutch Settings

## Introduction

Apache Nutch is a popular web crawler used by many websites. Since the tutorial on the official [website][1] is barebones, I'm writing this detailed tutorial on customizing your Nutch Crawler.

This tutorial will be tailored to crawl on the [UMD Libraries][2] website and use [Apache Solr][3] to index the pages.

## Requirements

* Unix environment (This was tested on Ubuntu Server 16.04)
* Java Runtime/Development Environment (JDK 1.8/Java 8)
* Apache Ant

## Versions

This tutorial supports the following versions of Nutcha and Solr:

Nutch | Solr
----- | -----
1.14 | 6.6

A *close* version of Nutch or Solr can be used, but is not guaranteed to work with this tutorial.

## Walkthrough

The walkthrough is best followed in this order:

1) [Setting up Nutch][4]

2) [Setting up Solr][5]

3) [Crawling and Analyzing Results][6]

4) [Known Issues][7]

5) [Resources][8]



[1]: https://www.apache.org/dyn/closer.cgi/nutch/
[2]: https://www.lib.umd.edu/
[3]: https://lucene.apache.org/solr/
[4]: https://github.com/samirlalvani/nutch-settings/blob/master/Nutch.md
[5]: https://github.com/samirlalvani/nutch-settings/blob/master/Solr.md
[6]: https://github.com/samirlalvani/nutch-settings/blob/master/Crawlanalysis.md
[7]: https://github.com/samirlalvani/nutch-settings/blob/master/KnownIssues.md
[8]: https://github.com/samirlalvani/nutch-settings/blob/master/Resources.md