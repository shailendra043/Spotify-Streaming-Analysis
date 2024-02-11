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

```python
playlist_link = "https://open.spotify.com/playlist/37i9dQZEVXbNG2KDcFcKOF?si=1333723a6eff4b7f"
playlist_URI = playlist_link.split("/")[-1].split("?")[0]
track_uris = [x["track"]["uri"] for x in sp.playlist_tracks(playlist_URI)["items"]]
```

