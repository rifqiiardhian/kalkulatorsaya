<template>
  <div class = "body">
    <h2>KALKULATOR SEDERHANA SAYA</h2>
    <div class = "interface-number">{{hasil || '0'}}</div>
    <div @click ="append('1')" class = "btn">1</div>
    <div @click ="append('2')" class = "btn">2</div>
    <div @click ="append('3')" class = "btn">3</div>
    <div @click = 'clear' class = "btn operator">C</div>
    <div @click = 'tambah' class = "btn operator">+</div>
    <div @click = 'sin' class = "btn operator">sin</div>
    <div @click ="append('4')" class = "btn">4</div>
    <div @click ="append('5')" class = "btn">5</div>
    <div @click ="append('6')" class = "btn">6</div>
    <div @click = 'tanda' class = "btn operator">+/-</div>
    <div @click = 'kurang' class = "btn operator">-</div>
    <div @click = 'cos' class = "btn operator">cos</div>
    <div @click ="append('7')" class = "btn">7</div>
    <div @click ="append('8')" class = "btn">8</div>
    <div @click ="append('9')" class = "btn">9</div>
    <div @click = 'persen' class = "btn operator">%</div>
    <div @click = 'kali' class = "btn operator">x</div>
    <div @click = 'tan' class = "btn operator">tan</div>
    <div @click ="append('0')" class = "btn nol">0</div>
    <div @click = 'dot' class = "btn">•</div>
    <div @click = 'samadengan' class = "btn operator">=</div>
    <div @click = 'bagi' class = "btn operator">:</div>
    <div @click = 'akar' class = "btn operator">√</div>
    <p>&copy; 2020 Created by Rifqi Ardhian</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      hasil: '',
      operator: null,
      operatorClicked: false,
    };
  },
  methods: {
    clear() {
      this.hasil = '';
    },
    tanda() {
      this.hasil = this.hasil.charAt(0) === '-' ? this.hasil.slice(1) : `-${this.hasil}`;
    },
    persen() {
      this.hasil = `${parseFloat(this.hasil) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.hasil = '';
        this.operatorClicked = false;
      }
      this.hasil = `${this.hasil}${number}`;
    },
    dot() {
      if (this.hasil.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.hasil;
      this.operatorClicked = true;
    },
    tambah() {
      this.operator = (x, y) => x + y;
      this.setPrevious();
    },
    kurang() {
      this.operator = (x, y) => y - x;
      this.setPrevious();
    },
    kali() {
      this.operator = (x, y) => x * y;
      this.setPrevious();
    },
    bagi() {
      this.operator = (x, y) => y / x;
      this.setPrevious();
    },
    samadengan() {
      this.hasil = `${this.operator(parseFloat(this.hasil), parseFloat(this.previous))}`;
      this.previous = null;
    },
    sin() {
      this.hasil = `${Math.sin(parseFloat(this.hasil))}`;
    },
    cos() {
      this.hasil = `${Math.cos(parseFloat(this.hasil))}`;
    },
    tan() {
      this.hasil = `${Math.tan(parseFloat(this.hasil))}`;
    },
    akar() {
      this.hasil = `${Math.sqrt(this.hasil)}`;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.body{
  width: 400px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
h2,p{
  grid-column: 1/7;
}
.interface-number{
  padding-top: 5px;
  grid-column: 1/7;
  background-color: #212121;
  color: whitesmoke;
  font-size: 30px;
  margin-right: 5px;
  margin-left: 5px;
  margin-bottom: 5px
}
.nol{
  grid-column: 1/3;
}
.btn{
  padding-top: 10px;
  background-color: #ededed;
  margin: 5px;
  border-radius: 5px
}
.operator{
  background-color: #cccccc;
}
.btn:hover{
  transition: all 0.3s ease;
  background: #6e6e6e;
  color: white
}
</style>
