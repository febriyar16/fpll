<template>
  <div id="app">
    <header>
      <h1>Konverter Suhu</h1>
    </header>

    <main>
      <div class="converter">
        <h2>Suhu Converter</h2>
        <div class="input-container">
          <input type="number" v-model="inputValue" placeholder="Masukkan suhu">
          <select v-model="inputUnit">
            <option value="c">°C (Celcius)</option>
            <option value="f">°F (Fahrenheit)</option>
            <option value="k">K (Kelvin)</option>
          </select>
        </div>
        <div class="output">
          <h3>Hasil:</h3>
          <ul>
            <li v-for="(value, unit) in result" :key="unit">{{ value }} {{ unit }}</li>
          </ul>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputValue: '',
      inputUnit: 'c',
    };
  },
  computed: {
    result() {
      return this.convertTemperature(this.inputValue, this.inputUnit);
    },
  },
  methods: {
    convertTemperature(value, unit) {
      switch (unit) {
        case 'c':
          return this.convertFromCelsius(value);
        case 'f':
          return this.convertFromFahrenheit(value);
        case 'k':
          return this.convertFromKelvin(value);
        default:
          return {};
      }
    },
    convertFromCelsius(value) {
      return {
        'Fahrenheit': (value * 9/5) + 32,
        'Kelvin': value + 273.15
      };
    },
    convertFromFahrenheit(value) {
      return {
        'Celsius': (value - 32) * 5/9,
        'Kelvin': (value - 32) * 5/9 + 273.15
      };
    },
    convertFromKelvin(value) {
      return {
        'Celsius': value - 273.15,
        'Fahrenheit': (value - 273.15) * 9/5 + 32
      };
    },
  },
};
</script>

<style scoped>
header {
  text-align: center;
  margin-bottom: 20px;
  font-family: 'Poppins', sans-serif;
  color: #fff; /* Warna teks putih */
}

h1 {
  margin: 0;
}

#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background-color: #2196F3; /* Warna biru muda */
}

.converter {
  max-width: 400px;
  padding: 20px;
  background-color: #fff; /* Warna latar belakang putih */
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  font-family: 'Poppins', sans-serif;
}

.converter h2 {
  margin-top: 0;
}

.input-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 20px;
}

input,
select {
  width: 100%;
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #ccc;
  margin-bottom: 10px;
}

.output {
  text-align: center;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  font-size: 18px;
  margin-bottom: 5px;
}
</style>
