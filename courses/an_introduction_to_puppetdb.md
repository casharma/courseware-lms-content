# An Introduction to PuppetDB
PuppetDB is a fast, scalable, and reliable data warehouse for Puppet. It caches data generated by Puppet, and offers advanced features through a powerful API. This course in an introduction to PuppetDB.

At the end of this course you will be able to:

* Identify the types of information stored in PuppetDB.
* List the three methods for retreiving data from PuppetDB.
* List three ways you can use PuppetDB.

## Video
[Link to Video](http://linktovideo)

## Slide 0



## Slide 1


                      

## Slide 2

In version 1.3, PuppetDB stores:
    The most recent facts from every node
    The most recent catalog for every node
    Optionally, seven days (configurable) of event reports for every node
Together, these give you a huge inventory of metadata about every node in your infrastructure and a searchable database of every single resource being managed on any node.

## Slide 3



## Slide 4

When resource stashing (AKA storeconfigs) is enabled, the puppet master will send a copy of every catalog it compiles to PuppetDB. PuppetDB retains the most recent catalog for every node and provides the puppet master with a search interface to those catalogs.

## Slide 5

Checking Node Status
The PuppetDB plugins installed on your puppet master(s) include a status action for the node face. On your puppet master, run:
$ sudo puppet node status <node> 
where <node> is the name of the node you wish to investigate. This will tell you whether the node is active, when its last catalog was submitted, and when its last facts were submitted.


## Slide 6

Declaring an exported resource causes that resource to be added to the catalog and marked with an “exported” flag, which prevents puppet agent from managing the resource (unless it was collected). When PuppetDB receives the catalog, it also takes note of this flag.
Collecting an exported resource causes the puppet master to send a search query to PuppetDB. PuppetDB will respond with every exported resource that matches the search expression, and the puppet master will add those resources to the catalog.

## Slide 7

The inventory is a collection of node facts. The inventory service is a retrieval, storage, and search API exposed to the network by the puppet master. The inventory service backend (AKA the facts_terminus) is what the puppet master uses to store the inventory and do some of the heavy lifting of the inventory service.
The puppet master updates the inventory when agent nodes report their facts, which happens every time puppet agent requests a catalog. Optionally, additional puppet masters can use the HTTP API to send facts from their agents to the central inventory.
Other tools, including Puppet Dashboard, can query the inventory via the puppet master’s HTTP API. An API call can return:
    Complete facts for a single node
or
    A list of nodes whose facts meet some search condition
Information in the inventory is never automatically expired, but it is timestamped.

## Slide 8


## Quiz
1. True or False. PuppetDB is a database that can replace your MySQL or PostgreSQL databases in your current configuration. (False)
2. PuppetDB stores all of the following, except:
a. Most recent facts from every node b. Hiera values calculated for every node c. Most recent catalog for every node d. Seven days of event reports for every node (b)
3. Which of the following are not used to get data from PuppetDB?
a. Puppet's Inventory Service b. PuppetDB's query API c. virtual resources d. exported resources
4. True or False. Declaring an exported resource causes that resource to be added to the catalog and marked with an “exported” flag, which prevents puppet agent from managing the resource (unless it was collected). When PuppetDB receives the catalog, it also takes note of this flag. (True)
5. True or False. Information in the inventory is automatically expires. (False)

## Resources
* [GitHub - PuppetDB](https://github.com/puppetlabs/puppetdb)
* [Puppet Labs Docs](http://docs.puppetlabs.com/puppetdb/latest/)
* [Exported Reources](http://docs.puppetlabs.com/puppet/2.7/reference/lang_exported.html)
* [Inventory Service](http://docs.puppetlabs.com/guides/inventory_service.html)