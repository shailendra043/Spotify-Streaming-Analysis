# Spotify-Streaming-Analysis
Tableau Visualization of Spotify's Global streaming data from countries over the world.

Unlocking the treasure trove of music data stored within Spotify is made possible through the Spotify API, a powerful tool for developers. Leveraging Python's Spotipy package, we can tap into this API to extract a plethora of information associated with unique song identifiers. This enables the creation of diverse systems that harness Spotify's extensive music database to enrich various projects and applications.

This project harnesses the robust capabilities of the Spotify API, providing access to a wealth of information about songs and artists available on the platform. This includes a diverse range of features that capture the essence of the audio, such as characteristics like "liveness," "acousticness," and "energy." Additionally, we leverage the API to obtain insights into the popularity of both artists and individual tracks. For more advanced analyses, we can delve into predictive data, such as the anticipated position of each beat within a song. By leveraging this comprehensive API, our project aims to unlock valuable insights and facilitate sophisticated analyses of music data.

## Connecting to Spotify data

### 1. Extracting Song Data From the Spotify API Using Python

To access Spotify's API and utilize its features in our application, we first need to create a Spotify for Developers account. This account is distinct from a regular Spotify account and does not require a premium subscription. After signing up and accessing the dashboard, we can create an application.

Once the application is created, we obtain a client ID and a client secret. These credentials serve as authentication keys for our application to interact with the Spotify web API. It's crucial to treat these credentials as sensitive information, similar to a username and password, and avoid sharing them publicly, especially the client secret key. To enhance security, we can store the client secret key in a separate file and include it in the project's .gitignore file if using Git for version control.

'''python
import spotipy
from spotipy.oauth2 import SpotifyClientCredentials
'''
