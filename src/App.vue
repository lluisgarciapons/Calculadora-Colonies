<template>
  <div id="app">
    <v-app>
      <v-container grid-list-md>
        <h1>Calculadora Colònies</h1>
        <v-form ref="form" v-model="valid">
          <v-layout row wrap>
            <v-flex xs12 md4>
              <v-text-field
                v-model.number="dies"
                type="number"
                label="Nombre de dies d'estada"
                append-outer-icon="mdi-add"
                @click:append-outer="increment"
                @click:prepend="decrement"
                :rules="[
                  (v) => (!isNaN(parseFloat(v)) && v > 0) || 'Obligatori',
                ]"
              ></v-text-field>
            </v-flex>

            <v-flex xs12 md4>
              <v-text-field
                v-model.number="infants"
                type="number"
                label="Nombre d'infants"
                append-outer-icon="mdi-add"
                @click:append-outer="increment"
                @click:prepend="decrement"
                :rules="[
                  (v) => (!isNaN(parseFloat(v)) && v > 0) || 'Obligatori',
                ]"
              ></v-text-field>
            </v-flex>

            <v-flex xs12 md4>
              <v-text-field
                v-model.number="monis"
                type="number"
                label="Nombre de monis"
                append-outer-icon="mdi-add"
                @click:append-outer="increment"
                @click:prepend="decrement"
                :rules="[
                  (v) => (!isNaN(parseFloat(v)) && v > 0) || 'Obligatori',
                ]"
              ></v-text-field>
            </v-flex>
          </v-layout>

          <v-expansion-panels class="mb-5">
            <v-expansion-panel>
              <v-expansion-panel-header
                >Opcions avançades</v-expansion-panel-header
              >
              <v-expansion-panel-content>
                <v-layout row wrap justify-center>
                  <v-flex xs12 sm4 md4>
                    <v-checkbox
                      v-model="checkbox"
                      label="Estada de moni gratuïta per nombre d'infants?"
                    ></v-checkbox>
                  </v-flex>
                  <v-flex xs12 sm4>
                    <v-text-field
                      :disabled="!checkbox"
                      v-model="llindar"
                      type="number"
                      hint="Si és així, quants infants necessaris per conseguir una estada gratuïta?"
                      persistent-hint
                      append-outer-icon="mdi-add"
                      @click:append-outer="increment"
                      @click:prepend="decrement"
                    >
                      <v-tooltip slot="append" top>
                        <template v-slot:activator="{ on }">
                          <v-icon v-on="on" color="primary" dark
                            >mdi-help-circle-outline</v-icon
                          >
                        </template>
                        <span
                          >Algunes cases ofereixen l'estada d'un monitor
                          gratuïta depenent del nombre d'infants</span
                        >
                      </v-tooltip>
                    </v-text-field>
                  </v-flex>
                </v-layout>

                <v-layout row wrap>
                  <v-flex xs12 sm4 md3>
                    <v-text-field
                      v-model.number="preuPersonaDia"
                      type="number"
                      label="Preu persona/dia"
                      prepend-icon="mdi-currency-eur"
                      append-outer-icon="mdi-add"
                      @click:append-outer="increment"
                      @click:prepend="decrement"
                      :rules="[
                        (v) =>
                          (!isNaN(parseFloat(v)) && v >= 0) || 'Obligatori',
                      ]"
                    >
                      <v-tooltip slot="append" top>
                        <template v-slot:activator="{ on }">
                          <v-icon v-on="on" color="primary" dark
                            >mdi-help-circle-outline</v-icon
                          >
                        </template>
                        <span
                          >Preu Pensió Completa per persona per un dia
                          d'estada</span
                        >
                      </v-tooltip>
                    </v-text-field>
                  </v-flex>

                  <v-flex xs12 sm4 md3>
                    <v-text-field
                      v-model.number="pctIns"
                      type="number"
                      label="percentatge % afegit"
                      prepend-icon="mdi-percent-outline"
                      append-outer-icon="mdi-add"
                      @click:append-outer="increment"
                      @click:prepend="decrement"
                      :rules="[
                        (v) =>
                          (!isNaN(parseFloat(v)) && v >= 0 && v <= 100) ||
                          'Obligatori entre 0 i 100',
                      ]"
                    >
                      <v-tooltip slot="append" top>
                        <template v-slot:activator="{ on }">
                          <v-icon v-on="on" color="primary" dark
                            >mdi-help-circle-outline</v-icon
                          >
                        </template>
                        <span
                          >Percentatge del preu de l'estada de l'infant que
                          s'afegeix al total per cobrir qualsevol
                          imprevist</span
                        >
                      </v-tooltip>
                    </v-text-field>
                  </v-flex>
                  <v-flex xs12 sm4 md3>
                    <v-text-field
                      v-model.number="gastosMaterial"
                      type="number"
                      label="Gastos Material per l'esplai"
                      prepend-icon="mdi-currency-eur"
                      append-outer-icon="mdi-add"
                      @click:append-outer="increment"
                      @click:prepend="decrement"
                      :rules="[
                        (v) =>
                          (!isNaN(parseFloat(v)) && v >= 0) || 'Obligatori',
                      ]"
                    >
                      <v-tooltip slot="append" top>
                        <template v-slot:activator="{ on }">
                          <v-icon v-on="on" color="primary" dark
                            >mdi-help-circle-outline</v-icon
                          >
                        </template>
                        <span
                          >Cost estimat del material necessari per les
                          colònies</span
                        >
                      </v-tooltip>
                    </v-text-field>
                  </v-flex>

                  <v-flex xs12 sm4 md3>
                    <v-text-field
                      v-model.number="materialBaseInfant"
                      type="number"
                      label="Preu Material per infant"
                      prepend-icon="mdi-currency-eur"
                      append-outer-icon="mdi-add"
                      @click:append-outer="increment"
                      @click:prepend="decrement"
                      :rules="[
                        (v) =>
                          (!isNaN(parseFloat(v)) && v >= 0) || 'Obligatori',
                      ]"
                    >
                      <v-tooltip slot="append" top>
                        <template v-slot:activator="{ on }">
                          <v-icon v-on="on" color="primary" dark
                            >mdi-help-circle-outline</v-icon
                          >
                        </template>
                        <span
                          >Preu base destinat a material per cada infant</span
                        >
                      </v-tooltip>
                    </v-text-field>
                  </v-flex>
                  <v-flex xs12 sm4 md3>
                    <v-text-field
                      v-model.number="materialInfantDia"
                      type="number"
                      label="Preu Material infant/dia"
                      prepend-icon="mdi-currency-eur"
                      append-outer-icon="mdi-add"
                      @click:append-outer="increment"
                      @click:prepend="decrement"
                      :rules="[
                        (v) =>
                          (!isNaN(parseFloat(v)) && v >= 0) || 'Obligatori',
                      ]"
                    >
                      <v-tooltip slot="append" top>
                        <template v-slot:activator="{ on }">
                          <v-icon v-on="on" color="primary" dark
                            >mdi-help-circle-outline</v-icon
                          >
                        </template>
                        <span
                          >Preu destinat a material per cada infant per cada dia
                          d'estada</span
                        >
                      </v-tooltip>
                    </v-text-field>
                  </v-flex>
                  <v-flex xs12 sm4 md3>
                    <v-text-field
                      v-model.number="devolucioIns"
                      type="number"
                      label="Retorn Inscripció"
                      prepend-icon="mdi-currency-eur"
                      append-outer-icon="mdi-add"
                      @click:append-outer="increment"
                      @click:prepend="decrement"
                      :rules="[
                        (v) =>
                          (!isNaN(parseFloat(v)) && v >= 0) || 'Obligatori',
                      ]"
                    >
                      <v-tooltip slot="append" top>
                        <template v-slot:activator="{ on }">
                          <v-icon v-on="on" color="primary" dark
                            >mdi-help-circle-outline</v-icon
                          >
                        </template>
                        <span
                          >Quantitat retornada famílies i llars per infant per
                          no haver pogut acabar el curs 19-20</span
                        >
                      </v-tooltip>
                    </v-text-field>
                  </v-flex>

                  <v-flex xs12 sm4 md3>
                    <v-text-field
                      v-model.number="pctMoni"
                      type="number"
                      label="A pagar per moni"
                      prepend-icon="mdi-percent-outline"
                      append-outer-icon="mdi-add"
                      @click:append-outer="increment"
                      @click:prepend="decrement"
                      :rules="[
                        (v) =>
                          (!isNaN(parseFloat(v)) && v >= 0 && v <= 100) ||
                          'Obligatori entre 0 i 100',
                      ]"
                    >
                      <v-tooltip slot="append" top>
                        <template v-slot:activator="{ on }">
                          <v-icon v-on="on" color="primary" dark
                            >mdi-help-circle-outline</v-icon
                          >
                        </template>
                        <span
                          >percentatge (0-100) del cost de l'estada a pagar per
                          cada moni, on 0 és gratis i 100 paga la
                          totalitat</span
                        >
                      </v-tooltip>
                    </v-text-field>
                  </v-flex>
                </v-layout>
              </v-expansion-panel-content>
            </v-expansion-panel>
          </v-expansion-panels>
          <v-btn
            :disabled="!valid"
            color="success"
            class="mr-4"
            @click="validate"
            >Calcula</v-btn
          >

          <!-- <v-btn color="error" class="mr-4" @click="reset">Reset Formulari</v-btn> -->
        </v-form>

        <v-timeline
          v-if="balancTotal"
          align-top
          :dense="$vuetify.breakpoint.smAndDown"
        >
          <v-timeline-item color="green lighten-2">
            <v-card color="green lighten-2" dark class="text-center">
              <v-card-title class="title">Preu per Infant</v-card-title>
              <v-card-text class="white text--primary">
                <p class="resultat">{{ preuPerInfant }}€</p>
              </v-card-text>
            </v-card>
          </v-timeline-item>

          <v-timeline-item color="green lighten-2">
            <v-card color="green lighten-2" dark class="text-center">
              <v-card-title class="title">A pagar cada Moni</v-card-title>
              <v-card-text class="white text--primary">
                <p class="resultat">{{ aPagarPerMoni }}€</p>
              </v-card-text>
            </v-card>
          </v-timeline-item>

          <v-timeline-item color="green lighten-2">
            <v-card color="green lighten-2" dark class="text-center">
              <v-card-title class="title">Balanç Total</v-card-title>
              <v-card-text class="white text--primary">
                <p
                  v-bind:class="[
                    balancTotal > 0
                      ? 'green--text text--darken-2'
                      : 'red--text text--darken-2',
                    'resultat',
                  ]"
                >
                  {{ balancTotal }}€
                </p>
              </v-card-text>
            </v-card>
          </v-timeline-item>
        </v-timeline>
      </v-container>
    </v-app>
  </div>
</template>

<script>
export default {
  name: "App",

  data: () => {
    return {
      valid: false,
      dies: null,
      infants: null,
      monis: null,
      checkbox: false,
      llindar: 15,
      preuPersonaDia: 30.3,
      pctIns: 10,
      gastosMaterial: 100,
      materialBaseInfant: 5,
      materialInfantDia: 1,
      devolucioIns: 0,
      pctMoni: 0,

      balancTotal: null,
      ingressosTotals: null,
      aPagarPerMoni: null,
      preuPerInfant: null,
    };
  },

  methods: {
    validate() {
      console.log(this.balanc());
    },
    reset() {
      // this.$refs.form.reset();
      console.log(this.tust);
    },
    increment() {
      this.foo = parseInt(this.foo, 10) + 1;
    },
    decrement() {
      this.foo = parseInt(this.foo, 10) - 1;
    },
    gastos() {
      let preuCasa =
        (this.infants + this.calculMonis()) * this.dies * this.preuPersonaDia;
      return Number((preuCasa + this.gastosMaterial).toFixed(2));
    },

    ingressos() {
      let pagamentPerInfant =
        ((this.preuPersonaDia + this.materialInfantDia) * this.dies +
          this.materialBaseInfant) *
          ((100 + this.pctIns) / 100) -
        this.devolucioIns;
      this.preuPerInfant = pagamentPerInfant.toFixed(2);
      return pagamentPerInfant * this.infants;
    },
    calculMonis() {
      let reduccio = Math.floor(this.infants / this.llindar);
      return this.monis - reduccio;
    },

    preuPerMoni() {
      let preu =
        (this.preuPersonaDia * this.dies * this.calculMonis()) / this.monis;
      return preu * (this.pctMoni / 100);
    },

    aPagarMonis() {
      this.aPagarPerMoni = this.preuPerMoni().toFixed(2);
      return this.preuPerMoni() * this.monis;
    },

    balanc() {
      this.ingressosTotals = this.ingressos().toFixed(2);
      this.gastosTotals = this.gastos().toFixed(2);
      this.balancTotal = (
        this.ingressos() +
        this.aPagarMonis() -
        this.gastos()
      ).toFixed(2);
    },
  },
};
</script>

<style>
.resultat {
  font-weight: bold;
  font-size: 30px;
  padding-top: 16px;
}

.green {
  color: #388e3c;
}

.red {
  color: #d32f2f;
}
</style>