<template>
  <div class="hello">
    <ApolloQuery :query="require('../graphql/allCharacters.gql')" :variables="{ first: 3 }">
      <template v-slot="{result: {loading, error, data}}">
        <div v-if="data">
          <div
            class="sw-person"
            v-for="person in data.allPeople.people"
            :key="person.name"
            @click="showModal = !showModal"
          >{{person.name}}</div>
        </div>
      </template>
    </ApolloQuery>
    <modal :person="person" v-if="showModal" @close="closeModalHandler">
      <ApolloQuery :query="require('../graphql/characterData.gql')" :variables="{ name: 'C3PO'}"></ApolloQuery>
      <template v-slot="{result: {loading, error, data}}">
        <div v-if="data"></div>
      </template>

      <PersonForm></PersonForm>
    </modal>
  </div>
</template>

<script>
// import gql from "graphql-tag";
import Modal from "./Modal";
import PersonForm from "./PersonForm";
export default {
  name: "People",
  components: {
    Modal,
    PersonForm
  },
  data() {
    return {
      showModal: false,
      first: 2
    };
  },
  props: {
    msg: String
  },
  methods: {
    closeModalHandler() {
      this.showModal = false;
    }
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
sw-person {
  color: #42b983;
}
</style>
