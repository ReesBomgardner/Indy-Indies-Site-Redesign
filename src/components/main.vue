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
            <h2 class="section-heading">
              <span class="heading-label">Upcoming Events</span>
            </h2>
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
      <div v-if="activeTab === 'events'" class="events-tab">
        <div class="events-header">
          <img :src="HeartlandLogo" alt="Heartland Logo" class="events-logo" />
        </div>

        <div class="section-box violet-glow">
          <h2 class="section-heading">
            <span class="heading-label">Our Main Events</span>
          </h2>
          <div class="highlight-wrapper">
            <div class="highlight-card gradient-border">
              <img src="@/assets/indy_indies.png" alt="Indy Indies" class="highlight-img">
              <div class="highlight-content">
                <h3 class="highlight-title">INDY INDIES</h3>
                <p class="highlight-desc">Twice-yearly showcase of regional games</p>
                <a href="#" class="highlight-link">Learn more</a>
              </div>
            </div>
            <div class="highlight-card gradient-border">
              <img src="@/assets/hands.png" alt="Board Game" class="highlight-img">
              <div class="highlight-content">
                <h3 class="highlight-title">LOREM IPSUM</h3>
                <p class="highlight-desc">Lorem ipsum dolor sit amet, consectetur adipiscing elit...</p>
                <a href="#" class="highlight-link">Learn more</a>
              </div>
            </div>
          </div>
        </div>

        <div class="section-box violet-glow">
          <h2 class="section-heading">
            <span class="heading-label">Upcoming Events</span>
          </h2>
          <div class="scroll-row">
            <div v-for="event in events" :key="event.title" class="event-scroll-card">
              <a href="#" class="event-title">{{ event.title }}</a>
              <p class="event-details">{{ event.details }}</p>
            </div>
            <div v-for="n in 3" :key="'placeholder-' + n" class="event-scroll-card">
              <a href="#" class="event-title">Lorem Ipsum</a>
              <p class="event-details">date<br>time<br>address line 1<br>address line 2</p>
            </div>
          </div>
        </div>
      </div>


      <!-- Staff Tab -->
      <div v-if="activeTab === 'staff'" class="staff-tab">
        <div class="staff-layout">
          <div class="staff-left">
            <h1 class="staff-heading">Meet the Team</h1>
            <div class="slideshow">
              <button class="nav-arrow left" @click="prevSlide">&#10094;</button>
              <img :src="slideshowImages[currentSlide]" alt="Staff Slideshow" class="slideshow-img" />
              <button class="nav-arrow right" @click="nextSlide">&#10095;</button>
            </div>
          </div>
          <div class="staff-right">
            <div class="staff-grid">
              <div class="staff-card" v-for="n in 6" :key="'staff-' + n">
                <img src="@/assets/Avatar.png" alt="Staff Avatar" class="staff-avatar" />
                <div class="staff-name">F Name L Name</div>
                <div class="staff-role">Position</div>
                <div class="staff-contact">@socialmedia<br />email@email.com</div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Resources Tab -->
      <div v-if="activeTab === 'resources'" class="resources-tab violet-glow">
        <h1 class="tab-title vt323">Connect With<br />More Communities</h1>
        <div class="resource-grid">
          <div class="resource-card gradient-border" v-for="resource in resources" :key="resource.title">
            <img :src="resource.image" :alt="resource.title" class="resource-img" />
            <div class="resource-content">
              <h3 class="resource-title">{{ resource.title }}</h3>
              <p class="resource-desc">{{ resource.description }}</p>
              <a href="#" class="resource-link">Learn more</a>
            </div>
          </div>
        </div>
      </div>

      <!-- Showcase Tab -->
      <div v-if="activeTab === 'showcase'" class="showcase violet-glow">
        <h1 class="tab-title vt323">Games from the Community</h1>
        <div class="game-grid">
          <div v-for="game in showcaseGames" :key="game.title" class="game-card gradient-border">
            <img :src="game.image" :alt="game.title" class="game-img" />
            <div class="game-content">
              <h3 class="game-title">{{ game.title }}</h3>
              <p class="game-creator">{{ game.creator }}</p>
              <p class="game-desc">{{ game.description }}</p>
              <div class="game-actions">
                <a href="#" class="game-link">Showcase</a>
                <button class="play-btn">Play</button>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Contact Tab -->
      <div v-if="activeTab === 'contact'" class="contact-tab violet-glow">
        <h1 class="tab-title vt323">Contact Us!</h1>
        <div class="contact-grid">
          <div class="contact-card gradient-border" v-for="member in contactStaff" :key="member.role">
            <h3 class="contact-role">{{ member.role }}</h3>
            <div class="contact-entry">
              <span class="contact-icon">❌</span> {{ member.username1 }}
            </div>
            <div class="contact-entry">
              <img src="@/assets/discord.png" alt="discord" class="icon" /> {{ member.username2 }}
            </div>
            <div class="contact-entry">
              <span class="contact-icon">✉️</span> {{ member.email }}
            </div>
          </div>
        </div>
        <div class="cta" style="justify-content: center;">
          <button class="join-btn">JOIN THE COMMUNITY</button>
          <img src="@/assets/discord.png" alt="discord" class="icon" />
        </div>
        <p class="contact-description">
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua...<br />
          (Reach out to staff to get involved!).
        </p>
      </div>

    </div>
  </div>
</template>




<script>
import HeartlandLogo from '@/assets/heartland_logo.png';
import TeamMeeting from '@/assets/team_meeting.jpg';
import MonaLisa from '@/assets/MonaLisa.jpg';
import StarryNight from '@/assets/StarryNight.jpg';
import GirlWithThePearlEarring from '@/assets/GirlWithThePearlEarring.jpg';
import TheScream from '@/assets/TheScream.jpg';

import Slide1 from '@/assets/staff1.png';
import Slide2 from '@/assets/staff2.png';
import Slide3 from '@/assets/staff3.png';

import UnrealLogo from '@/assets/unreal.png';
import DevsLogo from '@/assets/devs.png';
import TabletopLogo from '@/assets/tabletop.png';

import Showcase1 from '@/assets/showcase1.png';
import Showcase2 from '@/assets/showcase2.png';

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
        { id: 'showcase', label: 'Showcase' },
        { id: 'contact', label: 'Contact' }
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
        { id: 1, name: "Mona Lisa", image: MonaLisa, description: "A renowned painting by Leonardo Da Vinci..." },
        { id: 2, name: "Starry Night", image: StarryNight, description: "An oil painting from 1889 by Vincent van Gogh..." },
        { id: 3, name: "Girl with the Pearl Earring", image: GirlWithThePearlEarring, description: "A tronie painting by Johannes Vermeer..." },
        { id: 4, name: "The Scream", image: TheScream, description: "Painted by Edvard Munch in 1893..." }
      ],
      HeartlandLogo,
      TeamMeeting,
      currentSlide: 0,
      slideshowImages: [Slide1, Slide2, Slide3],
      resources: [
        {
          title: "UNREAL INDY",
          description: "Unreal Engine Enthusiasts who meet monthly to share work and collaborate",
          image: UnrealLogo
        },
        {
          title: "INDIANAPOLIS GAME DEVELOPERS",
          description: "Monthly meet-up of Indianapolis area game developers",
          image: DevsLogo
        },
        {
          title: "INDY TABLETOP GAME CREATORS",
          description: "Monthly playtesting meeting of tabletop game creators.",
          image: TabletopLogo
        }
      ],
      showcaseGames: [
        {
          title: "GAME TITLE",
          creator: "Creator Name",
          description: "Lorem ipsum dolor sit amet, consectetur adipiscing elit...",
          image: Showcase1
        },
        {
          title: "GAME TITLE",
          creator: "Creator Name",
          description: "Lorem ipsum dolor sit amet, consectetur adipiscing elit...",
          image: Showcase2
        }
      ],
      contactStaff: [
        { role: 'president', username1: 'username', username2: 'username', email: 'email@email.com' },
        { role: 'vice president', username1: 'username', username2: 'username', email: 'email@email.com' },
        { role: 'secretary', username1: 'username', username2: 'username', email: 'email@email.com' }
      ]
    };
  },
  methods: {
    nextSlide() {
      this.currentSlide = (this.currentSlide + 1) % this.slideshowImages.length;
    },
    prevSlide() {
      this.currentSlide = (this.currentSlide - 1 + this.slideshowImages.length) % this.slideshowImages.length;
    }
  }
};
</script>


<style scoped>
@import url('https://fonts.googleapis.com/css2?family=VT323&display=swap');

.page {
  background-color: #0b0b0b;
  background-image: url('@/assets/37bc7daf-7599-4e43-bf2f-d8ed7ed6f43a.png');
  background-repeat: repeat;
  background-size: 300px;
  background-blend-mode: multiply;
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
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.05);
}
.home-grid {
  display: flex;
  gap: 2rem;
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
  margin-top: 0.5rem;
  margin-bottom: 1rem;
  font-size: 1.3rem;
  font-weight: bold;
  text-align: left;
}
.heading-label {
  display: inline-block;
  padding-bottom: 0.2rem;
  border-bottom: 2px solid #888;
  background: rgba(255, 255, 255, 0.03);
  color: white;
  font-weight: 500;
  font-size: 1.2rem;
  border-radius: 4px;
  padding: 0.2rem 0.5rem;
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
.event-cards {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  justify-content: center;
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
  font-weight: bold;
  text-decoration: underline;
  margin-bottom: 0.5rem;
  display: block;
  text-align: left;
  color: white;
}
.event-details {
  text-align: left;
  white-space: pre-line;
  color: black;
}
.team-img {
  width: 100%;
  border-radius: 0.5rem;
  margin-bottom: 1rem;
}
.logo-img, .events-logo {
  width: 180px;
  margin-bottom: 2rem;
}
.events-header {
  display: flex;
  justify-content: flex-end;
  padding-bottom: 1rem;
}
.contact-text {
  font-size: 0.95rem;
  color: #ccc;
}
.contact-text a {
  color: white;
  text-decoration: underline;
}
.scroll-row {
  display: flex;
  gap: 1rem;
  overflow-x: auto;
  padding-bottom: 1rem;
}
.event-scroll-card {
  min-width: 200px;
  background-color: #999;
  padding: 1rem;
  border-radius: 0.5rem;
  flex-shrink: 0;
  text-align: left;
  white-space: pre-line;
  color: white;
}
.highlight-wrapper {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}
.highlight-card {
  display: flex;
  background-color: black;
  border: 1px solid white;
  border-radius: 10px;
  overflow: hidden;
  width: 100%;
  max-width: 500px;
}
.highlight-img {
  width: 150px;
  height: auto;
  object-fit: cover;
}
.highlight-content {
  padding: 1rem;
  color: white;
  text-align: left;
}
.highlight-title {
  font-family: 'VT323', monospace;
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
}
.highlight-desc {
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
}
.highlight-link {
  text-decoration: underline;
  color: white;
}
.section-box {
  background-color: #1a1a1a;
  border: 1px solid #444;
  border-radius: 16px;
  padding: 2rem;
  margin-bottom: 2rem;
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.05);
}

/* NEW STAFF STYLES */
.staff-tab {
  padding: 2rem 1rem 1rem; /* moved heading up */
}
.staff-layout {
  display: flex;
  flex-direction: row;
  gap: 2rem;
  align-items: flex-start;
}
.staff-left {
  flex: 1;
  position: relative;
}
.staff-heading {
  font-family: 'VT323', monospace;
  font-size: 2.5rem;
  margin-bottom: 1rem; /* was 1.5rem */
  letter-spacing: 1px;
  text-align: left;
}
.slideshow {
  position: relative;
  max-width: 360px; /* slightly smaller */
  margin: auto;
}
.slideshow-img {
  width: 100%;
  border-radius: 1rem;
  box-shadow: 0 0 8px rgba(255, 255, 255, 0.1);
}
.nav-arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-size: 2rem;
  color: white;
  background-color: rgba(0, 0, 0, 0.5);
  border: none;
  padding: 0.5rem;
  cursor: pointer;
  z-index: 2;
}
.nav-arrow.left {
  left: -2.5rem; /* moved fully outside */
}
.nav-arrow.right {
  right: -2.5rem; /* moved fully outside */
}
.nav-arrow:hover {
  background-color: rgba(255, 255, 255, 0.2);
}
.staff-right {
  flex: 1;
}
.staff-heading {
  font-family: 'VT323', monospace;
  font-size: 2.5rem;
  margin-bottom: 1.5rem;
  letter-spacing: 1px;
  text-align: left;
}
.slideshow-placeholder {
  width: 100%;
  max-width: 400px;
  border-radius: 1rem;
  box-shadow: 0 0 8px rgba(255, 255, 255, 0.1);
}
.staff-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  justify-items: center;
}
.staff-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1rem 0.5rem;
  border-radius: 12px;
}
.staff-avatar {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  margin-bottom: 0.8rem;
  object-fit: cover;
}
.staff-name {
  font-weight: bold;
  font-size: 1rem;
  margin-bottom: 0.25rem;
}
.staff-role {
  font-size: 0.85rem;
  color: #bbb;
  margin-bottom: 0.25rem;
}
.staff-contact {
  font-size: 0.75rem;
  color: #888;
  white-space: pre-line;
  text-align: center;
}
.resources-tab {
  padding: 2rem 0;
  text-align: center;
}
.resource-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  justify-content: center;
  margin-top: 2rem;
}
.resource-card {
  background-color: #111;
  border: 1px solid #444;
  border-radius: 12px;
  width: 320px;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  text-align: left;
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.05);
}
.resource-img {
  width: 100%;
  height: 160px;
  object-fit: cover;
}
.resource-content {
  padding: 1rem;
}
.resource-title {
  font-weight: bold;
  font-size: 1.1rem;
  margin-bottom: 0.5rem;
}
.resource-desc {
  font-size: 0.95rem;
  color: #ccc;
  margin-bottom: 1rem;
}
.resource-link {
  color: #d946ef;
  font-weight: bold;
  text-decoration: underline;
  font-size: 0.95rem;
}
.showcase {
  padding: 2rem 0;
  text-align: center;
}
.game-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  justify-content: center;
  margin-top: 2rem;
}
.game-card {
  background-color: #111;
  border: 1px solid #444;
  border-radius: 12px;
  width: 400px;
  overflow: hidden;
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.05);
  text-align: left;
}
.game-img {
  width: 100%;
  height: 200px;
  object-fit: cover;
}
.game-content {
  padding: 1rem;
}
.game-title {
  font-weight: bold;
  font-size: 1.1rem;
  margin-bottom: 0.2rem;
}
.game-creator {
  font-size: 0.95rem;
  color: #bbb;
  margin-bottom: 0.5rem;
}
.game-desc {
  font-size: 0.9rem;
  color: #ccc;
  margin-bottom: 1rem;
}
.game-actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.game-link {
  color: #d946ef;
  text-decoration: underline;
  font-size: 0.95rem;
}
.play-btn {
  background-color: #d946ef;
  color: white;
  border: none;
  padding: 0.4rem 1rem;
  border-radius: 9999px;
  cursor: pointer;
  font-weight: bold;
  font-size: 0.9rem;
}
.contact-tab {
  padding: 2rem 0;
  text-align: center;
}
.contact-grid {
  display: flex;
  gap: 2rem;
  justify-content: center;
  margin-bottom: 2rem;
}
.contact-card {
  background-color: #111;
  border: 1px solid #444;
  border-radius: 12px;
  padding: 1.5rem;
  width: 250px;
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.05);
}
.contact-role {
  font-weight: bold;
  font-size: 1.2rem;
  margin-bottom: 1rem;
  text-transform: capitalize;
}
.contact-entry {
  margin-bottom: 0.5rem;
  font-size: 0.95rem;
  color: #ccc;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}
.contact-icon {
  font-size: 1.1rem;
}
.contact-description {
  font-size: 0.9rem;
  color: #ccc;
  max-width: 800px;
  margin: 0 auto;
  line-height: 1.5;
  text-align: center;
  padding: 1rem;
}
.tab-title.vt323 {
  font-family: 'VT323', monospace;
  font-size: 2.5rem;
  margin-bottom: 1rem;
  letter-spacing: 1px;
  text-align: center;
}

.page {
  background-color: #0b0b0b;
  background-image: url('@/assets/37bc7daf-7599-4e43-bf2f-d8ed7ed6f43a.png');
  background-repeat: repeat;
  background-size: 300px;
  background-blend-mode: multiply;
  color: white;
  font-family: sans-serif;
  min-height: 100vh;
  max-width: 1300px;
  margin: 2rem auto;
  border-radius: 24px;
  overflow: hidden;
  box-shadow: 0 0 20px rgba(255, 255, 255, 0.05);
}

.violet-glow {
  box-shadow: 0 0 15px rgba(217, 70, 239, 0.3);
  border: 1px solid rgba(217, 70, 239, 0.4);
}

.gradient-border {
  border-image: linear-gradient(to right, #d946ef, #9333ea);
  border-image-slice: 1;
  border-width: 2px;
  border-style: solid;
}
</style>
