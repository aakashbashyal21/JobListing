<template>
  <div id="app">
    <header class="bg-dark-cyan container-fluid px-0 mb-6">
      <img src="./assets/images/bg-header-desktop.svg" alt="" />
    </header>
    <div class="container">
      <b-card
        body-class="d-flex flex-column flex-lg-row p-10"
        class="shadow-sm bg-white rounded border-0 my-n16"
      >
        <div
          class="d-flex align-items-center flex-row flex-wrap flex-lg-nowrap flex-lg-nowrap"
        >
          <div
            :key="item"
            :v-if="item !== null"
            v-for="item in selectItem"
            role="button"
            class="d-flex flex-row mr-2"
          >
            <h6 class="bg-light-cyan rounded-left text-cyan p-2">{{ item }}</h6>
            <h6
              @click="removeSelectedItem(item)"
              class="bg-dark-cyan text-white rounded-right p-2 font-weight-bold closetag"
              aria-hidden="true"
            >
              &times;
            </h6>
          </div>
        </div>
        <div v-if="selectItem.length" class="mt-4 ml-lg-auto">
          <h6 class="text-dark-cyan" role="button" @click="clearSelectedItem">
            Clear
          </h6>
        </div>
      </b-card>
      <template v-for="data in resultQuery">
        <JobBoard
          @clicked-show-detail="clickedShowDetailModal"
          :tools="data.tools"
          :languages="data.languages"
          :isNew="data.isNew"
          :featured="data.featured"
          :role="data.role"
          :level="data.level"
          :location="data.location"
          :contract="data.contract"
          :postedAt="data.postedAt"
          :position="data.position"
          :company="data.company"
          :img="data.logo"
          :key="data.id"
        ></JobBoard>
      </template>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";

import JobBoard from "./components/JobBoard";
import json from "./assets/data/data.json";

export default {
  name: "App",
  computed: {
    resultQuery() {
      if (this.selectItem.length !== 0) {
        return this.myJson.filter((el) => {
          if (this.selectItem && this.selectItem.length) {
            var allElement = [el.role, el.level].concat([
              ...el.tools,
              ...el.languages,
            ]);
            return this.selectItem.every((se) => allElement.includes(se));
          }
        });
      } else {
        return this.myJson;
      }
    },
  },
  methods: {
    clearSelectedItem: function() {
      this.selectItem = [];
    },
    removeSelectedItem(value) {
      const index = this.selectItem.indexOf(value);
      if (index > -1) {
        this.selectItem.splice(index, 1);
      }
    },
    clickedShowDetailModal: function(value) {
      if (this.selectItem.includes(value) === false)
        this.selectItem.push(value);
    },
  },
  data() {
    return {
      selectItem: [],
      myJson: json,
    };
  },
  components: {
    JobBoard,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Spartan:wght@500;700&display=swap");
* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}
:root {
  --Desaturated-Dark-Cyan: hsl(180, 29%, 50%);
  --Light-Grayish-Cyan: hsl(180, 52%, 96%);
  --Light-Grayish-Cyan-Filter-Tablets: hsl(180, 31%, 95%);
  --Dark-Grayish-Cyan: hsl(180, 8%, 52%);
  --Very-Dark-Grayish-Cyan: hsl(180, 14%, 20%);
  --shadow: rgba(44, 58, 58, 0.14);
}

body {
  background: var(--Light-Grayish-Cyan);
  font-family: "Spartan", sans-serif;
  font-size: 15px;
}
.text-dark-cyan {
  color: var(--Desaturated-Dark-Cyan);
}

.bg-dark-cyan {
  background-color: var(--Desaturated-Dark-Cyan);
}
.text-cyan {
  color: hsl(180, 29%, 50%);
}

.bg-light-cyan {
  background-color: hsl(180, 31%, 95%);
}

header > img {
  width: 100%;
  height: 100px;
}
.mb-6 {
  margin-bottom: 1.5rem !important;
}
.p-6 {
  padding: 1.5rem !important;
}

.border-left-4 {
  border-left: 4px solid var(--Desaturated-Dark-Cyan) !important;
}
.mt-n16,
.my-n16 {
  margin-top: -4rem;
}
.mt-16,
.my-16 {
  margin-top: 4rem !important;
}
.p-10 {
  padding: 2.5rem !important;
}

.tag-item:hover {
  background-color: var(--Desaturated-Dark-Cyan);
  color: var(--Light-Grayish-Cyan);
}
.closetag:hover {
  background-color: var(--Very-Dark-Grayish-Cyan);
}
.position:hover {
  color: var(--Desaturated-Dark-Cyan);
}
.border-top-1 {
  border-top: 1px solid #e3e7eb !important;
}
@media (min-width: 992px) {
  .border-lg-top-0 {
    border-top: 0 !important;
  }
  .mt-lg-8 {
    margin-top: 2rem !important;
  }
}
</style>
