<template>

  <div id="demo">
    <h1>Latest Vue.js Issues</h1>
    <template v-for="branch in branches">
      <input type="radio"
             :id="branch"
             :value="branch"
             name="branch"
             v-model="currentBranch">
      <label :for="branch">{{ branch }}</label>
    </template>
    <p>vuejs/vue@{{ currentBranch }}</p>
    <ul>
      <li v-for="record in issues">
        <issue v-bind:record="record"></issue>
      </li>
    </ul>
  </div>

</template>

<script>
import Commit from './Commit.vue'
import Issue from './Issue.vue'
var apiURL = 'https://api.github.com/repos/microsoft/vscode/issues?per_page=20'
export default {

  components: {
    commit: Commit,
    issue: Issue
  },

  data: () => ({
    branches: ['master', 'dev'],
    currentBranch: 'master',
    commits: null,
    issues: null
  }),

  created: function () {
    this.fetchData()
  },

  watch: {
    currentBranch: 'fetchData'
  },

  filters: {
    truncate: function (v) {
      var newline = v.indexOf('\n')
      return newline > 0 ? v.slice(0, newline) : v
    },
    formatDate: function (v) {
      return v.replace(/T|Z/g, ' ')
    }
  },

  methods: {
    fetchData: function () {
      var xhr = new XMLHttpRequest()
      var self = this
      xhr.open('GET', apiURL + self.currentBranch)
      xhr.onload = function () {
        self.issues = JSON.parse(xhr.responseText)
        console.log(self.issues[0].html_url)
      }
      xhr.send()
    }
  }
}
</script>

<style>

  #demo {
    font-family: 'Helvetica', Arial, sans-serif;
  }

  a {
    text-decoration: none;
    color: #f66;
  }

  li {
    line-height: 1.5em;
    margin-bottom: 20px;
  }

  .author,
  .date {
    font-weight: bold;
  }

</style>
