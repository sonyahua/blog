---
layout: post
title: Parse JSON Responses via Python (Movie DB API)
date:   2016-08-30 12:00:00
tag: [data-visualization, archive]
---
<html>
<head><link rel="stylesheet" href="/css/main.css">
</head>
<p>This post focuses on how to retrieve data from the web using Python, JSON, and APIs. Tapping into APIs is one of my most favorite coding activities since there is a plethora of information you can access nowadays through API's from weather to directions to movie information.</p>

<p>As part of Udacity's Nanodegree Plus program for Full-Stack Web Developers, one of the projects entail creating a static webpage filled with movie info and trailers of your favorite movies. In Python, I can manually enter the movie info for all my favorite movies into a script file or I can somehow automate the retrieval of info from the web using an <a href="https://www.themoviedb.org/documentation/api">API that stores movie info</a>. This post explores how-to using a <a href="http://stackoverflow.com/questions/2835559/parsing-values-from-a-json-file-in-python">JSON parser</a> and <a href="https://pypi.python.org/pypi/tmdbsimple">'tmdbsimple 1.4'</a> module, a python wrapper for The Movie Database API.</p>
<p>As an exercise, I would like to retrieve the movie title, synopsis, and release year of one of my most favorite movies "Joy."</p>

<p><div align="center"><img src="/images/postimages/joy.jpg" width="50%" id="resp-image"></div></p>

<p>The API can take in IMDB movie IDs in order to return info about a specific movie. First, I requested an API key on Movie DB's site. Then I googled IMDB's movie ID for "Joy" which is <b>'tt2446980'</b>. I will be using this movie ID in my URL code to ask for more info about "Joy":</p>

<pre><code>
<h1># Python Code by Sonya Hua</h1>
import json
import urllib2
import tmdbsimple as tmdb

#Retrieve an API key from Movie Database API
tmdb.API_KEY = '69f77b122c6932f085d9c8e992fe70ad'
imdb_id= 'tt2446980'   <cmt> #Imdb's movie ID for the move Joy </cmt>

def search_movie_info():
    """Fetches movie info from Movie Database"""
    
    #open and read url
    connection=urllib2.urlopen("https://api.themoviedb.org/3/find/"
                              <b>+imdb_id+</b>"?external_source=imdb_id&"
                              "api_key="<b>+tmdb.API_KEY</b>)
    output=connection.read()
	.....
</code></pre>

<br>
<p>The resulting read() produces a response in JSON format: </p>

<pre><code><cmt>
{u'tv_season_results': [], u'tv_episode_results': [], u'person_results': [],
 u'tv_results': [], u'movie_results': [{u'poster_path': u'/zNjxzdgSwzRXnP8Stu3HGzKQKWp.jpg',
  u'title': u'Joy', u'overview': u"A story based on the life of a struggling Long Island 
  single mom who became one of the country's most successful entrepreneurs.", u'release_date':
   u'2015-12-24', u'popularity': 3.609492, u'original_title': u'Joy', u'backdrop_path': 
   u'/5nBIWhdexEU0peSUK0wZEkjgy6h.jpg', u'vote_count': 793, u'video': False, u'adult': False, 
   u'vote_average': 6.3, u'genre_ids': [35, 18], u'id': 274479, u'original_language': u'en'}]}
   
</cmt></code></pre>
<br>
<p>Notice the appending 'u's next to each fieldset; nothing to worry about here. JSON is simply telling me that the code is in unicode. It can be removed easily by replacing the u with '[0]' in below code. Also, observe that there are 2 layers of data in the JSON response: data that starts with tv_... and data that starts with movie_results[...]. The data I am interested in is actually located in 'movie_results' element, and I must specify this in below code. We parse the data using <b>JSON</b> module, and then extract the specific fields by  using [] brackets such as ['movie_results'] and ['year'].</p>

<pre><code>
	.....
    <cmt>#load to-be-parsed data into JSON module</cmt>
    json_output=json.loads(output)
    
    <cmt>#parse/extract certain fieldsets or attributes from JSON response </cmt>
    title= (json_output['movie_results'][0]['title'])
    info= (json_output['movie_results'][0]['overview'])
    release_date=(json_output['movie_results'][0]['release_date'])
    year= release_date[:4]

    <cmt>#print out the results of specific attributes</cmt>
    print(title)
    print(info)
    print(year)
    
search_movie_info()

</code></pre>
<br>
<p> After running this code, I get the results I want from the API; the movie title, info, and release year of "Joy."

<pre><code><cmt>
Joy
A story based on the life of a struggling Long Island single mom
 who became one of the country's most successful entrepreneurs.
2015
</cmt></code></pre>
