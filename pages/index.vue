<template>
  <div>
    <h4 class="text-h4 text-center mb-4">
      FOREACH, MAP, FILTER, SORT, REDUCE & FETCH
    </h4>
    <v-card class="" outlined>
      <v-row danse>
        <v-col cols="4" class="pa-10 btns">
          <v-btn @click="addUser" block rounded large color="primary"
            ><v-icon left>mdi-account</v-icon>
            <span>Add Person</span>
          </v-btn>
          <v-btn @click="doubleMoney" block rounded large color="info">
            <v-icon left>mdi-cash-multiple</v-icon>
            <span> Double Money</span></v-btn
          >
          <v-btn
            @click="showMillionaires"
            block
            rounded
            large
            color="secondary"
          >
            <v-icon left>mdi-bed-king</v-icon>
            <span> Show Only Millionaires</span></v-btn
          >
          <v-btn @click="sortByRichest" block rounded large color="success">
            <v-icon left>mdi-cash</v-icon>
            <span> Sort By Richest</span></v-btn
          >
          <v-btn @click="calculateWealth" block rounded large color="warning">
            <v-icon left>mdi-format-horizontal-align-center</v-icon>
            <span> Calculate Entire Wealth</span></v-btn
          >
        </v-col>
        <v-col cols="8" class="pa-10">
          <div class="d-flex align-center data justify-space-between">
            <h5 class="text-h5 font-weight-bold">Person</h5>
            <h5 class="text-h5 info--text font-weight-bold">Wealth</h5>
          </div>
          <div
            v-for="(obj, i) in dataList"
            :key="i"
            class="d-flex align-center my-4 justify-space-between"
          >
            <h5 class="text-h5">
              <v-avatar v-if="obj.image" size="40">
                <v-img
                  :lazy-src="obj.image"
                  max-height="150"
                  max-width="250"
                  :src="obj.image"
                ></v-img>
              </v-avatar>
              {{ obj.name }}
            </h5>
            <h5 class="text-h5">${{ obj.money }}</h5>
          </div>
          <div
            v-if="showTotal"
            class="d-flex align-center total justify-space-between"
          >
            <h5 class="text-h5 font-weight-bold">Total</h5>
            <h5 class="text-h5 info--text font-weight-bold">
              ${{ totalWealth }}
            </h5>
          </div>
        </v-col>
      </v-row>
    </v-card>
  </div>
</template>

<script>
export default {
  async fetch() {
    this.getUser();
    console.log(`fetch`);
  },
  data() {
    return {
      dataList: [],
      showTotal: false,
      totalWealth: null,
    };
  },
  methods: {
    async getUser() {
      const res = await fetch("https://randomuser.me/api");
      const data = await res.json();
      const user = data.results[0];
      const new_user = {
        name: `${user.name.first} ${user.name.last}`,
        money: `${Math.floor(Math.random() * 1000000)}`,
        image: user.picture.thumbnail,
      };
      this.dataList.push(new_user);
      // console.log(new_user);
    },
    addUser() {
      this.getUser();
      this.showTotal = false;
    },
    doubleMoney() {
      this.showTotal = false;
      this.dataList = this.dataList.map((person) => {
        const tempPerson = {
          image: person.image,
          name: person.name,
          money: person.money * 2,
        };
        return tempPerson;
      });
    },
    showMillionaires() {
      this.showTotal = false;
      this.dataList = this.dataList.filter((item) => item.money >= 1000000);
    },
    sortByRichest() {
      this.showTotal = false;
      this.dataList.sort((a, b) => b.money - a.money);
    },
    calculateWealth() {
      this.showTotal = true;
      const totalWealth = this.dataList.reduce(
        (acc, user) => (acc += user.money),
        0
      );
      this.totalWealth = totalWealth;
    },
    formatNumberAsMoney(number) {
      return "$" + number.toFixed(2).replace(/\d(?=(\d{3})+\.)/g, "$&,");
    },
  },
  mounted() {
    // this.getUser();
    console.log(this.formatedObj);
  },
  computed: {},
};
</script>
<style>
.btns {
  display: grid !important;
  gap: 10px !important;
  align-self: start;
}
.total {
  padding-top: 8px;
  border-top: 2px solid #c7c7c7;
}
.data {
  padding-bottom: 8px;
  border-bottom: 2px solid #c7c7c7;
}
</style>
