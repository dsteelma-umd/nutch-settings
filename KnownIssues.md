# Known Issues

The following issues arise when trying to crawl the UMD Libraries website:

## SiteMap Parser

The current SitemapProcessor parses the UMD Libraries sitemap with errors:

```
> echo 'https://www.lib.umd.edu/sitemap.xml' > sitemaps/seed.txt
> bin/nutch sitemap test -sitemapUrls sitemaps/
SitemapProcessor: sitemap urls dir: sitemaps
SitemapProcessor: Starting at 2018-05-09 18:50:45
robots.txt whitelist not configured.
Exception for record https://www.lib.umd.edu/sitemap.xml : crawlercommons.sitemaps.UnknownFormatException: Failed to parse https://www.lib.umd.edu/sitemap.xml
	at crawlercommons.sitemaps.SiteMapParser.processXml(SiteMapParser.java:430)
	at crawlercommons.sitemaps.SiteMapParser.processXml(SiteMapParser.java:285)
	at crawlercommons.sitemaps.SiteMapParser.parseSiteMap(SiteMapParser.java:236)
	at org.apache.nutch.util.SitemapProcessor$SitemapMapper.generateSitemapUrlDatum(SitemapProcessor.java:213)
	at org.apache.nutch.util.SitemapProcessor$SitemapMapper.map(SitemapProcessor.java:164)
	at org.apache.nutch.util.SitemapProcessor$SitemapMapper.map(SitemapProcessor.java:95)
	at org.apache.hadoop.mapreduce.Mapper.run(Mapper.java:146)
	at org.apache.hadoop.mapreduce.lib.map.MultithreadedMapper$MapRunner.run(MultithreadedMapper.java:273)
Caused by: org.xml.sax.SAXParseException; lineNumber: 2026; columnNumber: 20; XML document structures must start and end within the same entity.
	at org.apache.xerces.parsers.AbstractSAXParser.parse(Unknown Source)
	at org.apache.xerces.jaxp.SAXParserImpl$JAXPSAXParser.parse(Unknown Source)
	at org.apache.xerces.jaxp.SAXParserImpl.parse(Unknown Source)
	at crawlercommons.sitemaps.SiteMapParser.processXml(SiteMapParser.java:407)
	... 7 more

SitemapProcessor: Total records rejected by filters: 0
SitemapProcessor: Total sitemaps from HostDb: 0
SitemapProcessor: Total sitemaps from seed urls: 1
SitemapProcessor: Total failed sitemap fetches: 0
SitemapProcessor: Total new sitemap entries added: 0
SitemapProcessor: Finished at 2018-05-09 18:50:50, elapsed: 00:00:05
```

## OnClick URLs

Certain URL hyperlinks surrounded by JavaScript are not parsed properly. These can be viewed in the linkdb dumps. View the inlinks for the following entry in the dump:

```
https://www.lib.umd.edu/pagenotfound	Inlinks:
```