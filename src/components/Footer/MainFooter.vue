<script>
export default {
  data() {
    return {
      personalLinks: [
        {
          name: "GitHub",
          link: "https://github.com/MarcoMpensabene"
        },
        {
          name: "Linkedin",
          link: "https://www.linkedin.com/in/marco-maria-pensabene-845a00325/"
        },
        {
          name: "ProfessionalEmail",
          link: "marcompensabene@gmail.com"
        },
        {
          name: "TelephoneNumber",
          link: "+39 3516860837"
        }
      ]
    }
  },
  methods: {
    formatLinkText(linkName) {
      return linkName === "ProfessionalEmail" ? "Email" :
        linkName === "TelephoneNumber" ? "Call Me" : linkName;
    }
  }
}

</script>

<template>

  <div class="footer">
    <h1>My Social Links </h1>
    <div class="footer-content">
      <div class="social-links" v-for="personalLink in personalLinks">
        <a :href="personalLink.link" target="_blank">{{ personalLink.name }}</a>

      </div>
    </div>
  </div>

</template>

<style lang="scss" scoped>
.footer {
  background-color: #2c3e50;
  padding: 40px;
  text-align: center;
  color: white;
}

h1 {
  color: #3498db;
  font-family: 'Roboto', sans-serif;
  font-size: 2rem;
  margin-bottom: 1.5rem;
}

.footer-content {
  display: flex;
  justify-content: center;
  gap: 20px;
  flex-wrap: wrap;
}

.social-links {
  margin-bottom: 15px;
}

.footer a {
  color: #ecf0f1;
  font-size: 1.2rem;
  font-weight: 500;
  padding: 10px 20px;
  background-color: #3498db;
  border-radius: 5px;
  text-decoration: none;
  transition: background-color 0.3s ease;
}

.footer a:hover {
  background-color: #2980b9;
}

.phone-link {
  background-color: #e67e22;
}

.phone-link:hover {
  background-color: #d35400;
}
</style>
