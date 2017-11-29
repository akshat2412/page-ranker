# Simple Python Search Spider, Page Ranker, and Visualizer (Part of Capstone Project on Coursera)
This is an assignment that I did as part of **Capstone project** of **Python for Everybody Specialization** on **Coursera**. 

This is a set of programs that emulate some of the functions of a 
search engine, i.e. it crawls the web pages according to the starting url that the user provides, ranks them according to the 
number of 'good' incoming links and then visualizes them in a web according to their rank.

## Requirements
### Python Libraries
* urllib
* ssl
* urlparse
* sqlite3 : 
You should install the SQLite browser to view and modify 
the databases from: http://sqlitebrowser.org/

## Working
### Crawling and Ranking ###
This program crawls a web site and pulls a series of pages into the
database, recording the links between pages. It stores the data in a SQLITE3 database named
'spider.sqlite'.  This file can be removed at any time to restart the
process if it already exists.

* **spider.py**

  ```Enter web url or enter:```
  
    Enter the url from where you wish to start the crawl or you can press `enter` to start the crawl from www.dr-chuck.com
  ```How many pages: ``` 2
  
    In this sample run, we told it to crawl a website and retrieve two 
    pages.  If you restart the program again and tell it to crawl more
    pages, it will not re-crawl any pages already in the database.  Upon 
    restart it goes to a random non-crawled page and starts there.  So 
    each successive run of spider.py is additive.

    You can have multiple starting points in the same database - 
    within the program these are called "webs".   The spider
    chooses randomly amongst all non-visited links across all
    the webs.
    
    If your code fails complainin about certificate probems, 
there is some code (SSL) that can be un-commented to work
around certificate problems.

* **spdump.py**

  If you want to dump the contents of the spider.sqlite file, you can 
  run *spdump.py*.
  It will show the contents of the database in the following format:
  
  ```(count of incoming links , old_rank, new_rank, id, url)```
  
  The *spdump.py* program only shows pages that have at least one incoming link to them.
  
* **sprank.py**
  
  Once you have a few pages in the database, you can run Page Rank on the
  pages using the sprank.py program.  You simply tell it how many Page
  Rank iterations to run.
  
  You can dump the database again to see that page rank has been updated
  
  You can run *sprank.py* as many times as you like and it will simply refine
  the page rank the more times you run it.  You can even run *sprank.py* a few times
  and then go spider a few more pages with *spider.py* and then run *sprank.py*
  to converge the page ranks.
  
  For each iteration of the page rank algorithm it prints the average
  change per page of the page rank. The network initially is quite 
  unbalanced and so the individual page ranks are changeing wildly.
  But in a few short iterations, the page rank converges.  You 
  should run *sprank.py* long enough that the page ranks converge.
  
* **spreset.py**
  
  If you want to restart the Page Rank calculations without re-spidering the 
  web pages, you can use *spreset.py*. It sets the ranks of all pages to 1.0
  
### Visualization ###

If you want to visualize the current top pages in terms of page rank,
run *spjson.py* to write the pages out in JSON format to be viewed in a
web browser.

You can view this data by opening the file force.html in your web browser.  
This shows an automatic layout of the nodes and links.  You can click and 
drag any node and you can also double click on a node to find the URL
that is represented by the node.

This visualization is provided using the force layout from: mbostock.github.com/d3

If you rerun the other utilities and then re-run spjson.py - you merely
have to press refresh in the browser to get the new data from *spider.js*.
  
  
