<template>
  <div class="min-h-screen bg-[#0E1B2B] text-white flex flex-col items-center">
    <!-- Navbar -->
    <header class="w-full flex justify-between items-center px-6 py-4 border-b border-gray-600">
      <div class="flex items-center space-x-2">
        <!-- GitHub Link -->
        <a
          href="https://github.com/your-repo-url" 
          target="_blank"
          rel="noopener noreferrer"
          class="font-semibold text-lg text-blue-400 hover:underline"
        >
          GitHub
        </a>
      </div>
      <button class="flex items-center space-x-2 font-semibold">
        Logout
      </button>
    </header>

    <main class="flex flex-col items-center mt-12 px-4 w-full">
      <!-- Title -->
      <h1 class="text-4xl font-bold mb-8 flex items-center space-x-2">
        <span>Spotify AI</span>
        <img
          src="https://upload.wikimedia.org/wikipedia/commons/1/19/Spotify_logo_without_text.svg"
          alt="Spotify"
          class="w-8 h-8"
        />
      </h1>

      <!-- Select and Button -->
      <div class="flex items-center space-x-4 mb-6">
        <select
          class="px-4 py-2 border rounded-md text-black focus:outline-none focus:ring-2 focus:ring-blue-500"
          v-model="genre"
        >
          <option value="">Select Genre</option>
          <option value="Pop">Pop</option>
          <option value="Jazz">Jazz</option>
          <option value="Rock">Rock</option>
          <option value="Afrobeats">Afrobeats</option>
          <option value="Amapiano">Amapiano</option>
          <option value="Raggae">Raggae</option>
          <option value="Hip-hop">Hip-hop</option>
        </select>
        <button
          class="px-6 py-2 bg-blue-600 text-white font-semibold rounded-md shadow hover:bg-blue-700"
          @click="generatePlaylist"
          :disabled="loading"
        >
          {{ loading ? "Generating..." : "Generate Playlist" }}
        </button>
      </div>

      <p v-if="error" class="text-red-500 text-sm mb-4">{{ error }}</p>

      <!-- Loading Spinner -->
      <div v-if="loading" class="flex justify-center items-center mt-6">
        <div class="w-12 h-12 border-4 border-t-transparent border-blue-500 rounded-full animate-spin"></div>
      </div>

      <!-- Playlist -->
      <div v-if="playlist.length > 0 && !loading" class="flex justify-center mt-6">
        <ul class="grid grid-cols-1 sm:grid-cols-2 gap-4 text-center">
          <li
            v-for="(song, index) in playlist"
            :key="index"
            class="bg-white text-[#0E1B2B] px-4 py-2 rounded-md shadow-md"
          >
            <strong>{{ song.title }}</strong> by {{ song.artist }}
          </li>
        </ul>
      </div>
    </main>
  </div>
</template>

<script>
import axios from 'axios';
import { ref } from 'vue';

export default {
  name: 'App',
  setup() {
    const genre = ref('');
    const playlist = ref([]);
    const loading = ref(false);
    const error = ref('');

    const generatePlaylist = async () => {
      if (!genre.value) {
        error.value = 'Please select a genre!';
        return;
      }

      loading.value = true;
      error.value = '';
      playlist.value = []; // Clear playlist during loading
      try {
        const response = await axios.get(
          //`https://backend-ne7e.onrender.com/api/playlist/${genre.value}`
          `http://localhost:5000/api/playlist/${genre.value}`
        );
        playlist.value = response.data.playlist;
      } catch (err) {
        error.value = 'Failed to fetch playlist. Please try again.';
      } finally {
        loading.value = false;
      }
    };

    return {
      genre,
      playlist,
      loading,
      error,
      generatePlaylist,
    };
  },
};
</script>