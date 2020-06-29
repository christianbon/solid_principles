<template>
  <div class="px-3 py-4 reportContainer">
    <v-chip color="secondary" dark small class="chips" px-3
      >Area and Volume Calculator</v-chip
    >
    Code with DRY KISS implementation
    <!-- Option -->
    <v-layout row align-center>
      <v-flex xs2 class="text-xs-left" px-3>Shape</v-flex>
      <v-flex xs10>
        <v-radio-group
          id="calculatorType"
          v-model="calculatorType"
          validate-on-blur
          row
        >
          <v-radio id="square"  label="square area" value="square"></v-radio>
          <v-radio id="rectangle" label="rectangle" value="rectangle"></v-radio>
          <v-radio id="triangle" label="triangle" value="triangle"></v-radio>
          <v-radio id="circle" label="circle" value="circle"></v-radio>
          <v-radio id="squarePrism" label="square prism" value="squarePrism"></v-radio>
          <v-radio id="trianglePrism" label="triangle prism" value="trianglePrism"></v-radio>
          <v-radio id="cylinder" label="cylinder" value="cylinder"></v-radio>
        </v-radio-group>
      </v-flex>
    </v-layout>
    <!-- Panjang -->
    <v-layout v-if="butuhPanjang" row align-center>
      <v-flex xs2 class="text-xs-left" px-3>Panjang</v-flex>
      <v-flex xs10>
        <v-text-field
          id="panjang"
          v-model="panjang"
          label="Panjang"
          validate-on-blur
        ></v-text-field>
      </v-flex>
    </v-layout>
    <!-- Lebar -->
    <v-layout v-if="butuhLebar" row align-center>
      <v-flex xs2 class="text-xs-left" px-3>lebar</v-flex>
      <v-flex xs10>
        <v-text-field
          id="lebar"
          v-model="lebar"
          label="Lebar"
          validate-on-blur
        ></v-text-field>
      </v-flex>
    </v-layout>
    <!-- Tinggi -->
    <v-layout v-if="butuhTinggi" row align-center>
      <v-flex xs2 class="text-xs-left" px-3>Tinggi</v-flex>
      <v-flex xs10>
        <v-text-field
          id="tinggi"
          v-model="tinggi"
          label="Tinggi"
          validate-on-blur
        ></v-text-field>
      </v-flex>
    </v-layout>
    <!-- Diameter -->
    <v-layout v-if="butuhDiameter" row align-center>
      <v-flex xs2 class="text-xs-left" px-3>Diameter</v-flex>
      <v-flex xs10>
        <v-text-field
          id="diameter"
          v-model="diameter"
          label="Diameter"
          validate-on-blur
        ></v-text-field>
      </v-flex>
    </v-layout>
    <br>
    <br>
    <!-- Submit -->
    <v-layout row align-center>
      <v-flex xs2 class="text-xs-left" px-3>Hasil: </v-flex>
      <v-flex xs2 class="text-xs-left" px-3> {{ result }} </v-flex>
    </v-layout>
    <v-layout row align-center>
      <v-flex xs12>
        <v-btn
          id="calculate"
          @click="calculate()"
          color="primary"
          block
          >Hitung</v-btn
        >
      </v-flex>
    </v-layout>
  </div>
</template>

<script>

export default {
  // DRY & KISS PRINCIPLE
  // 1. Semua methods kurang dari 50 baris
  // 2. Tidak ada code yang berulang
  // 3. Re-use method or component
  data(){
    return {
      calculatorType: 'square',
      result: '',
      panjang: '',
      lebar: '',
      tinggi: '',
      diameter: '',
      pi: 3.14,
      // Edit here to add more variables and input type
      // This code below is prepared for extension
      panjangList: [
        'square',
        'rectangle',
        'triangle',
        'squarePrism',
        'trianglePrism'
      ],
      lebarList: [
        'square',
        'rectangle',
        'squarePrism',
        'trianglePrism'
      ],
      tinggiList: [
        'triangle',
        'squarePrism',
        'trianglePrism',
        'cylinder'
      ],
      diameterList: [
        'circle',
        'cylinder'
      ]
    }
  },
  computed: {
    butuhPanjang: {
      get() {
        if(this.panjangList.indexOf(this.calculatorType) > -1){
          return true
        }
        return false
      },
    },
    butuhLebar: {
      get() {
        if(this.lebarList.indexOf(this.calculatorType) > -1){
          return true
        }
        return false
      },
    },
    butuhTinggi: {
      get() {
        if(this.tinggiList.indexOf(this.calculatorType) > -1){
          return true
        }
        return false
      },
    },
    butuhDiameter: {
      get() {
        if(this.diameterList.indexOf(this.calculatorType) > -1){
          return true
        }
        return false
      },
    }
  },
  methods: {
    resetState(){
      // Reset state
      this.panjang =  '',
      this.lebar = '',
      this.tinggi = '',
      this.diameter = ''
    },
    squareArea(){
      this.result = this.panjang * this.lebar
    },
    triangleArea(){
      this.result = 1/2 * this.panjang * this.lebar
    },
    circleArea(){
      this.result = this.pi * ((this.diameter/2)**2)
    },
    prismVolume(){
      this.result = this.result * this.tinggi
    },
    calculate(){
      if(this.calculatorType === 'square' || this.calculatorType === 'rectangle'){
        this.squareArea()
      }else if(this.calculatorType === 'triangle'){
        this.triangleArea()
      }else if(this.calculatorType === 'circle'){
        this.circleArea() 
      }else if(this.calculatorType === 'prismSquare'){
        // re-use code (DRY)
        this.squareArea()
        this.prismVolume()
      }else if(this.calculatorType === 'triangleSquare'){
        // re-use code (DRY)
        this.triangleArea()
        this.prismVolume()
      }else if(this.calculatorType === 'cylinder'){
        // re-use code (DRY)
        this.circleArea()
        this.prismVolume()
      }
      this.resetState()
    }
  }
}
</script>
