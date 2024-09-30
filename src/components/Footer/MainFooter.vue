<script>
export default {
  data() {
    return {
      personalLinks: [{
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
  padding: 20px;
  text-align: center;

  h1 {
    color: aqua;
    margin-bottom: 2rem;
  }
}

.footer a {
  color: #007bff;
  text-decoration: none;
}


.social-links a {
  margin: 0 15px;
}

.social-links {
  margin-bottom: 15px;
}

.cta-button {
  background-color: #007bff;
  color: #fff;
  padding: 10px 20px;
  text-decoration: none;
  border-radius: 5px;
}
</style>
