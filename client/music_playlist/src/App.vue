<template>
  <div class="min-h-screen bg-[#0E1B2B] text-white flex flex-col items-center relative">
    <!-- Navbar with GitHub link -->
    <header class="w-full flex justify-between items-center px-6 py-4 border-b border-gray-600">
      <div class="flex items-center space-x-2">
        <a
          href="https://github.com/samorobo/gridiron-test"
          target="_blank"
          rel="noopener noreferrer"
          class="font-semibold text-lg text-blue-400 hover:underline"
        >
          GitHub
        </a>
      </div>
    </header>

    <!-- Main Content -->
    <main class="flex flex-col items-center mt-12 px-4 w-full">
      <!-- Title -->
      <h1 class="text-4xl font-bold mb-4 flex items-center space-x-2">
        <span>Spotify AI</span>
        <img
          src="https://upload.wikimedia.org/wikipedia/commons/1/19/Spotify_logo_without_text.svg"
          alt="Spotify"
          class="w-8 h-8"
        />
      </h1>

      <!-- Label above row -->
      <p class="font-medium mb-2">Pick a genre</p>
      <!-- Genre Dropdown and Generate Button on the same line -->
      <div class="mb-8 flex items-end space-x-4">
        <select
          v-model="genre"
          class="bg-gray-700 text-white py-3 px-4 rounded border border-gray-600 focus:outline-none focus:ring-2 focus:ring-gray-600"
        >
          <option value="" disabled>Select Genre</option>
          <option value="Pop">Pop</option>
          <option value="Rock">Rock</option>
          <option value="Jazz">Jazz</option>
          <option value="Country">Country</option>
          <option value="Blues">Blues</option>
          <option value="Afrobeats">Afrobeats</option>
          <option value="Hip-hop">Hip-hop</option>
          <option value="Highlife">Highlife</option>
          <option value="Opera">Opera</option>
          <option value="Rnb">R&amp;B</option>
        </select>

        <button
          @click="generatePlaylist"
          class="bg-gray-700 hover:bg-gray-600 text-white py-3 px-4 rounded border border-gray-600 focus:outline-none focus:ring-2 focus:ring-gray-600 transition flex items-center justify-center whitespace-nowrap"
          :disabled="loading"
        >
          <span v-if="loading" class="mr-2">
            <span class="inline-block h-4 w-4 border-2 border-t-white border-l-white border-b-transparent border-r-transparent rounded-full animate-spin"></span>
          </span>
          {{ loading ? "Generating..." : "Generate Playlist" }}
        </button>
      </div>

      <p v-if="error" class="text-red-500 text-sm mb-4">{{ error }}</p>

      <!-- Converted Image Section -->
      <!-- Hidden on mobile and tablet; visible on large screens only -->
      <div class="mb-12 w-full hidden lg:flex justify-start md:mb-16 lg:w-3/3">
        <div class="relative left-12 top-12 z-10 -ml-12 overflow-hidden rounded-lg bg-gray-100 shadow-lg md:left-16 md:top-16 lg:ml-0">
          <img 
            :src="manListen"
            alt="Man Listening"
            class="h-full w-full object-cover object-center"
            width="500"
            height="500"
          />
        </div>
        <div class="overflow-hidden rounded-lg bg-gray-100 shadow-lg">
          <img
            :src="womanListen"
            alt="Woman Listening"
            class="h-full w-full object-cover object-center"
            width="500"
            height="500"
          />
        </div>
      </div>
    </main>

    <!-- Playlist Modal: Only visible when a playlist exists -->
    <div v-if="playlist.length > 0" class="fixed inset-0 bg-black bg-opacity-75 flex items-center justify-center z-40">
      <div class="bg-white rounded-lg shadow-xl max-w-md w-full h-[600px] max-h-[80vh] relative flex flex-col">
        
        <!-- Back Button in Top Right Corner -->
        <button
          @click="showConfirmModal = true"
          class="absolute top-2 right-2 flex items-center space-x-1 text-gray-700 hover:text-gray-900"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 transform rotate-180" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M10.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L12.586 11H5a1 1 0 110-2h7.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd" />
          </svg>
          <span>Back</span>
        </button>

        <!-- Modal Content with Scrollable Playlist -->
        <div class="p-6 pt-12 flex flex-col flex-grow overflow-y-auto">
          <h2 class="text-2xl font-semibold text-gray-800 text-center mb-4">Generated Playlist for {{ genre }}</h2>

          <div class="space-y-4 flex flex-col items-start">
            <div v-for="(song, index) in playlist" :key="index" class="flex items-start w-full">
              <div class="text-xl font-bold text-gray-800 mr-4">{{ index + 1 }}.</div>
              <div class="flex flex-col">
                <h3 class="text-lg font-semibold text-gray-800">{{ song.title }}</h3>
                <p class="text-gray-500">{{ song.artist }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Confirmation Modal (Appears on Back Button Click) -->
    <div v-if="showConfirmModal" class="fixed inset-0 z-50 flex items-center justify-center">
      <div class="absolute inset-0 bg-black bg-opacity-50" @click="showConfirmModal = false"></div>
      <div class="relative bg-white rounded-lg p-6 max-w-sm mx-auto">
        <h3 class="text-lg font-medium text-gray-900 mb-4">
          Are you sure you want to exit? You will lose your playlist suggestions if you don't take a screenshot.
        </h3>
        <div class="flex justify-end space-x-4 mt-6">
          <button
            @click="showConfirmModal = false"
            class="px-4 py-2 bg-gray-200 text-gray-800 rounded hover:bg-gray-300 transition"
          >
            Continue
          </button>
          <button
            @click="resetPlaylist"
            class="px-4 py-2 bg-red-500 text-white rounded hover:bg-red-600 transition"
          >
            Yes
          </button>
        </div>
      </div>
    </div>

    <!-- Loading Spinner in Main View (only if not showing the playlist modal) -->
    <div v-if="loading && playlist.length === 0" class="fixed inset-0 flex items-center justify-center z-30">
      <div class="w-12 h-12 border-4 border-t-transparent border-blue-500 rounded-full animate-spin"></div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import { ref } from 'vue';
import manListen from '@/assets/images/man-listen.jpg';
import womanListen from '@/assets/images/woman-listen.jpg';

export default {
  name: 'App',
  setup() {
    const genre = ref('');
    const playlist = ref([]);
    const loading = ref(false);
    const error = ref('');
    const showConfirmModal = ref(false);

    const generatePlaylist = async () => {
      if (!genre.value) {
        error.value = 'Please select a genre!';
        return;
      }

      loading.value = true;
      error.value = '';
      playlist.value = []; // Clear previous playlist during loading

      try {
        const response = await axios.get(
          `http://localhost:5000/api/playlist/${genre.value}`
        );
        playlist.value = response.data.playlist;
      } catch (err) {
        error.value = 'Failed to fetch playlist. Please try again.';
      } finally {
        loading.value = false;
      }
    };

    const resetPlaylist = () => {
      showConfirmModal.value = false;
      loading.value = false;
      playlist.value = [];
      genre.value = '';
    };

    return {
      genre,
      playlist,
      loading,
      error,
      generatePlaylist,
      showConfirmModal,
      resetPlaylist,
      manListen,
      womanListen,
    };
  },
};
</script>
