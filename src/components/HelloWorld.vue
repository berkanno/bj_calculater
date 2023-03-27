<template>
  <v-container>
    <v-row>
      <v-col
        cols="12"
        class="text-uppercase text-center text-black my-10"
        style="letter-spacing: 20px"
      >
        blackjack calculater
      </v-col>
      <v-col cols="12" sm="12" md="6" lg="6" xl="6">
        <v-row>
          <v-col cols="12" class="text-center">elde edilen kartlar</v-col>
          <v-col cols="6">
            <v-select
              v-model="val"
              @keyup.enter="ss(val)"
              :items="[
                'A',
                '2',
                '3',
                '4',
                '5',
                '6',
                '7',
                '8',
                '9',
                '10',
                'K',
                'J',
                'Q',
              ]"
            ></v-select>
          </v-col>
          <v-col cols="6" class="text-red"></v-col>
        </v-row>
      </v-col>
      <v-col cols="12" sm="12" md="6" lg="6" xl="6">
        <v-card height="100%">
          <v-row class="ma-4 d-flex justify-center ">
            <v-col
              cols="12"
              class="text-uppercase text-center"
              style="letter-spacing: 5px"
            >
              kalan kart sayısı</v-col
            >
            <v-col cols="6" sm="6" md="4" lg="3" xl="3" v-for="item in cards" :key="item" class="text-center">

                  <v-card>
                    <v-card-title class="text-overline">
                      kart : {{ item.item }}
                    </v-card-title>
                    <v-card-text class="text-caption text-uppercase">
                      sayısı : {{ item.count }}
                    </v-card-text>
                  </v-card>
             
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="12" class="text-uppercase text-center" style="letter-spacing:5px">Log</v-col>
            <v-col cols="12">
              asdasdasda
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
export default {
  data() {
    return {
      log:[],
      val: "",
      cards: [
        { item: "A", count: 4, value: 1 },
        { item: "2", count: 4, value: 2 },
        { item: "3", count: 4, value: 3 },
        { item: "4", count: 4, value: 4 },
        { item: "5", count: 4, value: 5 },
        { item: "6", count: 4, value: 6 },
        { item: "7", count: 4, value: 7 },
        { item: "8", count: 4, value: 8 },
        { item: "9", count: 4, value: 9 },
        { item: "10", count: 4, value: 10 },
        { item: "J", count: 4, value: 10 },
        { item: "Q", count: 4, value: 10 },
        { item: "K", count: 4, value: 10 },
      ],
    };
  },
  methods: {
    ss(value: string) {
      this.cards
        .filter((x) => x.item == value)
        .map((x: any) => (
          x.count == 0 ? (x.count = 0) : x.count--,


        ));
    },
  },
};
</script>
