<template>
  <div class="container-fluid d-flex px-0" style="height: 100vh">
    <div class="first-div right-border">
      <input v-debounce:500="checkData" v-model="data" type="number" />
    </div>
    <div class="second-div right-border">
      <select v-model="option">
        <option value="primeNumber">isPrime</option>
        <option value="fiboNumber">IsFibanacci</option>
      </select>
    </div>
    <div class="third-div right-border">
      {{ results || false }}
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      data: 0,
      option: "primeNumber",
    };
  },

  methods: {
    checkData() {
      if (this.data < 0) {
        this.data = 1;
      }
      if (typeof this.data !== "number") {
        this.data = Math.round(this.data);
      }
    },
    checkPrime() {
      let isPrime = true;
          if (this.data == 1) {
            return false;
          } else if (this.data > 1) {
            for (let count = 2; count < this.data; count++) {
              if (this.data % count == 0) {
                isPrime = false;
                break;
              }
            }
            if (isPrime) {
              return true;
            } else {
              return false;
            }
          }
    },
    checkFibo(number, first, next) {
      if (number === 0 || number === 1) {
        return true;
      }
      let nextNumber = first + next;
      if (nextNumber === number) {
        return true;
      } else if (nextNumber > number ) {
        return false;
      }
      //loop fuction()
      return this.checkFibo(number, next, nextNumber);
    },
  },
  computed: {
    results() {
      switch (this.option) {
        case "primeNumber":
          return this.checkPrime()
        case "fiboNumber":
         return this.checkFibo(this.data,0,1); 
      }
    
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
input[type="number"] {
  -moz-appearance: textfield;
}
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
.right-border {
  border-right: 1px solid;
}
.first-div {
  width: 200px;
}
.second-div {
  width: 100%;
}
.third-div {
  width: 300px;
}
</style>
