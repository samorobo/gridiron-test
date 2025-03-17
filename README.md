# Spotify AI

The Playlist Generator App is a web application that enables users to create AI-generated playlists tailored to their preferred music genres. It offers an easy-to-use interface for selecting genres and provides personalized song recommendations.

## Getting started

- **Dynamic Playlist Generation:** Users can select from multiple genres, and the app generates a unique playlist.
- **User Feedback:** Informative UI elements to guide users, including warnings about losing the playlist after navigating away.
- **Interactive Design:** Fully responsive with a modern aesthetic.

##  Screenshot

### 1. Home screen
![Generated Playlist](https://github.com/user-attachments/assets/636ce971-a51e-4f87-aa08-48ff2ea33eaf)


### 2. Generating State
![spotify-3](https://github.com/user-attachments/assets/58c8d1fe-ad3c-423d-936f-b20a9d56fee7)

### 3. Generated Playlist
![spotify-4](https://github.com/user-attachments/assets/39856cd5-986c-4834-8219-7bc9a359e951)

### 4. Confirmation modal for exit with warning
![spotify-5](https://github.com/user-attachments/assets/cc121da7-f57d-4755-915f-61cbbe4e2b89)

## Technologies Used
- **Front-end:** Vue.js, TailwindCSS
- **Back-end:** Flask Framework
- **Text Generation API:** Replicate AI model
- **Deployment:** Gitlab

## 🌐 Live Demo
Explore the live demonstration of the project: [Spotify AI_On_Vercel](https://gridiron-test-5lb5.vercel.app/)

## Notes For Users
- **Data Loss Warning:** Clicking the "Back" button clears the current playlist and resets the app. Ensure you save your playlist before proceeding.
- **Cross-Platform Compatibility:** The app is optimized for desktop and mobile devices.

## ⚙️ Installation and Run 

### 1. Clone the repository
```
https://gridirontest.com/bootcamp-cohort-5/godwin-samuel.git
```
### 2. Navigate to the client directory
```
cd client
cd music_playlist
```
### 3. Install frontend dependencies
```
npm install
```
### 4. Start front-end server
```
npm run dev
```
### 5. Set up the backend
- Navigate to the backend directory open a new terminal instance:
```
cd server
```
- Create a virtual enivironment
  - on mac:
```
python3 -m venv env
 source env/bin/activate
```
  - on windows:
```
python -m venv env
source env\Scripts\activate
```
Please note going forward that python3 is used on Mac while python is used on Windows.
- Install dependencies:
```
pip install -r requirements.txt
```
### 6.  🔒 Set up Enivironment variable at the root of server directory
```
REPLICATE_API_TOKEN=your_api_key
```
### 7. Start backend server:
```
python app.py
```
### 8. Access the app at http://localhost:3000


## API Documentation
### Endpoint: Generate Playlist
- **URL:** `/api/playlist/<genre>`
- **Method:** GET
- **URL Parameter:**
  - genre (string): The music genre for which you want to generate a playlist (e.g., Pop, Rock, Jazz).
### Example Request
```
GET http://127.0.0.1:5000/api/playlist/Jazz
```
### Successful Response
- **Status Code:** ````200 OK````
- **Response Body:**
  
  ![postman-pics](https://github.com/user-attachments/assets/7f7777c6-0440-4a82-af57-fbb733dcf956)
  

## CORS Configuration
During development, the API is configured to allow all routes access using the following setting:
```
CORS(app, origins=["*"], methods=["GET"], allow_headers=["Content-Type"])
```
This configuration permits any origin to access your API's GET endpoints, which is useful for testing across various environments and during development.

## Important note for production
When moving to production, i highly recommended to restrict access to your API. For example, you can update the configuration to only allow requests from your trusted frontend URL. An updated configuration might look like this:
```
CORS(app, origins=["https://your-frontend.vercel.app"], methods=["GET"], allow_headers=["Content-Type"])
```
By limiting access to your specific frontend, you improve the security of your API and prevent unauthorized requests from other domains.


## Usage
### Local Usage
1. Follow the installation instructions to set up the application locally.
2. Select a music genre from the dropdown menu on the interface.
3. Click "Generate Playlist" to create a curated list of songs based on your chosen genre.
4. Use the "Back" button to clear the playlist and select a new genre.

## Hosted Usage
1. The front-end of the application is hosted on Vercel and accessible [Spotify AI](https://gridiron-test-5lb5.vercel.app/)..
2. The back-end is also hosted on Render and is configured to only accept requests from the hosted front-end ip address.


## Areas of Improvement

- [ ] Implement user authentication for personalized playlists.
- [ ] Change the dropdown to a form where users can specify niche genres.
- [ ] Add persistent storage for playlist saving and sharing.
- [x] Host the server

## Support

If you encounter issues or need assistance with the Playlist Generator App, please feel free to open an issue on this repository. To ensure your concerns are addressed quickly, tag the issue as need-help or under-discussion to facilitate visibility.

## 🔧 Contributing
We welcome contributions to Spotify AI! Contributions make open source a great place to learn, inspire, and create. Any contributions you make are greatly appreciated.

To fix a bug or enhance an existing feature:

Fork the repo
Create a new branch: `git checkout -b improve-feature`
Make changes in the files
Commit changes: `git commit -m 'Improve feature`
Push to the branch: `git push origin improve-feature`
Create a Pull Request 🎉

## 📩 Bug / Feature Request
If you find a bug or want to request a feature:

Open an issue with a title and clear description.
For feature requests, please include sample queries and expected results.
