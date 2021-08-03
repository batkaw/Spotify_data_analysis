# Spotify_data_analysis

## Introduction

Music streaming services have become the most popular method for consumers to listen to music. With over 36% market share among online music subscribers and having a base of over 100 million subscribers, Spotify occupies the top spot. Being able to predict that something might be popular beforehand is an important research for every industry. This project's goal is develop a model that predicts the popularity of the song.

## Spotify Exploratory Data Analysis

In this EDA, we will take a look at the features of the dataset, closer look at few of them in order to have a better understanding for the rest of the analysis. In order to access them a bit more practically, we need a definition of the features. Here are definition of features.


## Feature Definitions

1. artists: The list of artists of the song
2. danceability: Danceability describes how suitable a track is for dancing based on a combination of musical elements including tempo, rhythm stability, beat strength, and overall regularity. A value of 0.0 is least danceable and 1.0 is most danceable.
3. duration_ms: The duration of the track in milliseconds
4. energy: Energy is a measure from 0.0 to 1.0 and represents a perceptual measure of intensity and activity. Typically, energetic tracks feel fast, loud, and noisy. For example, death metal has high energy, while a Bach prelude scores low on the scale. Perceptual features contributing to this attribute include dynamic range, perceived loudness, timbre, onset rate, and general entropy. (Float)
5. explicit: The content item is explicit and the user’s account is set to not play explicit content. Additional reasons may be added in the future. Note: If you use this field, make sure that your application safely handles unknown values.
6. instrumentalness: Predicts whether a track contains no vocals. “Ooh” and “aah” sounds are treated as instrumental in this context. Rap or spoken word tracks are clearly “vocal”. The closer the instrumentalness value is to 1.0, the greater likelihood the track contains no vocal content. Values above 0.5 are intended to represent instrumental tracks, but confidence is higher as the value approaches 1.0.
7. The key the track is in. Integers map to pitches using standard Pitch Class notation . E.g. 0 = C, 1 = C♯/D♭, 2 = D, and so on.
8. liveness: Detects the presence of an audience in the recording. Higher liveness values represent an increased probability that the track was performed live. A value above 0.8 provides strong likelihood that the track is live.
9. loudness: The overall loudness of a track in decibels (dB). Loudness values are averaged across the entire track and are useful for comparing relative loudness of tracks. Loudness is the quality of a sound that is the primary psychological correlate of physical strength (amplitude). Values typical range between -60 and 0 db.
10. mode: Mode indicates the modality (major or minor) of a track, the type of scale from which its melodic content is derived. Major is represented by 1 and minor is 0.
11. name: Name of the song.
12. popularity: The popularity of the track. The value will be between 0 and 100, with 100 being the most popular. The popularity of a track is a value between 0 and 100, with 100 being the most popular. The popularity is calculated by algorithm and is based, in the most part, on the total number of plays the track has had and how recent those plays are. Generally speaking, songs that are being played a lot now will have a higher popularity than songs that were played a lot in the past. Duplicate tracks (e.g. the same track from a single and an album) are rated independently. Artist and album popularity is derived mathematically from track popularity. Note that the popularity value may lag actual popularity by a few days: the value is not updated in real time.
13. release_date: The date the album was first released, for example “1981-12-15”. Depending on the precision, it might be shown as “1981” or “1981-12”.
14. speechiness: Speechiness detects the presence of spoken words in a track. The more exclusively speech-like the recording (e.g. talk show, audio book, poetry), the closer to 1.0 the attribute value. Values above 0.66 describe tracks that are probably made entirely of spoken words. Values between 0.33 and 0.66 describe tracks that may contain both music and speech, either in sections or layered, including such cases as rap music. Values below 0.33 most likely represent music and other non-speech-like tracks.
15. tempo: The overall estimated tempo of a track in beats per minute (BPM). In musical terminology, tempo is the speed or pace of a given piece and derives directly from the average beat duration.
16. valence: A measure from 0.0 to 1.0 describing the musical positiveness conveyed by a track. Tracks with high valence sound more positive (e.g. happy, cheerful, euphoric), while tracks with low valence sound more negative (e.g. sad, depressed, angry).
17. year: Year information extracted from release_date.


## Correlations

Let's see the correlations between continous metrics

![image](https://user-images.githubusercontent.com/43426359/128095093-f9ae1000-63f0-48cf-826f-5a99f01198d4.png)

* As expected, popularity is highly correlated with the year released. This makes sense as the Spotify algorithm which makes this decision generates its “popularity” metric by not just how many streams a song receives, but also how recent those streams are.
* Energy also seems to influence a song’s popularity. Many popular songs are energetic, though not necessarily dance songs. Because the correlation here is not too high, low energy songs do have some potential to be more popular.
* Acoustiness seems to be uncorrelated with popularity. Most popular songs today have either electronic or electric instruments in them. It is very rare that a piece of music played by a chamber orchestra or purely acoustic band becomes immensely popular
* Loudness and energy are highly correlated. This makes some sense as energy is definitely influenced by the volume at which the music is being played.

![image](https://user-images.githubusercontent.com/43426359/128095318-b924e41c-e6cc-4c4f-9889-0a30f8247779.png)

![image](https://user-images.githubusercontent.com/43426359/128095758-a08f4d20-9ebd-4be6-818a-e3d41e981022.png)



### Features over the years

![image](https://user-images.githubusercontent.com/43426359/128095510-4de796c7-3e2e-42c6-9aa8-aea66426f60a.png)


1. Acoustiness has decreased significantly. Most tracks past 1960 used electric instruments and, especially past the 1980s, electronic sounds. Most recorded music today includes both electric and electronic elements.
2. Danceability has varied significantly but has stayed mostly at the same level since 1980.
3. Energy seems to be inversely related to Acoustiness: Was very low in the first part of the century, but then rose significantly after 1960. It looks like it increased even more after 2000 as well.





## Modeling


Data was split into a training (80%) and a test set (20%). Using Sklearn classes, this split can be made and fitted to the following model types

* Decision TreeRegressor
* Random ForestRegressor
* Linear Regression 
* GradientBoosting Regressor
* Neural Network

The aim of these modelsis to fit and train the data and test the accuracy of fit. I used GridSearhCV and BayesianOptimization to find the optimal hyperparameters for all the models. 

### Model Evaluation 

I used Root mean squared error (RMSE) and R squared (R2) to evaluate my models. The reason I have chosen R2 score here is that I'm working on regressor model rather than the classifier model. 

![image](https://user-images.githubusercontent.com/43426359/128098443-9181bca9-6e76-4fe4-a735-f28654f79de2.png)

Neural Network RMSE = 11.5288   R2 = 0.7209

![image](https://user-images.githubusercontent.com/43426359/128098471-099a8f63-c03d-4215-b930-a2a921c6c6ab.png)



From the above analysis GradientBoostingRegressor have the most reliable result.


## Summary 

Overall, this was a very fun dataset to work with, and I am pleasantly surprised that I actually obtained fairly accurate results, especially with Gradient Boosting model. It is quite difficult to determine if a song will be a popular or not, and there appear to be other factors at play that are not necessarily included in this dataset.Other factors that influence if a song will be popular or not could potentially be:
* Does a particular artist have any current name recognition?
* Has this artist had any previous hits?
* What is this artist's genre of music?
* Has this artist collaborated with other popular artists?

I assume that merging the data I have now with answers to some of the above questions would definitely allow for a much more accurate prediction of popularity scores.
