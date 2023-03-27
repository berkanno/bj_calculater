<template>
  <v-container>
    <v-row>
      <v-col
        cols="12"
        class="text-uppercase text-center text-black my-10"
        style="letter-spacing: 20px"
      >
        <v-app-bar style="position: fixed">
          <v-col cols="12" class="text-center"> blackjack calculater </v-col>
        </v-app-bar>
      </v-col>
      <v-col cols="12" sm="12" md="6" lg="6" xl="6">
        <v-row>
          <v-col cols="6">
            <v-col cols="12" class="text-center text-overline"
              >alınan kartlar(ben)</v-col
            >
            <v-col cols="12">
              <v-text-field
                variant="outlined"
                ref="valueReset"
                v-model="value"
                @keyup.enter="valueCount(value)"
                clearable
              ></v-text-field>
            </v-col>
          </v-col>
          <v-col cols="6">
            <v-col cols="12" class="text-center text-overline"
              >alınan kartlar(o)</v-col
            >
            <v-col cols="12">
              <v-text-field
                variant="outlined"
                ref="valueRivalReset"
                v-model="valueRival"
                @keyup.enter="valueCountRival(valueRival)"
                clearable
              ></v-text-field>
            </v-col>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" class="text-center">
            <v-btn width="40%">
              <v-row>
                <v-col class="text-overline" @click="calculate()">
                  hesapla
                </v-col>
              </v-row>
            </v-btn>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12">
            <v-card height="100%">
              <v-row class="mx-2 mt-2">
                <v-col cols="6">
                  <v-col cols="12" class="text-center text-overline">
                    Kartlarım:
                  </v-col>
                  <v-row class="d-flex justify-center">
                    <v-col v-for="item in valueData" :key="item" cols="2">
                      {{ item }}
                    </v-col>
                  </v-row>
                </v-col>
                <v-col cols="6">
                  <v-col cols="12" class="text-center text-overline">
                    Kartları:
                  </v-col>
                  <v-row class="d-flex justify-center">
                    <v-col v-for="item in valueRivalData" :key="item" cols="2">
                      {{ item }}
                    </v-col>
                  </v-row>
                </v-col>
                <v-col cols="12" class="text-center text-overline">Sonuc</v-col>
              </v-row>
            </v-card>
          </v-col>
        </v-row>
      </v-col>
      <v-col cols="12" sm="12" md="6" lg="6" xl="6">
        <v-card height="100%">
          <v-row class="ma-4 d-flex justify-center">
            <v-col
              cols="12"
              class="text-uppercase text-center"
              style="letter-spacing: 5px"
            >
              kalan kart sayısı</v-col
            >
            <v-col
              cols="12"
              sm="6"
              md="4"
              lg="3"
              xl="3"
              v-for="item in cards"
              :key="item"
              class="text-center"
            >
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
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
export default {
  data() {
    return {
      valueData: [] as any,
      valueRivalData: [] as any,
      value: "" as string,
      valueRival: "" as string,
      cards: [
        { item: "A", count: 4, numbValue: 1 || 11 },
        { item: "2", count: 4, numbValue: 2 },
        { item: "3", count: 4, numbValue: 3 },
        { item: "4", count: 4, numbValue: 4 },
        { item: "5", count: 4, numbValue: 5 },
        { item: "6", count: 4, numbValue: 6 },
        { item: "7", count: 4, numbValue: 7 },
        { item: "8", count: 4, numbValue: 8 },
        { item: "9", count: 4, numbValue: 9 },
        { item: "10", count: 4, numbValue: 10 },
        { item: "J", count: 4, numbValue: 10 },
        { item: "Q", count: 4, numbValue: 10 },
        { item: "K", count: 4, numbValue: 10 },
      ] as any,
    };
  },
  methods: {
    valueCount(value: string) {
      this.cards
        .filter((x: any) => x.item == value)
        .map((x: any) => {
          if (x.count == 0) {
            x.count == 0;
          } else {
            x.count--;
            this.valueData.push(x.numbValue);
          }
        });
      this.$refs.valueReset.reset();
    },
    valueCountRival(value: string) {
      this.cards
        .filter((x: any) => x.item == value)
        .map((x: any) => {
          if (x.count == 0) {
            x.count == 0;
          } else {
            x.count--;
            this.valueRivalData.push(x.numbValue);
          }
        });
      this.$refs.valueRivalReset.reset();
    },
    calculate(): any {
      let valueTotal: number = 0;
      let valueRivalTotal: number = 0;
      this.valueData.map((x: number) => (valueTotal += x));
      this.valueRivalData.map((x: number) => (valueRivalTotal += x));
      console.log(valueTotal);
      this.valueData
        .filter((x: any) => x.numbValue + valueTotal == 21)
        .map((x: any) => console.log(x));
      console.log(valueRivalTotal);
    },
  },
};
</script>
