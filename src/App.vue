<template>

  <div id="demo">
    <h1>Latest VS Code Issues</h1>
    <span>Search:</span>
    <input type="text" name="filterText" v-model="filterText">
    <ul>
      <li v-for="record in filteredIssues">
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
    filterText: '',
    commits: null,
    issues: null,
    filteredIssues: null
  }),

  created: function () {
    this.fetchData()
  },

  watch: {
    currentBranch: 'fetchData',
    issues: 'filterIssues',
    filterText: 'filterIssues'
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
        const issues = JSON.parse(xhr.responseText)
        issues.forEach(issue => {
          issue.is_insiders = issue.body.match(/VSCode Version:.*Insiders/);
        })
        self.issues = issues
        console.log(self.issues[0].html_url)
      }
      xhr.send()
    },
    filterIssues: function () {
      this.filteredIssues = this.issues.filter(issue =>
        issue.title.toLowerCase().indexOf(this.filterText.toLowerCase()) !== -1 ||
        issue.body.toLowerCase().indexOf(this.filterText.toLowerCase()) !== -1
      );
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
