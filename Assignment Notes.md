# Assignment Notes

-Password: Sammy100!

-Ambari: Maria-dev

-Root / Sammy100!

-Neo4j password: y65Ed652X&

-ambari-agent stop

-ambari-server stop

>Ambari: Service monitoring and access to HDFS  http://localhost:8080/ (Links to an external site.)     login:  maria_dev / maria_dev

>Zeppelin Spark notebook programming client: http://localhost:am9995/#/ (Links to an external site.)

>HDP shell on the web (used to program Pig Latin scripts):  http://localhost:4200/ (Links to an external site.)

>Neo4J: http://localhost:7474/browser/  (Links to an external site.)     

>neo4j /y65Ed652X&

# Start VM

ssh -L7474:localhost:7474 -L7687:localhost:7687 -L 8000:localhost:8000 -L 4200:localhost:4200 -L 8080:localhost:8080 -L 8888:localhost:8888 -L 8890:localhost:8890 -L 9995:localhost:9995 -L 30800:localhost:30800 -L 1080:localhost:1080 -L 4040:localhost:4040 -p50088 pmissier@ml-lab-cbe4a721-1d12-4a04-bf73-b7eeeb4bee66.uksouth.cloudapp.azure.com

# Start dockers:

sudo docker start sandbox-hdp; sudo docker start sandbox-proxy

# If TEZ hangs:

for x in $(yarn application -list -appStates RUNNING | awk 'NR > 2 { print $1 }'); do yarn application -kill $x; done

for x in $(yarn application -list -appTypes SPARK | awk 'NR > 2 { print $1 }'); do yarn application -kill $x; done

scp -r -P <port> <local file path> <username>@<hostname>:~/data

scp -r -P -p 50088 pmissier@ml-lab-cbe4a721-1d12-4a04-bf73-b7eeeb4bee66.uksouth.cloudapp.azure.com <local file path> ssh -L7474:localhost:7474 -L7687:localhost:7687 -L 8000:localhost:8000 -L 4200:localhost:4200 -L 8080:localhost:8080 -L 8888:localhost:8888 -L 8890:localhost:8890 -L 9995:localhost:9995 -L 30800:localhost:30800 -L 1080:localhost:1080 -L 4040:localhost:4040 -p
:~/data

For unioning all files in one directory -- same answer as @Lester Martin. 
You can use globs (wildcard characters) in your LOAD path to pull a subset of files from a directory, based on the filename pattern. See http://chimera.labs.oreilly.com/books/1234000001811/ch05.html#pl_load. 
For example you could LOAD the path 

name	start_date	end_date	location	hashtags
16-days-of-action-2018	2018-11-25	2018-12-10	United Kingdom	['#16days', '#16daysofaction', '#16daysofactiontoolkit']

$0 AS index, $1 AS context, $2 AS date, $3 AS tw_id, $4 AS is_media, $5 AS is_retweet,
 $6 AS no_likes, $7 AS no_retweets, $8 AS reply, $9 AS text, $10 AS user_name;

Schema should look like this:
context	username	retweet
	U3	U3
	U2	U1
	U1	U2
		

Load file into hdfs 
Get from hdfs into another database – should have HBase / Hive. 
(There are layers you can put on top that make it look like a normal sql database, this is called drill. I probably won’t use this?)

Run queries
Select 


Will return results
Collate results into a conclusion
 
with csv loader to get headers
Will also get rid of dirty data 
Pandas – not going to help me

Check for phoenix


Joined using tw_id using 

USE Sort function 

Tell me number of retweets/tweets someone has 
 
Map it to my data

When vi I call reduce I get my answers back

Jason might have examples
Look at  
Or use koalas
Start Again:


# Code to get the columns sorted:

data = spark.read.format("csv").option("header", True).option("multiLine", True).option("ignoreTrailingWhiteSpace", True).load("hdfs://sandbox-hdp.hortonworks.com:8020/user/maria_dev/TWEET_RETWEET")

from pyspark.sql import Row

csvDF = rdd.map(lambda x: Row(Index = str(x.split("|")[0]),
Context = str(x.split("|")[1]),
Date = str(x.split("|")[2]),
Tweet_ID = str(x.split("|")[3]),
Retweet = str(x.split("|")[5]),
Username = str(x.split("|")[10]))).toDF()

csvDF.show()


Include in assignement:
#specifies the number of workers and distributes the content of the RDD to those workers:
Mydata = sc.parallelize([1,2,3,5],3)
Mydata
OR
Mydata_larger = sc.parallelize[x for x in range(10000)]


If retweet = 1.0
If mention column = 1.0


#use lambda to create a filter: (or should I use a .map function??)

1
 #Identify (and split?) the 25 separate contexts
Contexts = lines.filter(lambda x: “****insert each contect**** in x) <- is there a way of 
identifying each independent context

2
#Figure out which usernames have the most retweets and mention per context
Tweets = lines.filter(lambda x: “1.0” in x)?
#We need to count the number or tweets and mentions and rank in descending order
Tweets.count()

3
#show the top 10 (for each context)

You can link all of these together into something like:
Lines.filter(lambda x: “inferno” in x).map(lambda s: s.upper()).take(5)

OR

You can define functions:

Def uppercase(doc)
	Return doc.map(lambda s: s.upper())

Def filterDocForTerm(doc, term):
	Return doc.filter (lambda x: term in x)

Part 3

For each context, create a separate graph projection 
Call GDS library methods to compute properties of that context network:

-	The label propagation community detection algorithm

-	The degree centrality for each node

Website that explains it all:
https://towardsdatascience.com/getting-started-with-neo4j-in-10-minutes-94788d99cc2b

Code:

MATCH(c:Context),(x:User)
WHERE c.Name="wear-purple-for-jia-2018"AND x.Name="foomooboo"
CREATE(c)-[r:TWEET]->(o)
RETURN c,x,o
 
MATCH(c:FromUser),(x:ToUser)
WHERE c.Name="foomooboo"AND x.Name="Ed_Miliband"
CREATE(c)-[r:TWEET]->(x)
RETURN c,r,x

LOAD CSV FROM 'https://github.com/Knoxyherself/Big-Data-Assignment/blob/main/uu.csv' AS row
RETURN row
LIMIT 20


AS line CREATE (:User {Tweeter: line.Name, Context: (line.Context)})

LOAD CSV WITH HEADERS FROM 'https://github.com/Knoxyherself/Big-Data-Assignment/blob/main/uu.csv' AS line CREATE (Tweet:Tweet {TweetContext:tweet.context, from:tweet.from, to:tweet.to, weight: tweet.weight})
CREATE (from)-[:TWEET]->(to)



25 context networks
Each node and edge belong to a different context
Call GDS library methods to compute the properties of that context network 

EDGE BETWEENNESS CENTRALITY =  The number of shortest paths among all pairs of nodes within the network passing through that edge 

Label propogation: we use asynchronous propogation 

Tweet = weighted edge
User – node  

LOAD CSV FROM 'https://github.com/Knoxyherself/Big-Data-Assignment' AS row
RETURN row
LIMIT 20


Label propogation example has weights 

#show the top 10 (for each context)

You can link all of these together into something like:
Lines.filter(lambda x: “inferno” in x).map(lambda s: s.upper()).take(5)

OR

You can define functions:

Def uppercase(doc)
	Return doc.map(lambda s: s.upper())

Def filterDocForTerm(doc, term):
	Return doc.filter (lambda x: term in x)

Part 3

For each context, create a separate graph projection 
Call GDS library methods to compute properties of that context network:

-	The label propagation community detection algorithm

-	The degree centrality for each node

Website that explains it all:
https://towardsdatascience.com/getting-started-with-neo4j-in-10-minutes-94788d99cc2b

Code:

MATCH(c:Context),(x:User)
WHERE c.Name="wear-purple-for-jia-2018"AND x.Name="foomooboo"
CREATE(c)-[r:TWEET]->(o)
RETURN c,x,o
 
MATCH(c:FromUser),(x:ToUser)
WHERE c.Name="foomooboo"AND x.Name="Ed_Miliband"
CREATE(c)-[r:TWEET]->(x)
RETURN c,r,x

LOAD CSV FROM 'https://github.com/Knoxyherself/Big-Data-Assignment/blob/main/uu.csv' AS row
RETURN row
LIMIT 20


AS line CREATE (:User {Tweeter: line.Name, Context: (line.Context)})

LOAD CSV WITH HEADERS FROM 'https://github.com/Knoxyherself/Big-Data-Assignment/blob/main/uu.csv' AS line CREATE (Tweet:Tweet {TweetContext:tweet.context, from:tweet.from, to:tweet.to, weight: tweet.weight})
CREATE (from)-[:TWEET]->(to)

LOAD CSV WITH HEADERS FROM "file:///movies.csv" AS csvLine
MERGE (country:Country {name: csvLine.country})
CREATE (movie:Movie {id: toInteger(csvLine.id), title: csvLine.title, year:toInteger(csvLine.year)})
CREATE (movie)-[:ORIGIN]->(country)

Need to create a user node that has a context label and a weight label
We’ll have a user-user relationship
What is the type?
What is an edge? 


25 context networks
Each node and edge belong to a different context
Call GDS library methods to compute the properties of that context network 

EDGE BETWEENNESS CENTRALITY =  The number of shortest paths among all pairs of nodes within the network passing through that edge 

Label propogation: we use asynchronous propogation 

Tweet = weighted edge
User – node  

LOAD CSV FROM 'https://github.com/Knoxyherself/Big-Data-Assignment' AS row
RETURN row
LIMIT 20
sudo mv hdfs://sandbox-hdp.hortonworks.com:8020/user/maria_dev/data/uu.csv /var/lib/neo4j/import


hdfs://sandbox-hdp.hortonworks.com:8020/user/coursework/data/data


Got nodes:

load csv with headers from 'https://raw.githubusercontent.com/Knoxyherself/Big-Data-Assignment/main/uu.csv' AS row 

CREATE (a:Tweeter { Name: row.from}) 
CREATE (b:Tweeter { Name: row.to}) 
RETURN a,b 
LIMIT 20


load csv with headers from 'https://raw.githubusercontent.com/Knoxyherself/Big-Data-Assignment/main/uu.csv' AS row 
MATCH (c:Context {Name: row.context= "dry-january-2018"})
CREATE (a:Tweeter { Name: row.from}) 
CREATE (b:Tweeter { Name: row.to}) 
CREATE (a)-[r:TWEET]->(b)C



r.weight = toInteger(row.Weight);


Each network is distinguished by the context, so we need to separate each context (i.e. filter by “jeans-for-genes day” by creating a named graph. 
We need to project out “jeans-for-genes-day”. “Dry-january day….)
First we need a named graph for each context. 
One we have this big graph database of all 25 networks, we can use the algorithms. 

CALL gds.graph.create.cypher(
    'my-cypher-graph',
    'MATCH (n:City) RETURN id(n) AS id, n.stateId AS community, n.population AS population',
    'MATCH (n:City)-[r:ROAD]->(m:City) RETURN id(n) AS source, id(m) AS target, r.distance AS distance, coalesce(r.condition, 1.0) AS quality'
) 

load csv with headers from 'https://raw.githubusercontent.com/Knoxyherself/Big-Data-Assignment/main/uu.csv' AS row
CREATE (a:Tweeter { Name:row.from})
CREATE (b:Tweeter { Name:row.to})
CREATE (a)-[r:TWEET {Weight:row.weight}]->(b)
RETURN a,b,r
#Don’t need but nice to have:
ORDER BY r.weight DESC
