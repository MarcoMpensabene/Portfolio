<script>
export default {
  data() {
    return {
      repos: [],
      page: 1, // Track the current page
      perPage: 30 // Number of repos per page (default is 30)
    };
  },
  mounted() {
    this.fetchAllRepos();
  },
  methods: {
    async fetchAllRepos() {
      let moreRepos = true;
      while (moreRepos) {
        try {
          const response = await fetch(`https://api.github.com/users/MarcoMpensabene/repos?per_page=${this.perPage}&page=${this.page}`, {
            headers: {
              Authorization: ``
            }
          });
          const repos = await response.json();

          if (repos.length > 0) {
            this.repos = [...this.repos, ...repos]; // Append the new repos
            this.page++; // Move to the next page
          } else {
            moreRepos = false; // Stop when no more repos are returned
          }
        } catch (error) {
          console.error('Errore nel recupero dei repository:', error);
          moreRepos = false;
        }
      }
    }
  }
};

</script>


<template>
  <div class="main-wrapper">
    <div class="description">
      I'm a Jr full stack web developer that is starting is career , i don't have much to offer right now beside being
      honest and have a lot of passion and curiosity for almost anything related to technology.
    </div>
    <div class="github">
      Here i will post all my GitHubProject and information abount me .
    </div>
    <h2>I miei progetti GitHub</h2>
    <table>
      <thead>
        <tr>
          <th>Nome Progetto</th>
          <th>Link</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="repo in repos" :key="repo.id">
          <td>{{ repo.name }}</td>
          <td><a :href="repo.html_url" target="_blank">Visita</a></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped lang="scss">
div .main-wrapper {
  height: 100%;
  background-color: gainsboro;
}

div .description {
  text-align: center;
  margin-bottom: 3rem;
  font-size: larger;
  color: black;
}

div .github {
  text-align: center;
  color: black;
}
</style>
