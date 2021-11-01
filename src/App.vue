<template>
  <div id="app">
    <div class="office" @click="showPersonCard">
      <Map />
      <SideMenu 
        :isUserOpenned="personCardOpened"
        :person="person"
        @isUserOpenned="personCardOpened = false"
      />
    </div>
  </div>
</template>

<script>
import Map from "./components/Map.vue";
import SideMenu from "./components/SideMenu.vue";
import people from "@/assets/data/people.json";

export default {
  name: "App",
  components: {
    Map,
    SideMenu,
  },
  data() {
    return {
      personCardOpened: false,
      person: null,
    };
  },
  methods: {
    showPersonCard({ target }) {
      if (target.matches(".wrapper-table")) {
        this.personCardOpened = true;
        const table = target.closest(".employer-place");
        people.forEach((item) => {
          if (item.tableId == table.id) {
            this.person = item;
          }
        });
      } else {
        this.personCardOpened = false;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  background-color: #fafafa;
  padding: 24px;
  box-sizing: border-box;
}

html,
body,
#app {
  height: 100%;
}

* {
  box-sizing: border-box;
}

h3 {
  margin-top: 0px;
}

.office {
  display: grid;
  grid-template-columns: 1fr 320px;
  border-radius: 6px;
  border: 1px solid #ccd8e4;
  height: 100%;
  background: white;
  max-width: 1500px;
  margin: 0 auto;
}
</style>
