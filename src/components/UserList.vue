<template>
  <div>
    <table>
      <thead>
        <tr>
          <th @click="sort('title')">Tytuł</th>
          <th @click="sort('director')">Reżyser</th>
          <th @click="sort('composer')">Muzyka</th>
          <th @click="sort('release_date')">Premiera</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="test in tests" :key="test.id">
          <td>{{ test.id }}</td>
          <td>{{ test.name }}</td>
          <td>{{ test.login_name }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
//import MovieItem from "./MovieItem";
import gql from "graphql-tag";
const GET_LIST = gql`
  subscription getTests {
    tests {
      id
      login_name
      name
    }
  }
`;
export default {
  name: "UserList",
  //components: { MovieItem },
  data() {
    return {
      tests: []
    };
  },
  apollo: {
    $subscribe: {
      tests: {
        query: GET_LIST,
        result(data) {
          // Let's update the local data
          this.tests = data.data.tests;
        }
      }
    }
  }
};
</script>
<style></style>
