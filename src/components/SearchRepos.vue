<template>
  <div class="apollo-example">
    <div class="form">
      <label for="field-name" class="label">Github Username</label>
      <input
        v-model="login"
        placeholder="Github login"
        class="input"
        id="field-name"
      >
    </div>

    <ApolloQuery
      :query="require('../graphql/User.gql')"
      :variables="{ login }"
    >
      <template slot-scope="{ result: { loading, error, data } }">
        <!-- Loading -->
        <div v-if="loading" class="loading apollo">Loading...</div>

        <!-- Error -->
        <div v-else-if="error" class="error apollo">
          {{ error.gqlError.message }}
        </div>

        <!-- Result -->
        <div v-else-if="data" class="result apollo">
          <div v-for="repo in data.user.repositories.edges" :key="repo.id" class="repo">
            <div class="repo-head">
              <a v-bind:href="repo.node.url" target="_blank" class="repo-name">{{ repo.node.name }}</a>
              <div class="flex">
                <svg height="20" class="octicon-star" viewBox="0 0 16 16" version="1.1" width="16" aria-hidden="true"><path fill-rule="evenodd" d="M8 .25a.75.75 0 01.673.418l1.882 3.815 4.21.612a.75.75 0 01.416 1.279l-3.046 2.97.719 4.192a.75.75 0 01-1.088.791L8 12.347l-3.766 1.98a.75.75 0 01-1.088-.79l.72-4.194L.818 6.374a.75.75 0 01.416-1.28l4.21-.611L7.327.668A.75.75 0 018 .25zm0 2.445L6.615 5.5a.75.75 0 01-.564.41l-3.097.45 2.24 2.184a.75.75 0 01.216.664l-.528 3.084 2.769-1.456a.75.75 0 01.698 0l2.77 1.456-.53-3.084a.75.75 0 01.216-.664l2.24-2.183-3.096-.45a.75.75 0 01-.564-.41L8 2.694v.001z"></path></svg>
                {{ repo.node.stargazers.totalCount}}
              </div>
            </div>
            <div v-if="repo.node.description" class="repo-description">{{ repo.node.description }}</div>
          </div>
        </div>

        <!-- No result -->
        <div v-else class="no-result apollo">No result :(</div>
      </template>
    </ApolloQuery>
  </div>
  
</template>

<script>
import User from '../graphql/User.gql'
export default {
  data () {
    return {
      login: 'yusufseyrek',
    }
  },
  apollo: {
    user: User
  }
}
</script>

<style scoped>
.form,
.input,
.apollo,
.message {
  padding: 12px;
}

label {
  display: block;
  margin-bottom: 6px;
}

.input {
  font-family: inherit;
  font-size: inherit;
  border: solid 2px #ccc;
  border-radius: 3px;
}

.error {
  color: red;
}

.repo {
  padding: 10px;
  display: flex;
  flex-direction: column;
}

.repo-head {
  display: flex;
  justify-content: space-between;
}

.octicon-star {
  margin-right: 4px;
}

.repo:nth-child(odd) {
  background-color: #779ecb30;
}

.repo-name {
  font-weight: bold;
  font-size: 20px;
  text-align: left;
}

.repo-description {
  text-align: left;
  margin-top: 10px;
}

.flex {
  display: flex;
}

a { color: inherit; } 
</style>
