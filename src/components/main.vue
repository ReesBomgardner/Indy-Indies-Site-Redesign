<template>
  <div>
    <!-- Navigation Bar -->
    <nav class="bg-black">
      <div class="max-w-6xl mx-auto px-6 py-4">
        <div class="flex space-x-8">
          <button 
            v-for="tab in tabs" 
            :key="tab.id"
            @click="activeTab = tab.id"
            class="relative pb-2 text-white transition-colors hover:text-gray-300 focus:outline-none"
          >
            {{ tab.label }}
            <span 
              v-if="activeTab === tab.id"
              class="absolute bottom-0 left-0 w-full h-0.5 bg-white"
            ></span>
          </button>
        </div>
      </div>
    </nav>

    <!-- Tabs -->
    <div class="max-w-6xl mx-auto p-6">
      <div v-if="activeTab === 'home'">
        <h1 class="text-4xl font-bold text-center mb-6">Indy Grown Games</h1>
        <p class="text-center text-gray-600 mb-8">
          a collaborative community for game developers-- connecting professionals, creatives, and fostering innovation
        </p>
      </div>

      <div v-if="activeTab === 'events'">
        <h1 class="text-4xl font-bold text-center mb-6">Upcoming Events</h1>
        <p class="text-center text-gray-600">Our Events</p>
      </div>

      <div v-if="activeTab === 'staff'">
        <h1 class="text-4xl font-bold text-center mb-6">Meet the Team</h1>
      </div>

      <div v-if="activeTab === 'resources'">
        <h1 class="text-4xl font-bold text-center mb-6">Connect with more Communities</h1>
        <p class="text-center text-gray-600">Helpful tools and tutorials.</p>
      </div>

      <div v-if="activeTab === 'showcase'">
        <h1 class="text-4xl font-bold text-center mb-6">Games from the Community</h1>
        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
          <div v-for="art in artwork" :key="art.id" class="bg-white rounded-lg shadow-md overflow-hidden">
            <img :src="art.image" :alt="art.name" class="w-full h-48 object-cover">
            <div class="p-4">
              <h2 class="text-lg font-semibold">{{ art.name }}</h2>
              <p class="text-gray-600">{{ art.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import MonaLisa from '@/assets/MonaLisa.jpg';
import StarryNight from '@/assets/StarryNight.jpg';
import GirlWithThePearlEarring from '@/assets/GirlWithThePearlEarring.jpg';
import TheScream from '@/assets/TheScream.jpg';

export default {
  name: "main",
  data() {
    return {
      activeTab: 'home',
      tabs: [
        { id: 'home', label: 'Home' },
        { id: 'events', label: 'Events' },
        { id: 'staff', label: 'Staff' },
        { id: 'resources', label: 'Resources' },
        { id: 'showcase', label: 'Showcase' }
      ],
      artwork: [
        { id: 1, name: "Mona Lisa", image: MonaLisa, description: "A renoun painting by Leonardo Da Vinci from the the Renaissance in the 1500's depicting a portrait of a french wife." },
        { id: 2, name: "Starry Night", image: StarryNight, description: "An oil painting from 1889 by Vincent van Gogh of the view from his an asylum using one of the most famous brushstrokes." },
        { id: 3, name: "Girl with the Pearl Earring", image: GirlWithThePearlEarring, description: "A tronie painting done by Johannes Vermeer in 1665 renoun for its detail, lighting, and spacing." },
        { id: 4, name: "The Scream", image: TheScream, description: "Painted by Edvard Munch in 1893 dipicting an abstract depiction of panic and fear." },
      ]
    };
  }
};
</script>

<style scoped>
img {
  height: 15em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
</style>