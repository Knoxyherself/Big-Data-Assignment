# Big Data Assignment
## _Samantha Knox C 1000466_

## - ✨Part 1✨ 

- Login: root
- Password: Sammy100!
- See Appendix A for copy of Pig Scripts (TWEET, RETWEET, MENTIONS)
Define CSVLoader org.apache.pig.piggybank.storage.CSVLoader();                  
TWEET = LOAD 'hdfs://sandbox-hdp.hortonworks.com:8020/user/coursework/data/data/TWEET*.csv' USING CSVLoader()                  
AS (index:int,context:chararray,date:chararray,tw_id:chararray,is_media:chararray,is_retweet:chararray,no_likes:chararray,no_re
tweets:chararray,reply:chararray,text:chararray,user_name:chararray);           
DESCRIBE TWEET;                                                                 
STORE TWEET INTO 'root/user/Uni_Assignment/TWEET' USING PigStorage('|');


- Drag and drop images (requires your Dropbox account be linked)
- Import and save files from GitHub, Dropbox, Google Drive and One Drive
- Drag and drop markdown and HTML files into Dillinger
- Export documents as Markdown, HTML and PDF

## - ✨Part  2✨

Markdown is a lightweight markup language based on the formatting conventions
that people naturally use in email.
As [John Gruber] writes on the [Markdown site][df1]
## - ✨Part  3✨


## - ✨Appendix A - Pig Scripts✨

TWEET

> Define CSVLoader org.apache.pig.piggybank.storage.CSVLoader();                                                                 
TWEET = LOAD 'hdfs://sandbox-hdp.hortonworks.com:8020/user/coursework/data/data/TWEET*.csv' USING CSVLoader()                  
AS (index:int,context:chararray,date:chararray,tw_id:chararray,is_media:chararray,is_retweet:chararray,no_likes:chararray,no_re
tweets:chararray,reply:chararray,text:chararray,user_name:chararray);                                                          
DESCRIBE TWEET;                                                                                                                
STORE TWEET INTO 'root/user/Uni_Assignment/TWEET' USING PigStorage('|'); 

RETWEET

> Define CSVLoader org.apache.pig.piggybank.storage.CSVLoader();                                                                 
RETWEET = LOAD 'hdfs://sandbox-hdp.hortonworks.com:8020/user/coursework/data/data/RETWEET*.csv' USING CSVLoader()              
AS (index:int,rt_id:chararray,context:chararray,rt_user:chararray,tw_id:chararray);                                            
DESCRIBE RETWEET;                                                                                                              
STORE RETWEET INTO 'root/user/Uni_Assignment/RETWEET' USING PigStorage('|'); 

MENTIONS

Define CSVLoader org.apache.pig.piggybank.storage.CSVLoader();                                                                 
MENTIONS = LOAD 'hdfs://sandbox-hdp.hortonworks.com:8020/user/coursework/data/data/MENTIONS*.csv' USING CSVLoader()            
AS (index:int,context:chararray,mentions:chararray,tw_id:chararray);                                                           
DESCRIBE MENTIONS;                                                                                                             
STORE MENTIONS INTO 'root/user/Uni_Assignment/MENTIONS' USING PigStorage('|'); 

HASHTAGS_TIMELINES

Define CSVLoader org.apache.pig.piggybank.storage.CSVLoader();                                                                 
HASHTAGS_TIMELINES = LOAD 'hdfs://sandbox-hdp.hortonworks.com:8020/user/coursework/data/data/HASHTAGS_TIMELINES.csv'           
USING CSVLoader()                                                                                                              
AS (index:int,hashtag:chararray,tw_id:chararray,user_id:chararray);                                                            
DESCRIBE HASHTAGS_TIMELINES;                                                                                                   
STORE HASHTAGS_TIMELINES INTO 'root/user/Uni_Assignment/HASHTAGS_TIMELINES' USING PigStorage('|');  

TWEET_RETWEET

Define CSVLoader org.apache.pig.piggybank.storage.CSVLoader();                                                                 
tweetage = LOAD 'hdfs://sandbox-hdp.hortonworks.com:8020/user/coursework/data/data/TWEET*.csv' USING CSVLoader();              
tweetraw = FILTER tweetage BY $0>1;                                                                                            
tweetdetails = FOREACH tweetraw GENERATE $0 AS index, $1 AS context, $2 AS date, $3 AS tw_id, $4 AS is_media, $5 AS is_retweet,
 $6 AS no_likes, $7 AS no_retweets, $8 AS reply, $9 AS text, $10 AS user_name;                                                 
                                                                                                                               
retweetage = LOAD 'hdfs://sandbox-hdp.hortonworks.com:8020/user/coursework/data/data/RETWEET*.csv' USING CSVLoader();          
retweetraw = FILTER retweetage BY $0>1;                                                                                        
retweetdetails = FOREACH retweetraw GENERATE $0 AS index, $1 AS rt_id, $2 AS context, $3 AS rt_user, $4 AS tw_id;              
                                                                                                                               
jointweetretweet = JOIN tweetdetails by tw_id, retweetdetails by tw_id;                                                        
TWEET_RETWEET = FOREACH jointweetretweet GENERATE $0 AS index, $1 AS tw_id, $2 AS mentions, $3 AS rt_id, $4 AS rt_user, $5 AS d
ate, $6 AS context, $7 AS is_media, $8 AS is_retweet,  $9 AS no_likes, $10 AS no_retweets, $11 AS reply, $12 AS text, $13 AS us
er_name;                                                                                                                       
                                                                                                                               
DESCRIBE TWEET_RETWEET;                                                                                                        
STORE TWEET_RETWEET INTO 'root/user/Uni_Assignment/TWEET_RETWEET' USING PigStorage('|');




## Tech

Dillinger uses a number of open source projects to work properly:

- [AngularJS] - HTML enhanced for web apps!
- [Ace Editor] - awesome web-based text editor
- [markdown-it] - Markdown parser done right. Fast and easy to extend.
- [Twitter Bootstrap] - great UI boilerplate for modern web apps
- [node.js] - evented I/O for the backend
- [Express] - fast node.js network app framework [@tjholowaychuk]
- [Gulp] - the streaming build system
- [Breakdance](https://breakdance.github.io/breakdance/) - HTML
to Markdown converter
- [jQuery] - duh

And of course Dillinger itself is open source with a [public repository][dill]
 on GitHub.

## Installation

Dillinger requires [Node.js](https://nodejs.org/) v10+ to run.

Install the dependencies and devDependencies and start the server.

```sh
cd dillinger
npm i
node app
```

For production environments...

```sh
npm install --production
NODE_ENV=production node app
```

## Plugins

Dillinger is currently extended with the following plugins.
Instructions on how to use them in your own application are linked below.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Development

Want to contribute? Great!

Dillinger uses Gulp + Webpack for fast developing.
Make a change in your file and instantaneously see your updates!

Open your favorite Terminal and run these commands.

First Tab:

```sh
node app
```

Second Tab:

```sh
gulp watch
```

(optional) Third:

```sh
karma test
```

#### Building for source

For production release:

```sh
gulp build --prod
```

Generating pre-built zip archives for distribution:

```sh
gulp build dist --prod
```

## Docker

Dillinger is very easy to install and deploy in a Docker container.

By default, the Docker will expose port 8080, so change this within the
Dockerfile if necessary. When ready, simply use the Dockerfile to
build the image.

```sh
cd dillinger
docker build -t <youruser>/dillinger:${package.json.version} .
```

This will create the dillinger image and pull in the necessary dependencies.
Be sure to swap out `${package.json.version}` with the actual
version of Dillinger.

Once done, run the Docker image and map the port to whatever you wish on
your host. In this example, we simply map port 8000 of the host to
port 8080 of the Docker (or whatever port was exposed in the Dockerfile):

```sh
docker run -d -p 8000:8080 --restart=always --cap-add=SYS_ADMIN --name=dillinger <youruser>/dillinger:${package.json.version}
```

> Note: `--capt-add=SYS-ADMIN` is required for PDF rendering.

Verify the deployment by navigating to your server address in
your preferred browser.

```sh
127.0.0.1:8000
```

## License

MIT

**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>