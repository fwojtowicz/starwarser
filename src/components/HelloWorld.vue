<template>
  <div class="hello">
    <div v-for="person in allPeople.people" :key="person.name">{{person.name}}</div>
  </div>
</template>

<script>
import gql from "graphql-tag";
export default {
  name: "HelloWorld",
  data() {
    return {
      first: 10
    };
  },
  props: {
    msg: String
  },
  apollo: {
    allPeople: gql`
      query {
        allPeople {
          people {
            name
          }
        }
      }
    `
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
