<template>
  <div class="page-container">
    <!-- Centered and styled heading -->
    <div class="heading-container">
      <h1 class="heading">Available Jobs</h1>
      <div class="heading-underline"></div>
    </div>

    <!-- Search and Filter -->
    <div class="filter-container">
      <div class="search-bar-container">
        <input 
          type="text" 
          v-model="searchQuery" 
          class="search-bar" 
          placeholder="🔍 Search jobs by title or company..." 
        />
      </div>
      <div class="filter-dropdown-container">
        <select v-model="selectedLocation" class="filter-dropdown">
          <option value="">🌍 All Locations</option>
          <option v-for="location in uniqueLocations" :key="location" :value="location">
            {{ location }}
          </option>
        </select>
      </div>
    </div>

    <!-- Jobs Grid -->
    <div class="grid">
      <div
        v-for="job in filteredJobs"
        :key="job.id"
        class="card shadow rounded"
        @click="viewDetails(job)"
      >
        <div class="card-header">
          <h2 class="job-title">{{ job.title }}</h2>
          <p class="company-name">{{ job.company }}</p>
        </div>
        <div class="card-body">
          <p class="location"><strong>Location:</strong> {{ job.location }}</p>
          <p class="description">
            {{ job.shortDescription || "Description coming soon..." }}
          </p>
        </div>
        <div class="card-footer">
          <button class="btn-details">View Details</button>
        </div>
      </div>
    </div>

    <!-- Modals -->
    <JobDetailsModal 
      v-if="selectedJob" 
      :job="selectedJob" 
      @close="selectedJob = null" 
      @apply="showApplicationForm"
    />
    <JobApplicationForm 
      v-if="showForm" 
      @close="showForm = false"
    />
  </div>
</template>

<script>
import JobDetailsModal from './JobDetailsModal.vue';
import JobApplicationForm from './JobApplicationForm.vue';

export default {
  components: { JobDetailsModal, JobApplicationForm },
  data() {
    return {
      searchQuery: "",
      selectedLocation: "",
      jobs: [
        {
          id: 1,
          title: "Frontend Developer",
          company: "Tech Co",
          location: "Remote",
          shortDescription: "Build and maintain web applications.",
          detailedDescription: "As a Frontend Developer, you will build and optimize web pages using Vue.js, HTML, CSS, and JavaScript.",
          requirements: [
            "2+ years of experience in frontend development.",
            "Proficient in Vue.js, HTML, CSS, and JavaScript.",
            "Experience with responsive design and cross-browser compatibility."
          ],
          salary: "7,00,000 - 9,00,000 PA",
          type: "Full-time",
          remote: "No",
        },
        {
          id: 2,
          title: "Backend Developer",
          company: "Innovate Inc.",
          location: "New York",
          shortDescription: "Develop and maintain APIs.",
          detailedDescription: "Responsible for building and optimizing backend systems using Laravel.",
          requirements: [
            "3+ years of experience in backend development.",
            "Proficient in Laravel, PHP, and database management.",
            "Experience with RESTful APIs and server-side optimization."
          ],
          salary: "5,00,000 - 7,00,000 PA",
          type: "Full-time",
          remote: "Yes",
        },
        {
          id: 3,
          title: "UX/UI Designer",
          company: "DesignHub",
          location: "Bangalore",
          shortDescription: "Create intuitive user experiences for mobile and web.",
          detailedDescription: "As a UX/UI Designer, you'll design and test user interfaces for mobile and web applications.",
          requirements: [
            "2+ years of experience in UX/UI design.",
            "Proficient in design tools like Sketch, Figma, and Adobe XD.",
            "Experience with wireframes, mockups, and prototypes."
          ],
          salary: "6,00,000 - 8,00,000 PA",
          type: "Full-time",
          remote: "No",
        },
        {
          id: 4,
          title: "Data Scientist",
          company: "Data Labs",
          location: "London",
          shortDescription: "Analyze large datasets to uncover trends and insights.",
          detailedDescription: "As a Data Scientist, you'll work with big data tools to analyze trends and provide actionable insights to the business.",
          requirements: [
            "3+ years of experience in data analysis or data science.",
            "Proficiency in Python, R, SQL, and data visualization tools.",
            "Strong understanding of machine learning and AI algorithms."
          ],
          salary: "9,00,000 - 12,00,000 PA",
          type: "Full-time",
          remote: "Yes",
        },
        {
          id: 5,
          title: "Software Engineer",
          company: "CodeWorks",
          location: "Remote",
          shortDescription: "Develop robust and scalable software solutions.",
          detailedDescription: "As a Software Engineer, you'll build software solutions that are robust, scalable, and highly performant.",
          requirements: [
            "3+ years of experience in software engineering.",
            "Proficient in Java, C++, or Python.",
            "Experience with microservices architecture and cloud platforms."
          ],
          salary: "10,00,000 - 12,50,000 PA",
          type: "Full-time",
          remote: "Yes",
        },
        {
          id: 6,
          title: "Mobile App Developer",
          company: "AppX",
          location: "Delhi",
          shortDescription: "Develop mobile applications for Android and iOS.",
          detailedDescription: "As a Mobile App Developer, you'll design and build mobile applications for both Android and iOS platforms.",
          requirements: [
            "2+ years of experience in mobile app development.",
            "Proficient in Flutter, React Native, or Swift.",
            "Experience with Google Play Store and Apple App Store deployment."
          ],
          salary: "8,00,000 - 10,00,000 PA",
          type: "Full-time",
          remote: "No",
        },
        // Add more job entries as needed
      ],
      selectedJob: null,
      showForm: false,
    };
  },
  computed: {
    uniqueLocations() {
      return [...new Set(this.jobs.map((job) => job.location))];
    },
    filteredJobs() {
      return this.jobs.filter((job) => {
        const matchesSearch =
          job.title.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          job.company.toLowerCase().includes(this.searchQuery.toLowerCase());
        const matchesLocation =
          !this.selectedLocation || job.location === this.selectedLocation;
        return matchesSearch && matchesLocation;
      });
    },
  },
  methods: {
    viewDetails(job) {
      this.selectedJob = job;
    },
    showApplicationForm() {
      this.showForm = true;
      this.selectedJob = null;
    },
    closeApplicationForm() {
      this.showForm = false;
    },
  },
};
</script>

<style>
/* Page Background and General Styling */
.page-container {
  position: relative;
  background: linear-gradient(135deg, #f0f4f8, #d6e6f3);
  min-height: 100vh;
  padding: 30px;
  overflow: hidden;
  font-family: 'Poppins', sans-serif;
}

/* Heading Styling */
.heading-container {
  text-align: center;
  margin-bottom: 40px;
}

.heading {
  font-size: 3rem;
  color: #2c3e50;
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 2px;
}

.heading-underline {
  margin: 10px auto;
  width: 140px;
  height: 4px;
  background: linear-gradient(to right, #8e44ad, #3498db);
  border-radius: 50px;
}

/* Filter Container */
.filter-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  gap: 40px; 
  flex-wrap: wrap; 
}

.search-bar-container,
.filter-dropdown-container {
  flex: 1;
  min-width: 250px; 
  margin-bottom: 10px; 
}

.search-bar {
  width: 100%;
  padding: 12px 15px;
  border-radius: 30px;
  border: none;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  font-size: 1rem;
  background: #fff;
  color: #2c3e50;
  outline: none;
}

.search-bar:focus {
  box-shadow: 0 4px 12px rgba(52, 152, 219, 0.5);
}

.filter-dropdown {
  width: 100%;
  padding: 12px 15px;
  border-radius: 30px;
  border: none;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  font-size: 1rem;
  background: #fff;
  color: #2c3e50;
  appearance: none;
  outline: none;
  cursor: pointer;
}

.filter-dropdown:hover {
  box-shadow: 0 4px 12px rgba(52, 152, 219, 0.5);
}

/* Jobs Grid */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
  padding: 10px 0;
}

/* Card Enhancements */
.card {
  background: white;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  cursor: pointer;
}

.card:hover {
  transform: translateY(-10px);
  box-shadow: 0 12px 25px rgba(0, 0, 0, 0.2);
}

/* Button Animation */
.btn-details {
  background: linear-gradient(135deg, #3498db, #8e44ad);
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 50px;
  font-size: 1rem;
  cursor: pointer;
  transition: background 0.3s ease, transform 0.2s ease;
}

.btn-details:hover {
  background: linear-gradient(135deg, #2980b9, #6c3483);
  transform: scale(1.05);
}
</style>
