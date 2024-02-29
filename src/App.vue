<script setup lang="ts">
import { ref, computed } from 'vue';
import dollar from './assets/icon-dollar.svg'
import person from './assets/icon-person.svg'
import logo from './assets/logo.svg'

const num = ref(0);
const people = ref(0);
const n = ref<any>(1);

const click = (x:any) => {
  n.value = x;
};

const clickComp = computed(() => {
  return Math.round(num.value * n.value);
});

const NumPeople = computed(() => {
  return clickComp.value * people.value;
});

const sumTipChange = computed(() => {
  return clickComp.value - num.value || 0;
});

const promptModal = () => {
  let proc :  string | null = prompt('Какой процент нужен?', 100);
  if (proc !== null) {n.value = proc / 100 + 1}else {n.value = 1}
};

const reset = () => {
  n.value = 0;
  people.value = 0;
  num.value = 0
};
</script>

<template>
  <div class='logo'>
    <img class='logoChild' :src='logo'/>
  </div>
  <div class="container">
    <div class="miniContainer">
      <div>
        <p class='text'>Bill</p>

        <div class='inp'>
          <img class='dollar' :src='dollar'/>
          <input type="text" class='inpChild' v-model="num" />
        </div>
      </div>

      <p class='text'>Select Tip %</p>
      <div class=tab>
        <button class='btnZ' @click="() => click(1.05)">5%</button>
        <button class='btnZ' @click="() => click(1.1)">10%</button>
        <button class='btnZ' @click="() => click(1.5)">15%</button>
        <button class='btnZ' @click="() => click(1.25)">25%</button>
        <button class='btnZ' @click="() => click(1.5)">50%</button>
        <button class='btnZ zz' @click="promptModal">Custom</button>
      </div>

      <div>
        <p class='text'>Number of people</p>
        
        <div class='inp'>
          <img class='dollar' :src='person'/>
          <input  type="text"   class='inpChild' v-model="people" />
        </div>
      </div>
    </div>
    <div class='mini'> 
      <div class='amount'>
        <div><span class='s'>Tip amount</span> <br> <span class='sp'>/ person</span></div>
        <div class='num'>${{ sumTipChange }}.00</div>
      </div>
      <div class='amount'>
        <div><span class='s'>Total</span> <br> <span class='sp'>/ person</span></div>
        <div class='num'>${{ clickComp }}.00</div>
      </div>
      <div class='amount'>
        <div><span class='s'>Total all</span></div>
        <div class='num'>${{ NumPeople }}.00</div>
      </div>

      <div class='btn'>
        <button @click='reset' class='miniBtn'>RESET</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
@import './style.css';


.container {
  font-family:'Space Mono',monospace;
  background-color: white;
  border-radius: 2%;
  padding:10px;
  margin:0 auto;
  width:60%;
  display: grid;
  grid-template-columns: 50% 50%;
}
.miniContainer {
  padding:10px
}
.mini{
  background-color: #00474B;
  border-radius:5%;
  padding:20px;
  position: relative;
}
.inp{
  margin:5px;
  position: relative;
}
.inpChild{
  border:0;
  width: stretch;
  width: -webkit-fill-available;
  height:30px;
  padding:5px;
  border-radius:2%;
  background-color:#e4e9ed;
  text-align:end;
  padding-right:15px;
  font-family:'Space Mono',monospace;
}
.tab{
  display:grid;
  grid-template-columns: 1fr 1fr 1fr;
}
.amount{
  display: flex;
  justify-content:space-between;
  align-items:center;
  color:white;
  margin-bottom:10px;
}
.btn{
  width:90%;
  position: absolute;
  bottom:10px;
}

.btnZ{
  border-radius:5%;
  background-color:#00474B;
  color:white;
  height:40px;
  margin:5px;
  cursor:pointer;
  font-size: 18px;
  font-weight:bold;
  font-family:'Space Mono',monospace;
}
.zz{
  background-color: #e4e9ed;
  color: #00474B;
  font-weight:bold;
  border:0;
  font-family:'Space Mono',monospace;
}
.miniBtn{
  width:100%;
  height:40px;
  border-radius:5%;
  background-color: #0D686D;
  border:0;
  cursor:pointer;
}
.miniBtn:hover{
  background-color:#9FE8DF;
}
.text{
  font-weight:bold;
  color: #677A7B;
  margin-top:25px;
  margin-bottom:10px;
  margin-left:5px;
  font-family:'Space Mono',monospace;
}
.dollar{
  position: absolute;
  top:50%;
  left:4%;
  transform:translate(-50%, -50%);
}
.num{
  font-size: 45px;
  color:green;
 font-weight:bold;
 font-family:'Space Mono',monospace;
}
.s{
  font-size:18px;
  word-spacing:4px;
  font-weight:bold;
  font-family:'Space Mono',monospace;

}
.sp{
  color:#609397;
  font-family:'Space Mono',monospace;
}
.logo{
  width:100%;
  display:flex;
  justify-content:center;
  margin-top:140px;
  margin-bottom:80px;
}
.logoChild{
  
}
</style>
