<template>
  <div class="page">
    <!-- Navigation Bar -->
    <nav class="navbar">
      <div class="nav-inner">
        <button
          v-for="tab in tabs"
          :key="tab.id"
          @click="activeTab = tab.id"
          :class="['nav-button', { active: activeTab === tab.id }]"
        >
          {{ tab.label }}
        </button>
      </div>
    </nav>

    <!-- Main Content -->
    <div class="content">
      <!-- Home Tab -->
      <div v-if="activeTab === 'home'" class="home-grid">
        <div class="left-column">
          <h1 class="title">Indy Grown<br />Games</h1>
          <p class="subtitle">
            A collaborative community for game developers—<br />
            connecting professionals, creatives, and fostering innovation.
          </p>
          <div class="cta">
            <button class="join-btn">JOIN THE COMMUNITY</button>
            <img src="@/assets/discord.png" alt="discord" class="icon" />
          </div>

          <div class="events-section">
            <h2 class="section-heading">Upcoming Events</h2>
            <div class="event-cards">
              <div v-for="event in events" :key="event.title" class="event-card">
                <a href="#" class="event-title">{{ event.title }}</a>
                <p class="event-details">{{ event.details }}</p>
              </div>
            </div>
          </div>
        </div>

        <div class="right-column">
          <img :src="HeartlandLogo" alt="Heartland Game Makers logo" class="logo-img" />
          <img :src="TeamMeeting" alt="Team" class="team-img" />
          <p class="contact-text">
            Questions? Reach out!<br />
            <a href="https://x.com/meanderingleaf">x.com/meanderingleaf</a> |
            <a href="mailto:travis.faas@gmail.com">travis.faas@gmail.com</a>
          </p>
        </div>
      </div>

      <!-- Events Tab -->
      <div v-if="activeTab === 'events'" class="generic-tab">
        <h1 class="tab-title">Upcoming Events</h1>
        <p class="tab-description">Our Events</p>
      </div>

      <!-- Staff Tab -->
      <div v-if="activeTab === 'staff'" class="generic-tab">
        <h1 class="tab-title">Meet the Team</h1>
      </div>

      <!-- Resources Tab -->
      <div v-if="activeTab === 'resources'" class="generic-tab">
        <h1 class="tab-title">Connect with more Communities</h1>
        <p class="tab-description">Helpful tools and tutorials.</p>
      </div>

      <!-- Showcase Tab -->
      <div v-if="activeTab === 'showcase'" class="showcase">
        <h1 class="tab-title">Games from the Community</h1>
        <div class="art-grid">
          <div v-for="art in artwork" :key="art.id" class="art-card">
            <img :src="art.image" :alt="art.name" class="art-image">
            <div class="art-details">
              <h2 class="art-name">{{ art.name }}</h2>
              <p class="art-description">{{ art.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TeamMeeting from '@/assets/team_meeting.jpg';
import HeartlandLogo from '@/assets/heartland_logo.png';
import MonaLisa from '@/assets/MonaLisa.jpg';
import StarryNight from '@/assets/StarryNight.jpg';
import GirlWithThePearlEarring from '@/assets/GirlWithThePearlEarring.jpg';
import TheScream from '@/assets/TheScream.jpg';

export default {
  name: "Main",
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
      events: [
        {
          title: "BIG night",
          details: `4/10/2025\n6:30 PM EDT\nFranklin Hall IU, Bloomington, IN 47405\nIU Media School Game Lab, Room 035`
        },
        {
          title: "Game Developer Social Hours",
          details: `4/11/2025\n6:30 - 8:30 PM EDT\nGuggman Haus Brewing Co.\n1701 Gent St., Indianapolis, IN`
        },
        {
          title: "Game Developer Social Hours",
          details: `4/11/2025\n6:30 - 8:30 PM EDT\nGuggman Haus Brewing Co.\n1701 Gent St., Indianapolis, IN`
        }
      ],
      artwork: [
        { id: 1, name: "Mona Lisa", image: MonaLisa, description: "A renowned painting by Leonardo Da Vinci from the Renaissance in the 1500s depicting a portrait of a French woman." },
        { id: 2, name: "Starry Night", image: StarryNight, description: "An oil painting from 1889 by Vincent van Gogh, showing the view from his asylum using expressive brushwork." },
        { id: 3, name: "Girl with the Pearl Earring", image: GirlWithThePearlEarring, description: "A tronie painting by Johannes Vermeer in 1665, renowned for its lighting and composition." },
        { id: 4, name: "The Scream", image: TheScream, description: "Painted by Edvard Munch in 1893, depicting an abstract expression of panic and fear." }
      ],
      HeartlandLogo,
      TeamMeeting
    };
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=VT323&display=swap');

.page {
  background-color: black;
  color: white;
  font-family: sans-serif;
  min-height: 100vh;
  max-width: 1300px;
  margin: 2rem auto;
  border-radius: 24px;
  overflow: hidden;
  box-shadow: 0 0 20px rgba(255, 255, 255, 0.05);
}
.navbar {
  background-color: black;
  padding: 1rem 2rem;
}
.nav-inner {
  display: flex;
  gap: 2rem;
}
.nav-button {
  background: none;
  border: none;
  color: white;
  font-size: 1.1rem;
  padding-bottom: 0.25rem;
  cursor: pointer;
  position: relative;
}
.nav-button.active::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  height: 2px;
  width: 100%;
  background: white;
}
.content {
  max-width: 1200px;
  margin: 2rem auto;
  padding: 1rem 2rem;
  background-color: black;
  border-radius: 20px; 
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.05); /* optional soft glow */
}
.home-grid {
  display: flex;
  gap: 2rem; /* ⬅️ tighter horizontal space */
}
.left-column {
  flex: 1;
  padding-top: 1rem;
}
.events-section {
  background-color: #222;
  border-radius: 20px;
  padding: 1.5rem;
  margin-top: 2rem;
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.1);
}
.section-heading {
  font-size: 1.3rem;
  font-weight: bold;
  margin-bottom: 1rem;
}
.right-column {
  width: 360px;
  text-align: center;
}
.title {
  font-family: 'VT323', monospace;
  font-size: 4rem;
  line-height: 4.2rem;
  margin-bottom: 1rem;
  text-align: left;
}
.subtitle {
  color: #ccc;
  margin: 1rem 0;
  text-align: left;
  font-size: 1.1rem;
}
.cta {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin: 1.5rem 0;
}
.join-btn {
  background-color: #d946ef;
  color: white;
  padding: 0.6rem 1.5rem;
  border: none;
  border-radius: 9999px;
  font-weight: bold;
  font-size: 1rem;
  cursor: pointer;
}
.icon {
  width: 28px;
  height: 28px;
  object-fit: contain;
}
.section-heading {
  margin-top: 0.5rem; /* ⬅️ was 1.5rem */
  margin-bottom: 1rem;
  font-size: 1.3rem;
  font-weight: bold;
  text-align: center;
}
.event-cards {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  justify-content: center; /* ✅ centers them */
}
.event-card {
  background-color: #aaa;
  color: white;
  padding: 1rem;
  border-radius: 0.5rem;
  width: 250px;
  font-size: 0.9rem;
}
.event-title {
  color: white;
  text-decoration: underline;
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}
.team-img {
  width: 100%;
  border-radius: 0.5rem;
  margin-bottom: 1rem;
}
.logo-img {
  width: 180px;
  margin-bottom: 2rem;
}
.contact-text {
  font-size: 0.95rem;
  color: #ccc;
}
.contact-text a {
  color: white;
  text-decoration: underline;
}
</style>
