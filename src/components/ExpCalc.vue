<template>
      <div class="relative bg-[#251B37] px-6 pt-10 pb-8 shadow-xl ring-1 ring-gray-900/5 sm:mx-auto sm:max-w-lg sm:rounded-lg sm:px-10">
        <div class="mx-auto max-w-md border-double">
          <div class="text-right p-2 my-2 bg-[#372948] text-white rounded-lg">
            Total: {{ total || 0 }}
          </div>
          <div class="p-1 grid grid-cols-4 gap-2 bg-[#372948] rounded-lg">
            <button
              v-for="(value, name) in ultras"
              :key="name"
              @click="action(value, name)"
              class="bg-[#FFCACA] col-3 rounded-lg text-black hover:bg-[#372948]"
              :class="{
                'bg-green-300': ['Clear', 'Minus'].includes(name),
                'bg-orange-500': ['Trio', 'Dailies', 'Weeklies', 'All Ultras'].includes(name),
              }"
            >
              {{ name }}
            </button>
          </div>
          <div
            class="text-right p-2 my-2 bg-[#372948] text-white rounded-lg break-all"
          >
            {{ exp || "Values shown here" }}
          </div>
          <div
            class="text-right p-2 my-2 bg-[#372948] text-green-500 rounded-lg break-all"
          >
            {{ ultraSTR || "Ultras Shown Here" }}
          </div>
        </div>
      </div>
  </template>
  
  <script>
  /* eslint-disable */
  export default {
    name: "ExpCalc",
    mounted() {
      document.title = "Exp Calculator";
          },
  
    data() {
      return {
        exp: '',
        operator: '+',
        total: '',
        ultraSTR: '',
        ultras: {
                  "Dage":6000,
                  "Darkon":8000,
                  "Drakath":6000,
                  "Nulgath":4000,
                  "Drago":2500,
                  "Tyndarius":2000,
                  "Engineer":2000,
                  "Warden":2000,
                  "Ezrajal":2000,
                  "VA Daily":2500,
                  "Trio":6000,
                  "Minus":"-",
                  "Dailies":8000,
                  "Weeklies":26500,
                  "All Ultras":34500,
                  "Clear": "c"
                },
      }
    },
    methods: {
      action(n, name) {
        if (!['c','-'].includes(n)) {
          if (this.ultraSTR == '') {
            this.ultraSTR = name;
            this.exp = n;
          } else {
            this.ultraSTR = this.ultraSTR + this.operator + name;  
            this.exp = this.exp + this.operator + n;
          }
          this.total = eval(this.exp);
        }
        if (n == "c") {
          this.exp='';
          this.ultraSTR='';
          this.total='';  
        }
        if (n == "-") {
          this.exp = this.exp + n;
          this.ultraSTR = this.ultraSTR + n;
        }
        /* Prevents operator signs to Concatenate */
        if ((this.exp).includes("--")) {
          this.exp = (this.exp).replace("--", "-");
          this.ultraSTR = (this.ultraSTR).replace("--", "-");
        }
        if ((this.exp).includes("-+")) {
          this.exp = (this.exp).replace("-+", "-");
          this.ultraSTR = (this.ultraSTR).replace("-+", "-");
        }
      }
    },
  };
  </script>
  