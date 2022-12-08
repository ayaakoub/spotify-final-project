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

## Data Exploration 
We used Python code to examine the records. For example, we examined how many tracks were in each type of genre, which ones were underrepresented? Which features likely had no bearing on whether it was a hit (such as key or tempo)? How many tracks could be removed from various genres that were not likely to be musical “hits” such as comedy?


## Machine Learning
### Data Processing
  - The target is to build a machine learning model to interpret a track is a hit song or not. After inspect the raw data, we decided to determine a track is a hit song or not base on it's popularity, if it's popularity is over 50 than it will be consider as a hit song. So first, we imported the raw CSV file into Panda dataframe. Then add a new column 'hit' to the dataframe and assign either 0 or 1 to the column for each track base on it's popukarity. 
  - Next, we dropped the rows with non-popular genre such as 'comedy' and 'sleep' etc. 
  - Then group similar genres and reduce total genre number to 13.
  - Drop rows with null value.
  - Drop 'track_genre' column.
  - Separate artists, album_name, track_name, track_id, duration_ms, time_signature, key, mode, and popularity columns into a new dataframe track_df as these columns will noy be used in the machine learning model.
  - create a new datafram df2 which holds the features that will be use in the machine learning model.
  - Load dataframe df2 into sqlite table ('songs') and dataframe track_df into sqlite table ('trackinfo').
  
### Feature Engineering/Selection
  - The features 'duration_ms', 'time_signature', 'key', 'mode' are removed, as we think as a common people, we woldn't know what time_signature, key and mode will mean to a track, and whether a track is popular or not is not determined by the duration_ms. So all these 4 features should'd make any impact to the hit status of a track.
  - Since we will use OneHotEncoder to transform the categorical feature into binary feature, we grouped similar genres to reduce posible number of columns.
  - StandardScaler from sklearn is used to scale the 'loudness' and 'tempo' columns 

### Training and Testing sets
  - The column 'hit' is set as our y value which is our target.
  - Everything else except 'hit' and "track_id', is set as our x value, the independat features.
  - then x and y are split into training and testing data sets using train_test_split from sklearn.

### Model Choice
  - 3 machine learning models are tested Neutral Network, Logistic Regression and Random forest.
  - Neural Network is flexible, can be used on regression and classification problems. Good for nonlinear data with large number of inputs such as images. But Neural networks depend a lot on training data, and this leads to the problem of over-fitting and generalization.
  - Logistic Regression is easy to set up and train and it is efficient if the data is linearly separable. But it fails to predict a continuous outcome,and it assumes linearity between the predicted (dependent) variable and the predictor (independent) variables, also it may not be accurate if sample size is too small.
  - Random forest can perform both regression and classification tasks, works well with both categorical and continuous values, and good against overfitting. But Random Forests can be computationally intensive for large datasets and it is like a black box algorithm, you have very little control over what the model does. 

### Result of Analysis
  - Neural Network
    At first, We started the neural Network model with 2 hidden layers, 54 neurons in 1st layer and 30 neurons in 2nd layers, got a accuracy score of 74%. Then we added a 3rd hidden layer with 15 neurons and improved the accuracy score to 75%.
    
    ![image](https://user-images.githubusercontent.com/108709071/205805423-29ec9f0d-4452-4d63-8b27-9ec086bbb482.png)

  - Logistic Regression
    The Logistic model shows a accuracy score of 74%.
    
    ![image](https://user-images.githubusercontent.com/108709071/205805497-a045e1e5-be3f-4fe8-b25f-b4e4262a358c.png)

  - Random Forest
    The Random Forest model has the highest accuracy score of 82%.
    
    ![image](https://user-images.githubusercontent.com/108709071/205805541-e0271ff4-0bef-4c46-8a9c-2e319a6d6332.png)

  - According to the accuracy scores above, we can see that the Random Forest model has the highest accuracy of 82%. We can say that the Random Forest model is pretty accurate to determine whether a track is a hit song or not.
  - From the importance test, we can see that 'acousticness', 'loudness', 'danceability', 'valence', 'tempo', 'speechiness', 'energy', 'liveness', 'instrumentalness' are of similar importance, being 0.10 or more, and 'explicit' is not as important as other features with only 0.007.
  - The importance between different genres are ranging from 0.0027 to 0.0141, with genre_Jazz_Blues being the lowest and genre_Pop being the highest
  
  ![image](https://user-images.githubusercontent.com/108709071/205806839-75495664-7163-4cae-b555-176103e964d6.png)
  
### Recommandations for Future Analysis
  - Bring in larger dataset
  - testing on different years data
  - Combining genres
  - testing with more other machine learning models

## Dashboard
Tools used:
- HTML
- JS
- CSS
- Flask
- SQLAlchemy
- Tableau

![image](https://user-images.githubusercontent.com/107721712/205207779-2253d087-49f4-44ff-9303-01c8f29bdb45.png)</br>
## Link to Google Slides presentation
Link:
https://docs.google.com/presentation/d/1lWtTW_outLUK36EXIL17RH0IRR2bMdTED2p6CjRtJ0o/edit?usp=sharing
