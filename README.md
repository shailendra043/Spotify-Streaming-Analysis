# Spotify-Streaming-Analysis
Tableau Visualization of Spotify's Global streaming data from countries over the world.

Unlocking the treasure trove of music data stored within Spotify is made possible through the Spotify API, a powerful tool for developers. Leveraging Python's Spotipy package, we can tap into this API to extract a plethora of information associated with unique song identifiers. This enables the creation of diverse systems that harness Spotify's extensive music database to enrich various projects and applications.

This project harnesses the robust capabilities of the Spotify API, providing access to a wealth of information about songs and artists available on the platform. This includes a diverse range of features that capture the essence of the audio, such as characteristics like "liveness," "acousticness," and "energy." Additionally, we leverage the API to obtain insights into the popularity of both artists and individual tracks. For more advanced analyses, we can delve into predictive data, such as the anticipated position of each beat within a song. By leveraging this comprehensive API, our project aims to unlock valuable insights and facilitate sophisticated analyses of music data.

## Connecting to Spotify data

### Extracting Song Data From the Spotify API Using Python

To access Spotify's API and utilize its features in our application, we first need to create a Spotify for Developers account. This account is distinct from a regular Spotify account and does not require a premium subscription. After signing up and accessing the dashboard, we can create an application.

```python
import spotipy
from spotipy.oauth2 import SpotifyClientCredentials
```

Once the application is created, we obtain a client ID and a client secret. These credentials serve as authentication keys for our application to interact with the Spotify web API. It's crucial to treat these credentials as sensitive information, similar to a username and password, and avoid sharing them publicly, especially the client secret key. To enhance security, we can store the client secret key in a separate file and include it in the project's .gitignore file if using Git for version control.

### Authenticating with Spotipy

For our project, we have the option to authenticate with the Spotipy library without a specific user in mind. This type of authentication grants us access to general Spotify features, such as viewing playlists. However, it does not provide access to user-specific data, such as their following lists or listening stats.

To authenticate without signing into a user account, we only need the client ID and client secret. With these credentials, we can create a "Spotify" object using the following code:

```python
client_credentials_manager = SpotifyClientCredentials(client_id=cid, client_secret=secret)
sp = spotipy.Spotify(client_credentials_manager = client_credentials_manager)
```

### Extracting data from Global top 200 playlist

```python
playlist_link = "https://open.spotify.com/playlist/37i9dQZEVXbNG2KDcFcKOF?si=1333723a6eff4b7f"
playlist_URI = playlist_link.split("/")[-1].split("?")[0]
track_uris = [x["track"]["uri"] for x in sp.playlist_tracks(playlist_URI)["items"]]
```

```python
for track in sp.playlist_tracks(playlist_URI)["items"]:
    #URI
    track_uri = track["track"]["uri"]
    
    #Track name
    track_name = track["track"]["name"]
    
    #Main Artist
    artist_uri = track["track"]["artists"][0]["uri"]
    artist_info = sp.artist(artist_uri)
    
    #Name, popularity, genre
    artist_name = track["track"]["artists"][0]["name"]
    artist_pop = artist_info["popularity"]
    artist_genres = artist_info["genres"]
    
    #Album
    album = track["track"]["album"]["name"]
    
    #Popularity of the track
    track_pop = track["track"]["popularity"]
```
Save all of this data extracted into a dataframe using pandas, converting it into csv files that we can load into Tableau. 

Note: I performed this for all available countries and dates prior to July 1st, 2019 and combined the csv’s into one file called Spotify_Daily_Streaming. 

## Loading Data into Tableau

Connect to your Global Spotify Excel file as a data source.

![image](https://github.com/heetc27/Spotify-Streaming-Analysis/assets/51861740/590a4b53-439b-4925-ad55-814ec1f57783)

## Representation of Top 50 Global Artists by Stream
![image](https://github.com/heetc27/Spotify-Streaming-Analysis/assets/51861740/629ee218-bace-4572-a3ed-df953fc63e05)

## Dashboard
Global View of:
1.  Number of Streams across all the weeks.
2.  Number of Tracks vs Streams.
3.  The Most Popular Tracks based on number of Streams.
![image](https://github.com/heetc27/Spotify-Streaming-Analysis/assets/51861740/5ee07876-97e4-4382-97c4-33bc1ed442ea)

## Global Insights
### Best and Worst Performers

![image](https://github.com/heetc27/Spotify-Streaming-Analysis/assets/51861740/78b8266b-17bc-476e-81c9-6df34052fee4)
<li> The artists Post Malone and Drake standout as the most streaming and popular artists.
<li> Jul stands out as the artist with the least popularity for the maximum number of tracks in the dataset.

![image](https://github.com/heetc27/Spotify-Streaming-Analysis/assets/51861740/0a91a2bc-e0f2-40f9-9e24-fa4126f5fcd6)

Post Malone exhibits extremely high popularity with less number of tracks. With over 7,800,000,000 for only 44 tracks.

![image](https://github.com/heetc27/Spotify-Streaming-Analysis/assets/51861740/bc0a2213-d4dc-4bb7-adcb-863a3a6e2957)

While Drake has a great number of tracks along with high streams. With over 6,500,000,000 for 115 tracks.

## Country wise insights
With Tableau's filtering capability of dashboard, the filtered visualization for a country can simply be viewed by clicking the country on the map visualization.

### Spotify Streaming Analysis for India:

![image](https://github.com/heetc27/Spotify-Streaming-Analysis/assets/51861740/f25dd01f-ff0c-4e85-8880-b80be6a09655)

### Spotify Streaming Analysis for Japan:

![image](https://github.com/heetc27/Spotify-Streaming-Analysis/assets/51861740/3a816c58-53c9-4bbc-9695-b6b8af2ccbd0)
