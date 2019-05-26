# Sneaky Spider
Sneaky Spider is a C# library for web crawling and scraping. It is designed for simplicity and flexibility. Easy to install and easy to use. Surf the whole **World Wide Web** in just 3 Lines.

# Installing
Download or Clone the project. <br>
Open **Visual Studio** and open the **Solution Explorer**.<br>
Right click on **References** and click **Add Reference**.<br>
Click **Browse** button and add the **SneakySpider.dll** and **HtmlAgilityPack.dll**.<br>
Check mark them both and click **Ok**.<br>

That's all!!<br>

# Example
Sneaky Spider fetches data asynchonously. So we need a ```async``` method to bring the data from the web. Below, there is an example of crawling in **ASP.NET MVC:** <br>

```cs
using System.Threading.Tasks;
using HtmlAgilityPack;
using SneakySpider;

public async Task<ActionResult> Crawler(){
    Crawler crawler = new Crawler();
    crawler.setRootUrl("http://www.bishalsarker.com");
    await crawler.startCrawl(10);

    ViewBag.Data = crawler.getGraph().webify();
    return View();
}
```
The method ```setRootUrl()``` will give a point to crawler from where the crawler will start crawling. After that method ```startCrawl()``` will start crawling the web and gathering data from the web pages. This initializer is taking a parameter for the maximum itereration means how many links it will crawl. Then ```crawler.getGraph()``` will return a ```Graph``` object and using ```.webify()``` will return a result for showing data in a html page: <br>

```
graph = {
    Link Node 1: [List of edges, number of edges],
    Link Node 2: [List of edges, number of edges]
    ......
}

```

If you want to get the data of a particuler Node from the graph check the following example:

```cs
using System.Threading.Tasks;
using HtmlAgilityPack;
using SneakySpider;
using SneakySpider.GraphModel;

public async Task<ActionResult> Crawler(){
    Crawler crawler = new Crawler();
    crawler.setRootUrl("http://www.bishalsarker.com");
    await crawler.startCrawl(10);

    var myNode = crawler.getGraph().getAllNodes()[0];
    HtmlDocument myNodeData = crawler.getNodeData(myNode);
    
    return View();
}
```

You can even add rules to the crawler so that you can the specific links. To add rules use ```addRule()``` method. This method takes a parameter of [Regular Expression](https://regexone.com) patterns as a ```string```. You can add multiple of rules. For example,

```cs
using System.Threading.Tasks;
using HtmlAgilityPack;
using SneakySpider;
using SneakySpider.GraphModel;

public async Task<ActionResult> Crawler(){
    Crawler crawler = new Crawler();
    crawler.setRootUrl("http://www.bishalsarker.com");
    crawler.addRule("/post/[^$]");
    crawler.addRule("en.wikipedia.org");
    await crawler.startCrawl(10);

    var myNode = crawler.getGraph().getAllNodes()[0];
    HtmlDocument myNodeData = crawler.getNodeData(myNode);
    
    return View();
}
```

```crawler.getNodeData()``` will return an ```HtmlDocument``` object. If you want to learn more about it follow this [link](https://html-agility-pack.net/documentation) <br>

For scarping the data the ```SharpScraper``` will help you a lot. This class uses ```HtmlAgilityPack``` and has been developed to make the scraping more easier. For example,

```cs
using System.Threading.Tasks;
using HtmlAgilityPack;
using SneakySpider;
using SneakySpider.GraphModel;
using SneakySpider.SharpScraper;

public async Task<ActionResult> Crawler(){
    Crawler crawler = new Crawler();
    crawler.setRootUrl("http://www.bishalsarker.com");
    await crawler.startCrawl(10);

    var myNode = crawler.getGraph().getAllNodes()[0];
    HtmlDocument myNodeData = crawler.getNodeData(myNode);
    
    Scraper scraper = new Scraper();
    scraper.setHtmlDoc(myNodeData);
    var getAllLinks = scraper.getAllLinkNodes();
    
    return View();
}
```

The method ```getAllLinkNodes()``` will return a list of ```HtmlNode``` from the ```HtmlDocument```
Click here to learn more about [Html Agility Pack](https://html-agility-pack.net/) visit their website. It's a great tool for web scraping

# Documentation
Sneaky Scraper is still under development. Documentation will be here soon...

#
&copy; 2019 Binlab. 
