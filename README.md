# Spotify Final Project

## Selected Topic and Reason 

We analyzed a dataset of Spotify tracks over a range of 125 different genres, including a 114,000 tracks to see which features are the most predictive in determining the popularity of the track. We plan on using Python, Pandas, Flask, Tableau, among others. Our hope is to produce a web page that will share the findings, enabling a user to explore the data and enter characteristics to predict the popularity of a track. 

We chose this topic as our entire group is highly interested in music and wanted to have a better understanding of how a track becomes a hit. 

## Questions they hope to answer with the data

- What features are the most predictive in determining track popularity?
- What are the optimal combination of features for popular tracks?
- Are there any differences across genres?

## Description of the communication protocols

Our group will meet regularly during class times (Tuesdays and Thursdays from 7 to 9 pm). We will also be meeting on the weekend, with date and time being decided during our class time based on availability. We will be assigning separate tasks for completion and following up during our meetings. We also have a channel set up on slack for regular day-to-day communication. 

## Data ERD
https://app.quickdatabasediagrams.com/#/d/Fc0Y2R </br>
![image](https://user-images.githubusercontent.com/107721712/202347548-5c6d9ba7-8e67-4a60-bda4-b2f5694f8fef.png)

## Data Source:
Data was sourced from Kaggle.com. It includes 14,000 different tracks from Spotify API, approximately 1,000 tracks per different genre. And the raw data includes the following features:

  - track_id: The Spotify ID for the track.
  - artists: The artists' names who performed the track
  - album_name: The album name in which the track appears
  - track_name: Name of the track
  - popularity: The popularity of a track is a value between 0 and 100, with 100 being the most
  - duration_ms: The track length in milliseconds
  - explicit: Whether or not the track has explicit lyrics (true = yes it does; false = no it does not OR unknown)
  - danceability: Danceability describes how suitable a track is for dancing based on a combination of musical elements including tempo, rhythm stability, beat strength, and overall regularity. A value of 0.0 is least danceable and 1.0 is most danceable
  - energy: Energy is a measure from 0.0 to 1.0 and represents a perceptual measure of intensity and activity. Typically, energetic tracks feel fast, loud, and noisy. For example, death metal has high energy, while a Bach prelude scores low on the scale
  - key: The key the track is in. Integers map to pitches using standard Pitch Class notation. E.g. 0 = C, 1 = C♯/D♭, 2 = D, and so on. If no key was detected, the value is -1
  - loudness: The overall loudness of a track in decibels (dB)
  - mode: Mode indicates the modality (major or minor) of a track, the type of scale from which its melodic content is derived. Major is represented by 1 and minor is 0
  - speechiness: Speechiness detects the presence of spoken words in a track. The more exclusively speech-like the recording (e.g. talk show, audio book, poetry), the closer to 1.0 the attribute value. Values above 0.66 describe tracks that are probably made entirely of spoken words. Values between 0.33 and 0.66 describe tracks that may contain both music and speech, either in sections or layered, including such cases as rap music. Values below 0.33 most likely represent music and other non-speech-like tracks
  - acousticness: A confidence measure from 0.0 to 1.0 of whether the track is acoustic. 1.0 represents high confidence the track is acoustic
  - instrumentalness: Predicts whether a track contains no vocals. "Ooh" and "aah" sounds are treated as instrumental in this context. Rap or spoken word tracks are clearly "vocal". The closer the instrumentalness value is to 1.0, the greater likelihood the track contains no vocal content
  - liveness: Detects the presence of an audience in the recording. Higher liveness values represent an increased probability that the track was performed live. A value above 0.8 provides strong likelihood that the track is live
  - valence: A measure from 0.0 to 1.0 describing the musical positiveness conveyed by a track. Tracks with high valence sound more positive (e.g. happy, cheerful, euphoric), while tracks with low valence sound more negative (e.g. sad, depressed, angry)
  - tempo: The overall estimated tempo of a track in beats per minute (BPM). In musical terminology, tempo is the speed or pace of a given piece and derives directly from the average beat duration
  - time_signature: An estimated time signature. The time signature (meter) is a notational convention to specify how many beats are in each bar (or measure). The time signature ranges from 3 to 7 indicating time signatures of 3/4, to 7/4.
  - track_genre: The genre in which the track belongs

## Machine Learning
### Data Processing
  - The target is to build a machine learning model to interpret a track is a hit song or not. After inspect the raw data, we decided to determine a track is a hit song or not base on it's popularity, if it's popularity is over 50 than it will be consider as a hit song. So first, we imported the raw CSV file into Panda dataframe. Then add a new column 'hit' to the dataframe and assign either 0 or 1 to the column for each track base on it's popukarity. 
  - Next, we dropped the rows with non-popular genre such as 'comedy' and 'sleep' etc. 
  - Then group similar genres and reduce total genre number to 13.
  - Drop rows with null value.
  - Drop 'track_genre' column.
  - 

## Link to Google Slides presentation
Link:
https://docs.google.com/presentation/d/1lWtTW_outLUK36EXIL17RH0IRR2bMdTED2p6CjRtJ0o/edit?usp=sharing
