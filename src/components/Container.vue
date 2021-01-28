<template>
  <div class="top">
    <h1>{{ msg }}</h1>
    <div class="container">
      <!-- Block 1: SPECIAL stats, name and faction. -->
      <div class="special">
        <div class="special-box">
          <label class="text">
            Name
          </label>
          <input class="name" value="Courier">
        </div>
        <div class="special-box">
          <label class="text">
            Faction
          </label>
          <select name="factions" class="name" v-model="selectedFaction">
            <option v-for="faction in factions" v-bind:key="faction.name" v-bind:value="{ name: faction.name, text: faction.description }">
              {{ faction.name }}
            </option>
          </select>
        </div>
        <div class="header"></div>
        <div class="special-box">
          <label class="text">
            Strength
          </label>
          <div class="up" v-on:click="upStrength" id="strUp">+</div>
          <input class="score" type="number" max="10" min="1" :value="strength">
          <div class="down" v-on:click="downStrength" id="strDown">-</div>
        </div>
        <div class="special-box">
          <label class="text">
            Perception
          </label>
          <div class="up" v-on:click="upPerception">+</div>
          <input class="score" type="number" max="10" min="1" :value="perception">
          <div class="down" v-on:click="downPerception">-</div>
        </div>
        <div class="special-box">
          <label class="text">
            Endurance
          </label>
          <div class="up" v-on:click="upEndurance">+</div>
          <input class="score" type="number" max="10" min="1" :value="endurance">
          <div class="down" v-on:click="downEndurance">-</div>
        </div>
        <div class="special-box">
          <label class="text">
            Charisma
          </label>
          <div class="up" v-on:click="upCharisma">+</div>
          <input class="score" type="number" max="10" min="1" :value="charisma">
          <div class="down" v-on:click="downCharisma">-</div>
        </div>
        <div class="special-box">
          <label class="text">
            Intelligence
          </label>
          <div class="up" v-on:click="upIntelligence">+</div>
          <input class="score" type="number" max="10" min="1" :value="intelligence">
          <div class="down" v-on:click="downIntelligence">-</div>
        </div>
        <div class="special-box">
          <label class="text">
            Agility
          </label>
          <div class="up" v-on:click="upAgility">+</div>
          <input class="score" type="number" max="10" min="1" :value="agility">
          <div class="down" v-on:click="downAgility">-</div>
        </div>
        <div class="special-box">
          <label class="text">
            Luck
          </label>
          <div class="up" v-on:click="upLuck">+</div>
          <input class="score" type="number" max="10" min="1" :value="luck">
          <div class="down" v-on:click="downLuck">-</div>
        </div>
        <label class="text">
          Remaining points: 
          <div class="barrier"></div>
          <input class="score" type="number" readonly :value="remainingPoints">
        </label>
        <div class="header"></div>
        <p class="text" v-if="selectedFaction != null">{{ selectedFaction.text }}</p>
      </div>
      <!-- Block 2: Starting perks and description -->
      <div class="special">
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
        remainingPoints: 5,
        factions: [
          {name: "NCR", description: "The NCR emphasizes and strives to support a plethora of old world values, such as democracy, personal liberty, and the rule of law. It also aims to restore general order to the wasteland, the improvement and development of infrastructure and economic systems, and overarching peace between people. Similar to institutions of the old world it seeks to emulate, continued expansion has created challenges with territorial control, loyalty, and corruption that plague the Republic and serve to hinder its goals. The NCR is often criticized by residents of the Mojave wasteland as well as other factions for being hawkish, imperialistic, poorly managed and over-extended in the region, and trying to attempt to emulate old world values that led to nuclear holocaust in the first place."},
          {name: "The Legion", description:"Caesar's Legion is an imperialistic, ultra-reactionary totalitarian dictatorship based on large scale slavery. Founded in 2247 by Edward Sallow, who then renamed himself Caesar, and Joshua Graham (also known as the Malpais Legate). The Legion uses trappings of the ancient Roman Empire as part of a unifying identity imposed on its tribes but does not recreate any cultural, social, or political institutions of ancient Rome. The Legion itself is simply a slave army built on ruthlessly utilitarian principles, supported by several tributary populations."},
          {name: "Mr. House", description:"Robert Edwin House is the self-styled president, CEO, and sole proprietor of the New Vegas Strip in the Mojave Wasteland in the year 2281. Prior to the Great War, House was an ever-alluring, reclusive enigma to the world and a veritable celebrity with various tabloids and news articles covering his every move in business and private life. His founding of RobCo Industries propelled him to the top through business savvy using mathematical prediction algorithms; gaining the envy of other roboticists and corporations through sheer success. As such, RobCo technology became ubiquitous across the former United States both in the civilian and military sectors, and shaping the technological progression of it."},
          {name: "Yes Man", description:"Yes Man was originally a generic securitron robot programmed to work for Mr. House like all the other securitrons found on the Strip. He was recovered by Benny and several of the Chairmen after being damaged by a pulse grenade. Following this incident, Followers of the Apocalypse member Emily Ortal examined the securitron in order to learn Mr. House's secrets in exchange for reprogramming him for Benny's personal use. The reprogramming resulted in Yes Man doing exactly as he was told. Yes Man will help you take down House and rule New Vegas in your stead."}
        ],
        selectedFaction: null
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
.name{
  color: #ffb642;
  clear: none;
  width: 40%;
  background: #4d4336;
  border: 1px solid #666666 !important;
  padding: 2px;
  text-align: center;
  margin-top: 2px;
  border-radius: 3px;
  float: right;
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
.header{
    font-size: 12px;
    font-weight: bold;
    margin-top: 10px;
    margin-bottom: 10px;
    border-bottom: 2px solid #ffb642;
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
