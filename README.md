Music Recommendation System 

Problem Definition

The context: Why is this problem important to solve?
With the ever-increasing volume of songs becoming available on the Internet,searching for songs of interest has become a tedious task in itself for users.
Every Internet based company wants to increase customer time spent on their platform and increase company's revenue. 
By using smart recommendation systems(one like Spotify) that can recommend songs based on users’ likes/dislikes among millions of customers and billions of songs would be Win-Win for customers and internet based companies.

The objectives: What is the intended goal?
Build a recommendation system to propose the top 10 songs for a user based on the likelihood of them listening to those songs.
Build recommendation system to increase customer time spent on their platform and increase company's revenue.

The key questions: What are the key questions that need to be answered?
Main question is to figure out what kind of content customers are most likely to consume.
What are the most popular songs to suggest a new user.
Identify songs based on ratings, reviews, artists, genre, year released etc.
Identify songs for existing users that are similar to their listening history.
Identify users who have similar tastes in music and recommend similar songs to them.

The problem formulation: What are we trying to solve using data science?
Build recommendation system using different models.
For new users who have not history/data, we build recommendation systems based on populatrity and recommend popular songs.
For existing users we build recommendation system models using collaborative filtering, matrix factorization and other methods. We then compare the efficiancy of the models and choose the best one to recommend songs to users.

Data Dictionary
The core data is the Taste Profile Subset released by the Echo Nest as part of the Million Song Dataset. There are two files in this dataset. The first file contains the details about the song id, titles, release, artist name, and the year of release. The second file contains the user id, song id, and the play count of users.

song_data
song_id - A unique id given to every song
title - Title of the song
Release - Name of the released album
Artist_name - Name of the artist
year - Year of release
count_data
user _id - A unique id given to the user
song_id - A unique id given to the song
play_count - Number of times the song was played


Data Source
http://millionsongdataset.com/
