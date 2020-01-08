<template>
  <div class="hello">
    <!-- <div v-for="person in allPeople.people" :key="person.name">{{person.name}}</div> -->

    <!-- <ApolloQuery
      :query="gql => gql `query {
    allPeople {
    people {
    name
    }
    }
    }`"
    >
     <template v-slot="{result: {loading, error, allPeople}}"></template>
      <div v-if="allPeople">
        <div v-for="person in allPeople.people" :key="person.name">{{person.name}}</div>
      </div>
    </ApolloQuery>-->
    <ApolloQuery :query="require('../graphql/allCharacters.gql')" :variables="{ first: 5 }">
      <template v-slot="{result: {loading, error, data}}">
        <div v-if="data">
          <div v-for="person in data.allPeople.people" :key="person.name">{{person.name}}</div>
        </div>
      </template>
    </ApolloQuery>
  </div>
</template>

<script>
// import gql from "graphql-tag";

export default {
  name: "HelloWorld",
  data() {
    return {
      first: 2
    };
  },
  props: {
    msg: String
  }
  // apollo: {
  //   allPeople: gql`
  //     query {
  //       allPeople {
  //         people {
  //           name
  //         }
  //       }
  //     }
  //   `
  // }
};
</script>

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
