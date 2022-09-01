<template>
  <div class="row justify-content-center p-5" style="background-color: white; 
  margin-top: 5rem; margin-left: 1rem; margin-right:1rem;border-radius: 40px; 
  box-shadow: rgb(38, 57, 77) 0px 20px 30px -10px;">
    <div class="col-sm-12 col-md-8 ">
        <h2 class="text-center">Shahzad</h2>
      <div class="main1 text-center text-white">
          
        <div
          class="submain1"
          style="background-color: green"
          :style="{ width: shhealth + '%' }"
        >
          <h4>{{ shhealth }}</h4>
        </div>
      </div>
    </div>
    <div class="col-sm-12 col-md-8 mt-4 mb-4 ">
         <h2 class="text-center">Computer</h2>
      <div class="main1 text-center text-white">
        <div
          class="submain1"
          style="background-color: green"
          :style="{ width: comhealth + '%' }"
        >
          <h4>{{ comhealth }}</h4>
        </div>
      </div>
    </div>

    <div class="col-sm-12 col-md-10" v-if="gameisrunning">
      <div class="startbtn text-center text-white">
        <button class="btn btn1" @click="gameisRunning">Start New Game</button>
      </div>
    </div>
    <div class="col-sm-12 col-md-10 mt-3" v-else>
      <div class="startbtn text-center text-white">
        <button class="btn btn2" @click="attack">Attack</button>
        <button class="btn btn3" @click="Specialattack">Special Attack</button>
        <button class="btn btn4" @click="heal">Heal</button>
        <button class="btn btn5" @click="newStart">Give Up</button>
      </div>
    </div>
    <div class="col-sm-12 col-md-10 mt-3" v-if="data.length > 0">
      <div class="startbtn text-center text-white">
        <ul>
          <li
            v-for="da in data"
            :key="da"
            :class="{ red: da.isData, green: !da.isData }"
          >
            {{ da.text }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      gameisrunning: true,
      shhealth: 100,
      comhealth: 100,

      data: [],
    };
  },
  methods: {
    heal() {
      if (this.shhealth <= 90 && this.comhealth <= 90) {
        this.shhealth += 10;
        this.comhealth += 10;
      } else {
        this.shhealth = 100;
        this.comhealth = 100;
      }
    },
    gameisRunning() {
      this.gameisrunning = false;
      this.shhealth = 100;
      this.comhealth = 100;
      this.data=[]
    },
    newStart() {
      this.gameisrunning = true;
      this.shhealth = 100;
      this.comhealth = 100;
      this.data=[]
    },

    attack() {
      var max = 10;
      var min = 3;
      this.shhealth -= Math.floor((Math.random() * max )+ 1, min);
      this.data.unshift({
        isData: true,
        text: "Playe Attach Moster" + this.shhealth,
      });

      max = 15;
      min = 5;
      this.comhealth -= Math.floor((Math.random() * max) + 1, min);
      this.data.unshift({
        isData: false,
        text: "Monster Attack Player" + this.comhealth,
      });
      this.checkHealth();
    },
    Specialattack() {
      max = 15;
      min = 5;
      this.comhealth -= Math.floor((Math.random() * max )+ 1, min);
      this.data.push({
        isData: true,
        text: "Playe Attach Moster" + this.shhealth,
      });
      var max = 10;
      var min = 3;
      this.shhealth -= Math.floor((Math.random() * max) + 1, min);
      this.data.push({
        isData: false,
        text: "Monster Attack Player" + this.comhealth,
      });
      this.checkHealth();
    },
    checkHealth() {
      if (this.shhealth <= 0) {
        if (confirm("You Won Start New Game?")) {
          this.newStart();
        } else {
          this.gameisrunning = true;
        }
      } else if (this.comhealth <= 0) {
        if (confirm("You Loss Start New Game?")) {
          this.newStart();
        } else {
          this.gameisrunning = true;
        }
      }
    },
  },
};
</script>

<style>
body{
    background-color: #e2e2e2;
}
ul li{
    list-style: none;
}
h2{
    /* background-color: #ccc; */
    color: red;
    font-weight: bolder;
}
.red {
  background-color: red;
}
.green {
  background-color: green;
}
.main1 {
  background-color: lightgray;
  margin-top: 10px;
}
.submain1 {
  transition: width 500ms;
}
.startbtn {
  box-shadow: 1px 1px 5px rgb(81, 76, 76);
  padding: 10px 0px;
}
.startbtn button {
  margin: 0 20px;
}
.startbtn .btn1 {
  background-color: lightcoral;
  color: white;
  font-weight: bold;
  border: none;
  outline: none;
  height: 50px;
  transition: background-color 0.3s ease-in-out;
}
.btn1:hover {
  background-color: coral;
  color: white;
}
.startbtn .btn2 {
  background-color: rgb(103, 103, 224);

  color: white;
  font-weight: bold;
  border: none;
  outline: none;
  height: 50px;
  transition: background-color 0.3s ease-in-out;
}
.btn2:hover {
  background-color: lightblue;
  color: white;
}
.startbtn .btn3 {
  background-color: rgb(103, 131, 131);
  color: white;
  font-weight: bold;
  border: none;
  outline: none;
  height: 50px;
  transition: background-color 0.3s ease-in-out;
}
.btn3:hover {
  background-color: cyan;
  color: white;
}
.startbtn .btn4 {
  background-color: lightgreen;
  color: white;
  font-weight: bold;
  border: none;
  outline: none;
  height: 50px;
  transition: background-color 0.3s ease-in-out;
}
.btn4:hover {
  background-color: rgb(58, 162, 58);
  color: white;
}
.startbtn .btn5 {
  background-color: lightgray;
  color: white;
  font-weight: bold;
  border: none;
  outline: none;
 max-height: 50px;
  transition: background-color 0.3s ease-in-out;
}
.btn5:hover {
  background-color: gray;
  color: white;
}
</style>