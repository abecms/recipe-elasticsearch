# ElasticSearch Abe Recipe
This Abe recipe demonstrates how to setup abe-elasticsearch plugin and use it on the frontend

![Screenshot](/site/screenshot.png?raw=true)

# Installation
1. git clone https://github.com/Abejs/recipe-elasticsearch.git
2. cd recipe-elasticsearch
3. abe install gregorybesson/abe-elasticsearch
4. Once you have an elasticsearch instance ready, configure abe.json and the templates using elasticsearch (jquery-autocomplete and jquery-livesearch) with the host ad port of your elasticsearch instance.
4. abe serve
5. open your browser at the address : http://localhost:3000/abe/plugin/abe-elasticsearch/console and index the blog with your elasticsearch
6. Enjoy ! (go to the site on http://localhost:3000/autocomplete.html or http://localhost:3000/livesearch.html to see elasticsearch in action)

# Description
In this demo, you'll see 
- different templates illustrating Elasticsearch usage (auto-complete, live search)
- the Elasticsearch console

These templates uses jquery and jquery-ui to query elasticsearch. The usage of jquery and elasticsearch are not directly related to Abe. It's an illustration of how you can add a search engine on your Abe static website: Using the plugin abe-elasticsearch, each time a contributor publish a content from the Abe editor, this content is indexed by an Elasticsearch instance and available on your front.

You'll find also "default" templates (index and single) to create regular content and you'll find already published content to ease your discovery. Don't hesitate to add content and test with this recipe.

# Installation
Before enjoying the demo, you must have an elasticsearch instance available. The default configuration in abe.json looks for an instance at 127.0.0.1:9200
Change the config if your elasticsearch instance is located elsewhere.

Once done, index the Abe published content (some articles are already published) with you elasticsearch instance: http://localhost:3000/abe/plugin/abe-elasticsearch/console click on the "index" button.

Once done, all the published posts are indexed in Elasticsearch. If you create a new content and publish it, it will be automatically indexed.

# The autocomplete template
name:jquery-autocomplete
This template includes a partial containing jquery + jquery-ui autocomplete which requests your elasticsearch instance.

A published post already exist: autocomplete.html but you can create your own post. You can also create a partial to add this search feature on all pages.

## How it works
The search query search the term in the Abe fields "article_content", "article_title" and "abe_meta.template"

```
var postData = {
  "query": {
    "query_string": {
      "fields": ["article_content", "article_title", "abe_meta.template"], 
      "query": request.term.toLowerCase() + "*"
    }
  }
}
```
The ajax request then use this query. Note in the "url" that we query localhost:9200. Note also "recipe-elasticsearch". This last entry is the name of your project directory. This name has been used to create an index in your elasticsearch (you can change the name of the index by providing a name in abe.json).
On success, we get the item._source.article_title as label and item_id as id.

```
$.ajax({
  url: "http://localhost:9200/recipe-elasticsearch/_search",
  method: "POST",
  crossDomain: true,
  dataType: "JSON",
  data: JSON.stringify(postData),
  success: function(data) {
    response($.map(data.hits.hits, function(item) {
      return {
        label: item._source.article_title,
        id: item._id
      }
    }));
  },
});
```

# The livesearch template
name:jquery-livesearch
This template uses jquery to live search blog posts on your elasticsearch instance.

A published post already exist: livesearch.html
create your own and try to create a partial you'll use on your header.

# The abe-elasticsearch plugin console /abe/plugin/abe-elasticsearch/console
You'll be able to index or reindex your whole Abe website in a breeze. As soon as the index is finished, you'll be able to search your content on your Elasticsearch instance from the front.
