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
    <h2>My GitHub Projects</h2>
    <table>
      <thead>
        <tr>
          <th>Projects Name</th>
          <th>Link</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="repo in paginatedRepos" :key="repo.id">
          <td class="repo-name">{{ repo.name }}</td>
          <td><a :href="repo.html_url" target="_blank">Visit</a></td>
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
  background-color: #f7f7f7;
  /* Light background for contrast */
  font-family: 'Roboto', sans-serif;
  /* Modern font */
  padding: 2rem;
}

.description,
.github {
  text-align: center;
  color: #333;
  margin-bottom: 1.5rem;
  font-size: 1.5rem;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;

}

h2 {
  text-align: center;
  font-size: 1.8rem;
  color: #2c3e50;
  margin-bottom: 1.5rem;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 1rem;
  background-color: white;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  /* Soft shadow for depth */
  border-radius: 10px;
  overflow: hidden;

}

.repo-name {
  text-transform: uppercase;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  font-weight: bold;
}

thead {
  background-color: #2c3e50;
  /* Dark header background */
  color: white;
  /* White text for contrast */
}

th,
td {
  padding: 1rem;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

tbody tr {
  transition: background-color 0.2s ease-in-out;
}

tbody tr:hover {
  background-color: #f1f1f1;
  /* Soft hover effect */
}

th {
  font-weight: bold;
  text-transform: uppercase;
}

td a {
  text-decoration: none;
  color: #3498db;
  /* Link color */
  font-weight: bold;
}

td a:hover {
  color: #2980b9;
  /* Darker color on hover */
}

.pagination {
  margin-top: 1.5rem;
  display: flex;
  justify-content: center;
  align-items: center;
}

button {
  padding: 0.75rem 1.5rem;
  margin: 0 0.5rem;
  background-color: #3498db;
  /* Primary button color */
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #2980b9;
  /* Darker hover effect */
}

button:disabled {
  background-color: #bdc3c7;
  /* Disabled button */
  cursor: not-allowed;
}

span {
  font-size: 1rem;
  color: #2c3e50;
}
</style>
