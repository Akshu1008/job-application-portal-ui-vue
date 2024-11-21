<template>
  <div class="page-container">
    <!-- Centered and styled heading -->
    <div class="heading-container">
      <h1 class="heading">Available Jobs</h1>
      <div class="heading-underline"></div>
    </div>

    <div class="grid">
      <div
        v-for="job in jobs"
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
      jobs: [
        {
          id: 1,
          title: "Frontend Developer",
          company: "Tech Co",
          location: "Remote",
          shortDescription: "Build and maintain web applications.",
        },
        {
          id: 2,
          title: "Backend Developer",
          company: "Innovate Inc.",
          location: "New York",
          shortDescription: "Develop and maintain APIs.",
        },
        {
          id: 3,
          title: "UX/UI Designer",
          company: "DesignHub",
          location: "Bangalore",
          shortDescription: "Create intuitive user experiences for mobile and web.",
        },
        {
          id: 4,
          title: "Project Manager",
          company: "BizCorp",
          location: "London",
          shortDescription: "Manage cross-functional teams and project deliverables.",
        },
        {
          id: 5,
          title: "Data Scientist",
          company: "DataSolutions",
          location: "Germany",
          shortDescription: "Analyze and interpret complex datasets to drive decision-making.",
        },
        {
          id: 6,
          title: "Software Engineer",
          company: "CodeWorks",
          location: "Australia",
          shortDescription: "Develop robust and scalable software solutions.",
        },
        {
          id: 7,
          title: "Digital Marketing Specialist",
          company: "AdSphere",
          location: "Canada",
          shortDescription: "Plan and execute online marketing campaigns.",
        },
        {
          id: 8,
          title: "Cybersecurity Analyst",
          company: "SecureTech",
          location: "USA",
          shortDescription: "Protect organizational data and prevent security breaches.",
        },
        {
          id: 9,
          title: "DevOps Engineer",
          company: "CloudStream",
          location: "Remote",
          shortDescription: "Automate deployment pipelines and ensure infrastructure reliability.",
        },

        // Add more jobs as needed
      ],
      selectedJob: null,
      showForm: false,
    };
  },
  methods: {
    viewDetails(job) {
      this.selectedJob = job;
    },
    showApplicationForm() {
      this.showForm = true; // Show the application form
      this.selectedJob = null; // Close the Job Details Modal
    },
    closeApplicationForm() {
      this.showForm = false;
    },
  },
};
</script>

<style>
/* Background with rounded circles */
.page-container {
  position: relative;
  background-color: #ecf0f1;
  background-image: radial-gradient(circle, rgba(52, 152, 219, 0.1), rgba(236, 240, 241, 0.6));
  min-height: 100vh;
  padding: 20px;
  overflow: hidden;
}

/* Center and design the heading */
.heading-container {
  text-align: center;
  margin-bottom: 40px;
}

.heading {
  font-size: 2.8rem;
  color: #34495e;
  font-family: 'Roboto', sans-serif;
  font-weight: 700;
  margin: 0;
}

.heading-underline {
  margin: 10px auto;
  width: 120px;
  height: 3px;
  background: linear-gradient(to right, #8e44ad, #3498db);
  border-radius: 50px;
}

/* Jobs grid styling */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 20px;
  padding: 0 15px;
}

/* Card Styling */
.card {
  background: #fff;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  border: 1px solid #ecf0f1;
}

.card:hover {
  transform: translateY(-10px);
  box-shadow: 0 12px 20px rgba(0, 0, 0, 0.15);
}

/* Card Header */
.card-header {
  background: linear-gradient(135deg, #8e44ad, #3498db);
  color: white;
  padding: 20px;
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
}

.job-title {
  font-size: 1.8rem;
  font-weight: bold;
  margin: 0;
}

.company-name {
  font-size: 1.1rem;
  opacity: 0.8;
  margin: 5px 0 0;
}

/* Card Body */
.card-body {
  padding: 15px 20px;
}

.location,
.description {
  font-size: 1rem;
  color: #7f8c8d;
  margin: 10px 0;
}

/* Card Footer */
.card-footer {
  padding: 15px 20px;
  background: #f9f9f9;
  border-bottom-left-radius: 20px;
  border-bottom-right-radius: 20px;
  text-align: right;
}

.btn-details {
  background: #3498db;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 50px;
  font-size: 1.1rem;
  cursor: pointer;
  transition: background 0.3s ease, transform 0.2s ease;
}

.btn-details:hover {
  background: #2980b9;
  transform: translateY(-3px);
}

.btn-details:active {
  transform: translateY(0);
}
</style>
