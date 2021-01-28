<template>
  <div class="top">
    <h1>{{ msg }}</h1>
    <div class="container">
      <div class="special">
        <div class="special-box">
          <label class="text">
            Strength
          </label>
          <div class="up" v-on:click="upStrength" id="strUp">+</div>
          <input id="str" class="score" type="number" max="10" min="1" :value="strength">
          <div class="down" v-on:click="downStrength" id="strDown">-</div>
        </div>
        <div class="special-box">
          <label class="text">
            Perception
          </label>
          <div class="up" v-on:click="upPerception">+</div>
          <input id="per" class="score" type="number" max="10" min="1" :value="perception">
          <div class="down" v-on:click="downPerception">-</div>
        </div>
        <div class="special-box">
          <label class="text">
            Endurance
          </label>
          <div class="up" v-on:click="upEndurance">+</div>
          <input id="end" class="score" type="number" max="10" min="1" :value="endurance">
          <div class="down" v-on:click="downEndurance">-</div>
        </div>
        <div class="special-box">
          <label class="text">
            Charisma
          </label>
          <div class="up" v-on:click="upCharisma">+</div>
          <input id="cha" class="score" type="number" max="10" min="1" :value="charisma">
          <div class="down" v-on:click="downCharisma">-</div>
        </div>
        <div class="special-box">
          <label class="text">
            Intelligence
          </label>
          <div class="up" v-on:click="upIntelligence">+</div>
          <input id="int" class="score" type="number" max="10" min="1" :value="intelligence">
          <div class="down" v-on:click="downIntelligence">-</div>
        </div>
        <div class="special-box">
          <label class="text">
            Agility
          </label>
          <div class="up" v-on:click="upAgility">+</div>
          <input id="agl" class="score" type="number" max="10" min="1" :value="agility">
          <div class="down" v-on:click="downAgility">-</div>
        </div>
        <div class="special-box">
          <label class="text">
            Luck
          </label>
          <div class="up" v-on:click="upLuck">+</div>
          <input id="lck" class="score" type="number" max="10" min="1" :value="luck">
          <div class="down" v-on:click="downLuck">-</div>
        </div>
        <label class="text">
          Remaining points: 
          <div class="barrier"></div>
          <input id="rem" class="score" type="number" readonly :value="remainingPoints">
        </label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Container',
  props: {
    msg: String
  },
   data: function () {
    return {
        strength: 5,
        perception: 5,
        endurance: 5,
        charisma: 5,
        intelligence: 5,
        agility: 5,
        luck: 5,
        remainingPoints: 5
    }
  },
  methods:{
    upStrength: function() {
      if(this.strength < 10 && this.remainingPoints > 0){
        this.strength++;
        this.remainingPoints--;
      }
    },
    downStrength: function() {
      if(this.strength > 1){
        this.strength--;
        this.remainingPoints++;
      }
    },
    upPerception: function() {
      if(this.perception < 10 && this.remainingPoints > 0){
        this.perception++;
        this.remainingPoints--;
      }
    },
    downPerception: function() {
      if(this.perception > 1){
        this.perception--;
        this.remainingPoints++;
      }
    },
    upEndurance: function() {
      if(this.endurance < 10 && this.remainingPoints > 0){
        this.endurance++;
        this.remainingPoints--;
      }
    },
    downEndurance: function() {
      if(this.endurance > 1){
        this.endurance--;
        this.remainingPoints++;
      }
    },
    upCharisma: function() {
      if(this.charisma < 10 && this.remainingPoints > 0){
        this.charisma++;
        this.remainingPoints--;
      }
    },
    downCharisma: function() {
      if(this.charisma > 1){
        this.charisma--;
        this.remainingPoints++;
      }
    },
    upIntelligence: function() {
      if(this.intelligence < 10 && this.remainingPoints > 0){
        this.intelligence++;
        this.remainingPoints--;
      }
    },
    downIntelligence: function() {
      if(this.intelligence > 1){
        this.intelligence--;
        this.remainingPoints++;
      }
    },
    upAgility: function() {
      if(this.agility < 10 && this.remainingPoints > 0){
        this.agility++;
        this.remainingPoints--;
      }
    },
    downAgility: function() {
      if(this.agility > 1){
        this.agility--;
        this.remainingPoints++;
      }
    },
    upLuck: function() {
      if(this.luck < 10 && this.remainingPoints > 0){
        this.luck++;
        this.remainingPoints--;
      }
    },
    downLuck: function() {
      if(this.luck > 1){
        this.luck--;
        this.remainingPoints++;
      }
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.container{
  width: 60%;
  margin: auto;
}
.special{
  background-color: #363027;
  text-align: left;
  display: inline-block;
  padding: 5px;
  border: 1px solid #666666;
  width: 33%;
}
.score{
  color: #ffb642;
  clear: none;
  width: 40px;
  background: #4d4336;
  border: 1px solid #666666 !important;
  padding: 2px;
  text-align: center;
  margin-top: 2px;
  border-radius: 3px;
  float: right;
}
.text{
  color: #ffb642;
}
.special-box{
  line-height: 25px;
  position: relative;
}
.up{
  color: #ffb642;
  float: right;
  padding-left: 5px;
  padding-right: 5px;
  font-size: 20px;
  font-weight: bold;
  cursor: pointer;
}
.down{
  color: #ffb642;
  float: right;
  padding-left: 5px;
  padding-right: 8px;
  font-size: 20px;
  font-weight: bold;
  cursor: pointer;
}
.barrier{
  width: 21px;
  height: 2px;
  float: right;
}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
input[type=number] {
  -moz-appearance: textfield;
}
</style>
<!-- npm run serve -->
