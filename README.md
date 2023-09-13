# Music-Recommendation-System-for-Group
Music recommendation system for group of peopl by Content-based filtering.

Lets start from the `Data.zip` file. It contains `mpd.slice.0-999.json`, `raw_data.csv`, `processed_data.csv`, `allsong_data_final.csv`, `complete_feature_final.csv` and 
`test_playlist.csv`. The only file that is initially needed for this project is the `mpd.slice.0-999.json`, all the other files besides `test_playlist.csv` are generated by 
python scripts inside the `Data Processing` folder. The `mpd.slice.0-999.json` file contains information about 1000 Spotify playlists. This is 1 of 1000 json files available in the "Spotify Million Playlist Dataset" from "https://www.aicrowd.com/challenges/spotify-million-playlist-dataset-challenge/dataset_files#". You can of course do this project using all the "Spotify Million Playlist Dataset", but it will require huge time and resources.

Lets discuss the python files inside the `Data Processing` folder. Firstly, the `load_data.py` script takes the path of the `mpd.slice.0-999.json` and extracts all the songs from all the playlists inside it, by storing them in the `raw_data.csv` (it was mentioned above).

Now is the time to speak about the `processing_data.ipynb`. This script shows how we gather features of each song from the `raw_data.csv` (mentioned above), by using the 
Spotify API calls. The features of the song are `danceability`, `energy`, `artist_pop`, `genres` and many more.  The values of 'cid' and 'secret' variables inside the script, should be the Spotify Client App credentials (check the video "https://www.youtube.com/watch?v=WAmEZBEeNmg"). Then the script outputs all the songs with their features into `processed_data.csv` (it was mentioned above).

We reach the most important script of this project that is `Final_Model_ISP.ipynb`. This script takes the `processed_data.csv` and processes it. Firstly it takes the features which
will be useful for the further analysis and model building. Afterwards it starts to develope the features by using different techniques, such as sentiment anlysis, TF-IDF, OHE, normalization. By combining all the features the script generates the dataframe (database-matrix) which will be used for recommendation and outputs it that to `complete_feature_final.csv` (it was mentioned above). In the meantime it outputs all the songs without analyzed features to `allsong_data_final.csv`. To continue, the script takes `test_playlist.csv` which is basically songs from a playlist for which we should recommend the songs. Then the `test_playlist.csv` is being processed in the same way as our
raw data was processed. After that the script uses two ways of recommendation for the playlist. 
  The first version of recommendation uses similarity matrix, which is created from the complete feature set and the playlist feature set. Then it recommends the best suited songs   for each song from the playlist separately.
  The second version takes the entire playlist, for which the recommendation should me made, and converts it into a single vector, then uses cosine similarity to find appropriate    tracks for it. It uses the mean of the playlist feature matrix (weighted mean in the future version) to vectorize it.
  Both versions are type of Content-based filtering.

Now lets speak about the `test_playlist.csv` and how it is gathered (!!! This part is not implemented yet). So the process will be the following: the program will ask each user
to rate ~20 musics, which will be taken by Spotify API, from charts of Spotify. Then it will take the ratings and filters the song by the treshold. Then puts them into the `test_playlist.csv` and then you know everything (explained from the start).


