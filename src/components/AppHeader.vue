<template>
  <header class="header">
    <div class="container">
      <h1 class="main-heading">Job Application Portal</h1>
      <p class="subheading">Find your dream job with ease!</p>
    </div>
  </header>
</template>

<script>
export default {};
</script>

<style>
.header {
  background: linear-gradient(135deg, #4c8bf5, #4adede);
  color: white;
  text-align: center;
  padding: 60px 20px;
  border-bottom-left-radius: 50px;
  border-bottom-right-radius: 50px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

.main-heading {
  font-size: 3rem;
  font-weight: 700;
  font-family: 'Poppins', sans-serif;
  text-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  margin-bottom: 15px;
}

.subheading {
  font-size: 1.2rem;
  font-weight: 400;
  opacity: 0.9;
  font-family: 'Roboto', sans-serif;
  margin: 0;
}

@media (max-width: 768px) {
  .main-heading {
    font-size: 2.5rem;
  }
  .subheading {
    font-size: 1rem;
  }
}
</style>
