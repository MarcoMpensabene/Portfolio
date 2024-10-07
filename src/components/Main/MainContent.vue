<script>
export default {
  data() {
    return {
      repos: [], // All repositories
      currentPage: 1, // Current page of displayed repos
      reposPerPage: 10, // Repos to display per page
      apiPage: 1, // GitHub API pagination page
      perPage: 30 // Number of repos per API request
    };
  },
  mounted() {
    this.fetchAllRepos();
  },
  computed: {
    paginatedRepos() {
      const start = (this.currentPage - 1) * this.reposPerPage;
      const end = start + this.reposPerPage;
      return this.repos.slice(start, end);
    },
    totalPages() {
      return Math.ceil(this.repos.length / this.reposPerPage);
    }
  },
  methods: {
    async fetchAllRepos() {
      let moreRepos = true;
      while (moreRepos) {
        try {
          const response = await fetch(`https://api.github.com/users/MarcoMpensabene/repos?per_page=${this.perPage}&page=${this.apiPage}`, {
            headers: {
              Authorization: `` // Add token here if needed
            }
          });
          const repos = await response.json();

          if (repos.length > 0) {
            this.repos = [...this.repos, ...repos]; // Append new repos
            this.apiPage++; // Move to next API page
          } else {
            moreRepos = false; // Stop when no more repos are returned
          }
        } catch (error) {
          console.error('Errore nel recupero dei repository:', error);
          moreRepos = false;
        }
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) this.currentPage++;
    },
    previousPage() {
      if (this.currentPage > 1) this.currentPage--;
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
      Here I will post all my GitHub projects and information about me.
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
        <tr v-for="repo in paginatedRepos" :key="repo.id">
          <td>{{ repo.name }}</td>
          <td><a :href="repo.html_url" target="_blank">Visita</a></td>
        </tr>
      </tbody>
    </table>
    <!-- Pagination controls -->
    <div class="pagination">
      <button @click="previousPage" :disabled="currentPage === 1">Previous</button>
      <span>Page {{ currentPage }} of {{ totalPages }}</span>
      <button @click="nextPage" :disabled="currentPage === totalPages">Next</button>
    </div>
  </div>
</template>

<style scoped lang="scss">
.main-wrapper {
  height: 100%;
  background-color: gainsboro;
}

.description {
  text-align: center;
  margin-bottom: 3rem;
  font-size: larger;
  color: black;
}

.github {
  text-align: center;
  color: black;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 1rem;
}

th,
td {
  padding: 0.75rem;
  text-align: left;
  border: 1px solid black;
}

.pagination {
  margin-top: 1rem;
  display: flex;
  justify-content: center;
  align-items: center;
}

button {
  padding: 0.5rem 1rem;
  margin: 0 0.5rem;
  cursor: pointer;
}
</style>
