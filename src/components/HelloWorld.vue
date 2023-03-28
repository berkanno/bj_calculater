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
                    <v-col v-show="value21 != 0" cols="6">
                      <v-row>
                        <v-col
                          cols="6"
                          class="text-uppercase"
                          style="letter-spacing: 5px"
                          >21 gelme olasılığı:</v-col
                        >
                        <v-col cols="6">%{{ possiblityValue21 }}</v-col>
                      </v-row>
                    </v-col>
                    <v-col v-show="value20 != 0" cols="6">
                      <v-row>
                        <v-col
                          cols="6"
                          class="text-uppercase"
                          style="letter-spacing: 5px"
                          >20 gelme olasılığı:</v-col
                        >
                        <v-col cols="6">%{{ value20 }}</v-col>
                      </v-row>
                    </v-col>

                    <v-col v-show="value19 != 0" cols="6">
                      <v-row>
                        <v-col
                          cols="6"
                          class="text-uppercase"
                          style="letter-spacing: 5px"
                          >19 gelme olasılığı:</v-col
                        >
                        <v-col cols="6">%{{ value19 }}</v-col>
                      </v-row>
                    </v-col>
                    <v-col v-show="value18 != 0" cols="6">
                      <v-row>
                        <v-col
                          cols="6"
                          class="text-uppercase"
                          style="letter-spacing: 5px"
                          >18 gelme olasılığı:</v-col
                        >
                        <v-col cols="6">%{{ value18 }}</v-col>
                      </v-row>
                    </v-col>
                    <v-col v-show="value17 != 0" cols="6">
                      <v-row>
                        <v-col
                          cols="6"
                          class="text-uppercase"
                          style="letter-spacing: 5px"
                          >17 gelme olasılığı:</v-col
                        >
                        <v-col cols="6">%{{ value17 }}</v-col>
                      </v-row>
                    </v-col>
                    <v-col v-show="value16 != 0" cols="6">
                      <v-row>
                        <v-col
                          cols="6"
                          class="text-uppercase"
                          style="letter-spacing: 5px"
                          >16 gelme olasılığı:</v-col
                        >
                        <v-col cols="6">%{{ value16 }}</v-col>
                      </v-row>
                    </v-col>
                    <v-col v-show="value16 != 0" cols="6">
                      <v-row>
                        <v-col
                          cols="6"
                          class="text-uppercase"
                          style="letter-spacing: 5px"
                          >16 gelme olasılığı:</v-col
                        >
                        <v-col cols="6">%{{ value16 }}</v-col>
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
export default {
  data() {
    return {
      lastValue: "" as String,
      totalCount: 0 as any,
      value21: 0 as any,
      value20: 0 as any,
      value19: 0 as any,
      value18: 0 as any,
      value17: 0 as any,
      value16: 0 as any,
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
              if (this.lastValue == "10" || "K" || "Q" || "J" || "9") {
                this.valueData.push(11);
                alert("BLACKJACK!! TEBRİKLERR");
              } else if (
                this.lastValue == "A" ||
                "2" ||
                "3" ||
                "4" ||
                "5" ||
                "6" ||
                "7" ||
                "8"
              ) {
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

      this.cards
        .filter((x: any) => x.numbValue == 21 - valueTotal)
        .map((x: any) => {
          this.value21 += x.count;
          const possiblityValue21 = Math.ceil(
            (this.value21 / this.totalCount) * 100
          );
        }),
        this.cards
          .filter((x: any) => x.numbValue == 20 - valueTotal)
          .map((x: any) => {
            this.value20 += x.count;
            const possiblityValue20 = Math.ceil(
              (this.value20 / this.totalCount) * 100
            );
          }),
        this.cards
          .filter((x: any) => x.numbValue == 19 - valueTotal)
          .map((x: any) => {
            this.value19 += x.count;
            const possiblityValue19 = Math.ceil(
              (this.value19 / this.totalCount) * 100
            );
          }),
        this.cards
          .filter((x: any) => x.numbValue == 18 - valueTotal)
          .map((x: any) => {
            this.value18 += x.count;
            const possiblityValue18 = Math.ceil(
              (this.value18 / this.totalCount) * 100
            );
          }),
        this.cards
          .filter((x: any) => x.numbValue == 17 - valueTotal)
          .map((x: any) => {
            this.value17 += x.count;
            const possiblityValue17 = Math.ceil(
              (this.value17 / this.totalCount) * 100
            );
          }),
        this.cards
          .filter((x: any) => x.numbValue == 16 - valueTotal)
          .map((x: any) => {
            this.value16 += x.count;
            const possiblityValue16 = Math.ceil(
              (this.value16 / this.totalCount) * 100
            );
          });
      const possiblityValue21_19 = Math.ceil(
        ((this.value21 + this.value20 + this.value19) / this.totalCount) * 100
      );
      const possiblityValue21_18 = Math.ceil(
        ((this.value21 + this.value20 + this.value19 + this.value18) /
          this.totalCount) *
          100
      );
      const possiblityValue21_17 = Math.ceil(
        ((this.value21 +
          this.value20 +
          this.value19 +
          this.value18 +
          this.value17) /
          this.totalCount) *
          100
      );
      const possiblityValue21_16 = Math.ceil(
        ((this.value21 +
          this.value20 +
          this.value19 +
          this.value18 +
          this.value17 +
          this.value16) /
          this.totalCount) *
          100
      );
    },
  },
};
</script>
