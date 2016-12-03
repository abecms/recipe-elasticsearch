# ElasticSearch Abe Recipe
This Abe recipe demonstrates how to setup abe-elasticsearch plugin and use it on the frontend

![Screenshot](/site/screenshot.png?raw=true)

# Installation
1. git clone https://github.com/Abejs/recipe-elasticsearch.git
2. cd recipe-elasticsearch
3. abe install gregorybesson/abe-elasticsearch
4. abe serve
5. open your browser at the address : http://localhost:3000/abe/editor
6. Enjoy !

# Description
In this demo, you'll see 
- different templates illustrating Elasticsearch usage (auto-complete, live search)
- the Elasticsearch console

These templates uses jquery and jquery-ui to query elasticsearch. The usage of jquery and elasticsearch are not directly related to Abe. It's an illustration of how you can add a search engine on your Abe static website: Using the plugin abe-elasticsearch, each time a contributor publish a content from the Abe editor, this content is indexed by an Elasticsearch instance and available on your front.

You'll find also a "default" template to create regular content and already published content to ease your discovery. Don't hesitate to add content and test with this recipe.

## The autocomplete template
This template includes a partial containing jquery + jquery-ui autocomplete which requests your elasticsearch instance.

## The livesearch template
This template uses jquery to live search blog posts on your elasticsearch instance.

## The abe-elasticsearch plugin console /abe/plugin/abe-elasticsearch/console
You'll be able to index or reindex your whole Abe website in a breeze. As soon as the index is finished, you'll be able to search your content on your Elasticsearch instance from the front.