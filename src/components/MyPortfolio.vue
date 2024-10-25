<template>
  <v-app>
    <v-app-bar elevation="2" class="fixed-nav">
      <v-toolbar-title><b>My Portfolio</b></v-toolbar-title>
      <v-spacer></v-spacer>
      <div class="nav-links hidden-sm-and-down">
        <a 
          v-for="item in menuItems" 
          :key="item.href" 
          :href="item.href" 
          :class="{ 'active': selectedCategory === item.href.substring(1) }"
          @click.prevent="filterCategory(item.href.substring(1))"
        >
          <v-icon>{{ item.icon }}</v-icon>
          {{ item.text }}
        </a>
      </div>
       <!-- Mobile Menu Button -->
      <v-app-bar-nav-icon
        class="hidden-md-and-up"
        @click="drawer = !drawer">
      </v-app-bar-nav-icon>
    </v-app-bar>

    <!-- Mobile Navigation Drawer -->
    <v-navigation-drawer
      v-model="drawer"
      temporary
      right
      class="hidden-md-and-up"
      >

    <v-list>
      <v-list-item
        v-for="item in menuItems"
        :key="item.href"
        :href="item.href"
        @click="mobileNavClick(item.href.substring(1))"
      >
      <v-list-item-icon>
        <v-icon>{{ item.icon }}</v-icon>
      </v-list-item-icon>
      <v-list-item-content>
        <v-list-item-title>{{ item.text }}</v-list-item-title>
      </v-list-item-content>
    </v-list-item>
  </v-list>
</v-navigation-drawer>

    <div class="nav-spacer"></div>

    <v-container fluid>
      <!-- Hero Section -->
      <section id="hero" class="hero section-margin">
        <v-row>
          <v-col class="text-center">
            <h2>Hi, I'm Omaimah!</h2>
            <p>I am an aspiring graphic designer/web developer from Caraga State University.</p>
            <v-btn class="get-in-touch" @click="scrollTo('#contact')">Get in Touch</v-btn>
          </v-col>
        </v-row>
      </section>

      <!-- About Section -->
      <section id="about" class="section-margin about-section">
        <h2>About Me</h2>
        <v-row>
          <v-col cols="12" md="3">
            <v-img src="../assets/mamai.jpg" alt="Omaimah" class="wide-image" style="border-radius: 10px; box-shadow: 0 2px 8px rgba(0,0,0,0.2);" contain></v-img>
          </v-col>
          <v-col cols="12" md="8">
            <h3 style="font-weight: bold; color: #f9f9f9;">UI/UX Designer & Web Developer</h3>
            <v-row>
              <v-col>
                <v-card-text>
                  <ul style="margin: 0; padding: 0; color: #f9f9f9;">
                    <li style="margin-bottom: 10px;"><v-icon left>mdi-cake</v-icon> Birthday: 25 May 2001</li>
                    <li style="margin-bottom: 10px;"><v-icon left>mdi-calendar-today</v-icon> Age: 23</li>
                    <li style="margin-bottom: 10px;"><v-icon left>mdi-phone</v-icon> Phone #: 09563104232</li>
                    <li style="margin-bottom: 10px;"><v-icon left>mdi-map-marker</v-icon> City: Butuan City</li>
                  </ul>
                </v-card-text>
              </v-col>
              <v-col>
                <v-card-text class="elegant-text">
                  <ul style="margin: 0; padding: 0; color: #f9f9f9;">
                    <li style="margin-bottom: 10px;"><v-icon left>mdi-school</v-icon> Degree: Undergrad</li>
                    <li style="margin-bottom: 10px; white-space: nowrap;"><v-icon left>mdi-email</v-icon> Email: <a href="mailto:omaimahameril999@gmail.com" style="color: inherit; text-decoration: none;">omaimahameril999@gmail.com</a></li>
                    <li style="margin-bottom: 10px;"><v-icon left>mdi-briefcase</v-icon> Freelance: Available</li>
                  </ul>
                </v-card-text>
              </v-col>
            </v-row>
            <p class="elegant-text" style="margin-top: 5px;">
              Currently pursuing my studies at Caraga State University, I am eager to combine my design skills and technical knowledge to build innovative web solutions. 
              I thrive on challenges and enjoy transforming ideas into reality through thoughtful design and coding. 
              I’m excited to continue learning and growing in the ever-evolving tech landscape.
            </p>
          </v-col>
        </v-row>
      </section>

      <section id="skills" class="section-margin">
        <h2>Skills</h2>
        <v-row>
          <v-col v-for="skill in skills" :key="skill.name" cols="12" md="6" style="margin-bottom: 20px;">
            <div class="skill-item" :style="{ backgroundColor: skill.color, padding: '10px', borderRadius: '20px' }">
              <v-icon>{{ skill.icon }}</v-icon>
              <span class="skill-name">{{ skill.name }}</span>
              <span class="skill-value">{{ skill.value }}%</span>
            </div>
            <v-progress-linear :value="skill.value" :color="skill.color" style="margin-top: 5px;"></v-progress-linear>
          </v-col>
        </v-row>
      </section>

      <!-- Portfolio Section -->
      <section id="portfolio" class="section-margin">
        <h2>Portfolio</h2>
        <div class="portfolio-filters">
          <v-btn 
            class="filter-button" 
            :class="{ 'active': selectedCategory === 'all' }" 
            @click="filterCategory('all')">
            <v-icon left>mdi-view-grid</v-icon> All
          </v-btn>
          <v-btn 
            class="filter-button" 
            :class="{ 'active': selectedCategory === 'app' }" 
            @click="filterCategory('app')">
            <v-icon left>mdi-application</v-icon> Apps
          </v-btn>
          <v-btn 
            class="filter-button" 
            :class="{ 'active': selectedCategory === 'certificate' }" 
            @click="filterCategory('certificate')">
            <v-icon left>mdi-certificate</v-icon> Certificates
          </v-btn>
        </div>

        <v-row>
          <v-col v-for="item in filteredPortfolioItems" :key="item.title" cols="12" md="4">
            <v-card>
              <v-img :src="item.image" height="200px" contain></v-img>
              <v-card-title>{{ item.title }}</v-card-title>
              <v-card-subtitle>{{ item.description }}</v-card-subtitle>
            </v-card>
          </v-col>
        </v-row>
      </section>

      <!-- Contact Section -->
      <section id="contact" class="section-margin">
        <h2>Contact Us</h2>
        <v-card class="contact-card" elevation="2" style="padding: 20px; background-color: #f9f9f9;">
          <v-form ref="form" v-model="valid" @submit.prevent="sendMessage">
            <v-text-field 
              v-model="contactForm.name" 
              label="Your Name" 
              :rules="[rules.required]" 
              required 
              prepend-icon="mdi-account" 
              placeholder="Enter your full name"></v-text-field>

            <v-text-field 
              v-model="contactForm.email" 
              label="Your Email" 
              :rules="[rules.required, rules.email]" 
              required 
              prepend-icon="mdi-email" 
              placeholder="Enter your email address"></v-text-field>

            <v-text-field 
              v-model="contactForm.phone" 
              label="Your Phone (Optional)" 
              :rules="[rules.phone]" 
              prepend-icon="mdi-phone" 
              placeholder="Enter your phone number"></v-text-field>

            <v-select
              v-model="contactForm.subject"
              :items="['General Inquiry', 'Support', 'Feedback', 'Other']"
              label="Subject"
              required
              prepend-icon="mdi-comment-question-outline"></v-select>

            <v-textarea 
              v-model="contactForm.message" 
              label="Message" 
              :rules="[rules.required]" 
              required 
              placeholder="Type your message here"></v-textarea>

            <v-btn type="submit" class="send-button" :disabled="!valid" color="primary">Send Message</v-btn>

            <v-snackbar v-model="snackbar" :timeout="3000" color="success">
              {{ snackbarMessage }}
              <v-btn text @click="snackbar = false">Close</v-btn>
            </v-snackbar>
          </v-form>
        </v-card>
      </section>

      <!-- Footer Section -->
      <footer class="footer">
        <v-container>
          <v-row justify="center">
            <v-col class="text-center">
              <h4>Connect with me</h4>
              <div class="social-icons">
                <a href="https://www.facebook.com/profile.php?id=61551192152228" target="_blank" rel="noopener noreferrer">
                  <v-icon>mdi-facebook</v-icon>
                </a>
                <a href="https://www.instagram.com/yourprofile" target="_blank" rel="noopener noreferrer">
                  <v-icon>mdi-instagram</v-icon>
                </a>
              </div>
              <h4>&copy; 2024 Omaimah. All rights reserved.</h4>
            </v-col>
          </v-row>
        </v-container>
      </footer>
    </v-container>
  </v-app>
</template>

<script>
export default {
  name: 'MyPortfolio',
  data() {
    return {
      drawer: false,
      menuItems: [
        { href: '#hero', text: 'Home', icon: 'mdi-home' },
        { href: '#about', text: 'About', icon: 'mdi-account' },
        { href: '#skills', text: 'Skills', icon: 'mdi-brain' },
        { href: '#portfolio', text: 'Portfolio', icon: 'mdi-briefcase' },
        { href: '#contact', text: 'Contact', icon: 'mdi-email' },
      ],

      valid: false,
      rules: {
        required: value => !!value || 'This field is required.',
        email: value => /.+@.+\..+/.test(value) || 'Must be a valid email.',
      },
      skills: [
        { name: 'HTML', value: 100, color: '#e34c26', icon: 'mdi-language-html5' },
        { name: 'JavaScript', value: 70, color: '#f0db4f', icon: 'mdi-language-javascript' },
        { name: 'CSS', value: 75, color: '#264de4', icon: 'mdi-language-css3' },
        { name: 'PHP', value: 60, color: '#777bb3', icon: 'mdi-language-php' },
        { name: 'Photoshop', value: 50, color: '#31a8ff', icon: 'mdi-adobe' },
      ],

      portfolioItems: [
        {
          title: 'FinderSphere Login',
          image: require('@/assets/App 1.jpg'),
          category: 'app',
        },
        {
          title: 'FinderSphere Signup',
          image: require('@/assets/App 2.jpg'),
          category: 'app',
        },
        {
          title: 'Certificate 1',
          image: require('@/assets/Certificate 1.jpg'),
          category: 'certificate',
        },
        {
          title: 'Certificate 2',
          image: require('@/assets/Certificate 2.jpg'),
          category: 'certificate',
        },
        {
          title: 'Certificate 3',
          image: require('@/assets/Certificate 3.jpg'),
          category: 'certificate',
        },
        {
          title: 'Certificate 4',
          image: require('@/assets/Certificate 4.jpg'),
          category: 'certificate',
        },
        {
          title: 'Certificate 5',
          image: require('@/assets/Certificate 5.jpg'),
          category: 'certificate',
        },
      ],
      contactForm: {
        name: '',
        email: '',
        message: '',
      },
      selectedCategory: 'hero', // Default active link
      snackbar: false,
      snackbarMessage: '',
    };
  },
  computed: {
    filteredPortfolioItems() {
      if (this.selectedCategory === 'all') {
        return this.portfolioItems;
      }
      return this.portfolioItems.filter(item => item.category === this.selectedCategory);
    },
  },
  methods: {
    mobileNavClick(category) {
    this.drawer = false;
    this.filterCategory(category);
    },

    filterCategory(category) {
      this.selectedCategory = category;
      // Only scroll if the category matches a section ID
      if (['hero', 'about', 'skills', 'portfolio', 'contact'].includes(category)) {
        this.scrollTo(`#${category}`);
      }
    },
    sendMessage() {
      if (this.$refs.form.validate()) {
        console.log("Message Sent:", this.contactForm);
        alert("Thank you for your message! We'll get back to you soon.");
        this.contactForm.name = '';
        this.contactForm.email = '';
        this.contactForm.message = '';
        this.$refs.form.reset();
      }
    },
    scrollTo(href) {
      const element = document.querySelector(href);
      if (element) {
        element.scrollIntoView({ behavior: 'smooth' });
      }
    },
  },
};
</script>

<style scoped>
:root {
  --primary-color: #3498db;
  --secondary-color: #2c3e50;
  --accent-color: #e74c3c;
  --text-color: #ffffff;
  --background-color: #fef9f9;
  --card-background: #ffffff;
  --nav-text-color: #ffffff;
}

body {
  font-family: 'Lora', serif;
  background-color: #0a0909;
  margin: 0;
}

.v-application {
  background-color: #0e0a0a !important;
  color: var(--text-color) !important;
}

.v-app-bar {
  background-color: #f4f8f8 !important;
  z-index: 10;
}

.nav-links {
  display: flex;
  align-items: center;
}

.nav-links a {
  color: white;
  text-decoration: none;
  margin: 0 10px;
  padding: 8px 12px;
  border-radius: 4px;
  transition: background-color 0.3s, color 0.3s;
  font-weight: 500;
  display: flex;
  align-items: center;
}

.nav-links a:hover {
  background-color: rgba(255, 255, 255, 0.1);
  color: white;
}

.nav-links a.active {
  color: rgb(255, 254, 254);
}

.nav-links .v-icon {
  margin-right: 4px;
}

/* Mobile styles */
.v-navigation-drawer {
  background-color: #080606 !important;
}

.v-list {
  background-color: transparent !important;
}

.v-list-item {
  margin: 4px 0;
  color: #fef9f9;
}

.v-list-item:hover {
  background-color: rgba(255, 255, 255, 0.1) !important;
}

h2 {
  font-family: 'Playfair Display', serif;
  font-size: 2em;
  margin-bottom: 20px;
  color: white;
}

.section-margin {
  margin: 40px 0; /* Adjust margins */
}

.skill-item {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
  padding: 10px;
  border-radius: 30px;
  color: rgb(255, 250, 250) !important;
}

.wide-image {
  height: auto; /* Ensure images are responsive */
  width: 100%;
  max-width: 400px; /* Limit max width for large screens */
  object-fit: cover;
}

.portfolio-filters {
  display: flex;
  justify-content: center;
  margin-bottom: 30px;
}

.filter-button {
  margin: 0 10px;
  border-radius: 20px;
  transition: background-color 0.3s, transform 0.2s;
}

.filter-button:hover {
  background-color: #e0e0e0;
  transform: translateY(-2px);
}

.filter-button.active {
  background-color: #90afc4;
  color: white;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.contact-card {
  padding: 20px;
  background-color: white !important;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  max-width: 700px;
  margin: 0 auto;
}

.v-text-field,
.v-textarea {
  margin-bottom: 20px;
}

.hero {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  background-image: url('../assets/mamai1.jpg');
  background-size: cover;
  background-position: center;
  color: rgb(255, 255, 255);
}

/* Footer styles */
.footer {
  background-color: white;
  color: rgb(5, 6, 7);
  padding: 20px 0;
}

.social-icons {
  margin: 10px 0;
}

.social-icons a {
  color: rgb(5, 7, 7);
  margin: 0 10px;
  font-size: 24px;
}

.social-icons a:hover {
  color: rgb(82, 108, 239);
}

.get-in-touch {
  background-color: var(--primary-color);
  margin-top: 8%;
  color: white;
  padding: 10px 20px;
  border-radius: 25px;
  font-weight: bold;
  transition: background-color 0.3s, transform 0.2s, box-shadow 0.2s;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
  border: 1px solid rgba(255, 255, 255, 0.8);
  width: fit-content; /* Ensure the button width adapts */
}

.get-in-touch:hover {
  background-color: #5bb4ef;
  transform: translateY(-2px);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.4);
}

.fixed-nav {
  position: fixed !important;
  top: 0;
  left: 0;
  right: 0;
  background-color: #070606 !important;
  z-index: 1000; 
  color: #fef9f9;
}

.nav-spacer {
  height: 30px;
}

.section-margin {
  padding-top: 20px;
  margin-bottom: 60px;
}

p {
  font-family: 'Georgia', serif;
  font-size: 18px;
  line-height: 1.6;
  color: white;
}

@media (max-width: 960px) {
  .v-toolbar-title {
    font-size: 1.25rem;
  }
}

/* Media Queries for responsiveness */
@media (max-width: 768px) {
  h2 {
    font-size: 1.5em; /* Smaller headings on mobile */
  }

  .nav-links {
    flex-direction: column; /* Stack links vertically */
    align-items: center; /* Center align */
  }

  .hero {
    height: 60vh; /* Adjust hero height on smaller screens */
    padding: 20px; /* Add padding */
  }

  .wide-image {
    max-width: 100%; /* Ensure image is responsive */
  }

  .contact-card {
    padding: 15px; /* Reduce padding */
  }

  .get-in-touch {
    width: 100%; /* Make button full width */
    margin-top: 20px; /* Add margin on top */
  }

  .skill-item {
    flex-direction: column; /* Stack skill items vertically */
    align-items: flex-start; /* Align items to the start */
  }
}
</style>

