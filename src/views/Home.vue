<template>
  <div>
    <h1 class="display-1 my-3 text-center font-weight-medium">
      Real-time Crypto Tracking
    </h1>
    <v-col class="d-flex justify-center mx-auto" lg="12">
      <v-card v-for="crypto in mainList" :key="crypto.id" outlined class="mx-2">
        <v-list-item three-line>
          <v-list-item-avatar class="d-flex flex-column" tile size="30">
            <img :src="crypto.image" alt="" />
          </v-list-item-avatar>
          <v-list-item-content>
            <div class="text-overline">{{ crypto.symbol }}</div>
            <v-list-item-title class="text-h5 mb-1">
              {{ crypto.name }}:
              <span>${{ crypto.current_price }} </span>
            </v-list-item-title>
            <v-list-item-subtitle></v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-card>
    </v-col>
    <v-col lg="9" class="mx-auto">
      <v-card>
        <v-card-title>
          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Search"
            single-line
            hide-details
          ></v-text-field>
        </v-card-title>

        <v-data-table :headers="headers" :items="postList" :search="search">
        </v-data-table>
      </v-card>
    </v-col>
    <!-- <v-col
      class="mx-auto px-5"
      lg="9"
      v-for="crypto in postList"
      :key="crypto.id"
    >
      <v-list dar>
        <v-list-item-group>
          <v-list-item-avatar size="30">
            <img :src="crypto.image" alt="" />
          </v-list-item-avatar>
          <v-list-content> {{ crypto.name }} </v-list-content>
          <v-list-content class="">
            {{ crypto.current_price }}
          </v-list-content>
        </v-list-item-group>
      </v-list>
      
    </v-col> -->
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Home",
  data() {
    return {
      postList: [],
      mainList: [],
      search: "",
      cryptoObj: {
        name: null,
        image: null,
        currentPrice: null,
        change24hr: null,
      },
      headers: [
        {
          text: "Crypto name",
          align: "start",
          filterable: true,
          value: "name",
        },
        { text: "Current price", value: "current_price", align: "center" },
        { text: "Market cap", value: "market_cap", align: "end" },
      ],
    };
  },
  created() {
    axios
      .get(
        "https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false"
      )
      .then((response) => {
        this.postList = response.data;
        console.log(response.data);
        // let data = response.data;
        // data.forEach((element) => {
        //   this.cryptoObj.name = element.name;
        //   this.cryptoObj.image = element.image;
        //   this.cryptoObj.currentPrice = element.currentPrice;
        //   this.postList.push(element);
        // });

        console.log(response);
        console.log(this.postList);
        this.mainList = response.data.filter((val) => {
          return (
            val.id === "bitcoin" || val.id === "ethereum" || val.id === "ripple"
          );
        });
      });
  },
};
</script>
