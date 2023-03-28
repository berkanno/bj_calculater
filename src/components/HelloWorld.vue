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
                <v-col cols="12" class="text-center text-overline">
                  <v-row class="text-overline">
                    <v-col cols="6" v-for="item in resultValue" :key="item">
                      <v-row v-show="item.possiblity != 0">
                        <v-col
                          cols="6"
                          class="text-uppercase"
                          style="letter-spacing: 5px"
                          >{{ item.title }}</v-col
                        >
                        <v-col cols="6">% {{ item.possiblity }}</v-col>
                      </v-row>
                    </v-col>
                  </v-row>
                </v-col>
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
import { stringify } from "querystring";
export default {
  data() {
    return {
      lastValue: "" as String,
      totalCount: 0 as any,
      resultValue: [
        {
          title: "21 gelme olasılığı",
          count: 0 as any,
          possiblity: 0 as any,
          value: 21 as any,
        },
        {
          title: "20 gelme olasılığı",
          count: 0 as any,
          possiblity: 0 as any,
          value: 20 as any,
        },
        {
          title: "19 gelme olasılığı",
          count: 0 as any,
          possiblity: 0 as any,
          value: 19 as any,
        },
        {
          title: "18 gelme olasılığı",
          count: 0 as any,
          possiblity: 0 as any,
          value: 18 as any,
        },
        {
          title: "17 gelme olasılığı",
          count: 0 as any,
          possiblity: 0 as any,
          value: 17 as any,
        },
        {
          title: "16 gelme olasılığı",
          count: 0 as any,
          possiblity: 0 as any,
          value: 16 as any,
        },
        {
          title: "21_20 gelme olasılığı",
          count: 0 as any,
          possiblity: 0 as any,
          value: 2 as any,
        },
        {
          title: "21_19 gelme olasılığı",
          count: 0 as any,
          possiblity: 0 as any,
          value: 3 as any,
        },
        {
          title: "21_18 gelme olasılığı",
          count: 0 as any,
          possiblity: 0 as any,
          value: 4 as any,
        },
        {
          title: "21_17 gelme olasılığı",
          count: 0 as any,
          possiblity: 0 as any,
          value: 5 as any,
        },
        {
          title: "21_16 gelme olasılığı",
          count: 0 as any,
          possiblity: 0 as any,
          value: 6 as any,
        },
      ] as any,
      valueData: [] as any,
      valueRivalData: [] as any,
      value: "" as string,
      valueRival: "" as string,
      cards: [
        { item: "A", count: 4, numbValue: 1 },
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
      if (value !== "A") {
        console.log(typeof value);
        this.cards
          .filter((x: any) => x.item == value)
          .map((x: any) => {
            if (x.count == 0) {
              x.count == 0;
            } else {
              x.count--;
              this.lastValue = x.item;
              this.valueData.push(x.numbValue);
            }
          });
      } else if (value == "A") {
        this.cards
          .filter((x: any) => x.item == value)
          .map((x: any) => {
            if (x.count == 0) {
              x.count = 0;
            } else {
              x.count--;
              if (this.lastValue == "10") {
                console.log(x.count);
                this.valueData.push(11);
              } else if (this.lastValue == String(2)) {
                console.log("çalı");
                this.valueData.push(1);
              }
            }
          });
      }
      (this.$refs.valueReset as InstanceType<any>).reset();
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
      (this.$refs.valueRivalReset as InstanceType<any>).reset();
    },
    calculate(): any {
      console.log("çalıştı");
      let valueTotal: number = 0;
      let valueRivalTotal: number = 0;
      this.valueData.map((x: number) => (valueTotal += x));
      this.valueRivalData.map((x: number) => (valueRivalTotal += x));
      this.cards.map((x: any) => (this.totalCount += x.count));
      if (valueTotal == 9 || 10) {
        this.cards
          .filter((x: any) => x.item == "A")
          .map((x: any) => (x.numbValue = 11));
      } else {
        this.cards
          .filter((x: any) => x.item == "A")
          .map((x: any) => (x.numbValue = 1));
      }
      for (let i = 0; i < 6; i++) {
        this.cards
          .filter(
            (x: any) => x.numbValue == this.resultValue[i].value - valueTotal
          )
          .map((x: any) => {
            this.resultValue[i].count = x.count;
            this.resultValue[i].possiblity = Math.ceil(
              (this.resultValue[i].count / this.totalCount) * 100
            );
          });
      }
      for (let n = 6; n < this.resultValue.length; n++) {
        for (let i = 0; i < this.resultValue[n].value; i++) {
          this.resultValue[n].count += this.resultValue[i].count;
        }
        this.resultValue[n].possiblity = Math.ceil(
          (this.resultValue[n].count / this.totalCount) * 100
        );
      }

      console.log(this.resultValue);
    },
  },
};
</script>
