<template>
  <div class="top">
    <div class="container">
      <!-- Block 1: SPECIAL stats, name and faction. -->
      <div class="row">
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
            <label class="text" id="level">
              Level
            </label>
            <div class="barrier"></div>
            <input class="score" type="number" :value="level" readonly>
          </div>
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
          <div v-for="trait in traits" :key="trait.name">
            <input type="checkbox" :value="trait.name" v-model="selectedTraits" 
            :disabled="selectedTraits.length > 1 && selectedTraits.indexOf(trait.name) === -1"  @change="updateAll()">
            <label class="text" :for="trait.name"> {{ trait.name }}</label>
          </div>
          <div class="header"></div>
          <p class="text" v-if="selectedTraits[0] != null"> {{ traitDescription(selectedTraits[0]) }}</p>
          <p class="text" v-if="selectedTraits[1] != null"> {{ traitDescription(selectedTraits[1]) }}</p>
        </div>
        <!-- Block 3: Skills -->
        <div class="special">
          <div class="special-box">
            <label v-on:click="toggleSkill" class="text" id="barter">
              Barter
            </label>
            <input class="score" type="number" :value="barter" readonly>
          </div>
          <div class="special-box">
            <label v-on:click="toggleSkill" class="text" id="energy">
              Energy Weapons
            </label>
            <input class="score" type="number" :value="energy" readonly>
          </div>
          <div class="special-box">
            <label v-on:click="toggleSkill" class="text" id="explosives">
              Explosives
            </label>
            <input class="score" type="number" :value="explosives" readonly>
          </div>
          <div class="special-box">
            <label v-on:click="toggleSkill" class="text" id="guns">
              Guns
            </label>
            <input class="score" type="number" :value="guns" readonly>
          </div>
          <div class="special-box">
            <label v-on:click="toggleSkill" class="text" id="lockpick">
              Lockpick
            </label>
            <input class="score" type="number" :value="lockpick" readonly>
          </div>
          <div class="special-box">
            <label v-on:click="toggleSkill" class="text" id="medicine">
              Medicine
            </label>
            <input class="score" type="number" :value="medicine" readonly>
          </div>
          <div class="special-box">
            <label v-on:click="toggleSkill" class="text" id="melee">
              Melee Weapons
            </label>
            <input class="score" type="number" :value="melee" readonly>
          </div>
          <div class="special-box">
            <label v-on:click="toggleSkill" class="text" id="repair">
              Repair
            </label>
            <input class="score" type="number" :value="repair" readonly>
          </div>
          <div class="special-box">
            <label v-on:click="toggleSkill" class="text" id="science">
              Science
            </label>
            <input class="score" type="number" :value="science" readonly>
          </div>
          <div class="special-box">
            <label v-on:click="toggleSkill" class="text" id="sneak">
              Sneak
            </label>
            <input class="score" type="number" :value="sneak" readonly>
          </div>
          <div class="special-box">
            <label v-on:click="toggleSkill" class="text" id="speech">
              Speech
            </label>
            <input class="score" type="number" :value="speech" readonly>
          </div>
          <div class="special-box">
            <label v-on:click="toggleSkill" class="text" id="survival">
              Survival
            </label>
            <input class="score" type="number" :value="survival" readonly>
          </div>
          <div class="special-box">
            <label v-on:click="toggleSkill" class="text" id="unarmed">
              Unarmed
            </label>
            <input class="score" type="number" :value="unarmed" readonly>
          </div>
          <div class="header"></div>
          <!-- Place Action Points, Equipment Weight & Damage percentage based upon chosen weapon -->
          <div class="special-box">
            <label class="text" id="hp">
              Health Points
            </label>
            <input class="score" type="number" :value="hp" readonly>
          </div>
          <div class="special-box">
            <label class="text" id="ap">
              Action Points
            </label>
            <input class="score" type="number" :value="ap" readonly>
          </div>
          <div class="special-box">
            <label class="text" id="carry">
              Carry Weight
            </label>
            <input class="score" type="number" :value="carry" readonly>
          </div>
          <div class="special-box hidden">
            <label class="text" id="lvlUpPoints">
              Points to spend
            </label>
            <input class="score" type="number" :value="lvlUpPoints" readonly>
          </div>
          <div class="header hidden"></div>
          <button class="lvlUp hidden" v-on:click="levelUp">
            Level up
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
   data: function () {
    return {
      // Initializing data
      strength: 5,
      perception: 5,
      endurance: 5,
      charisma: 5,
      intelligence: 5,
      agility: 5,
      luck: 5,
      remainingPoints: 5,
      barter: null,
      energy: null,
      explosives: null,
      guns: null,
      lockpick: null,
      medicine: null,
      melee: null,
      repair: null,
      science: null,
      sneak: null,
      speech: null,
      survival: null,
      unarmed: null,
      ap: null,
      equip: null,
      carry: null,
      hp: null,
      lvlUpPoints: 0,
      level: 1,
      // Choosing a faction/ multiple traits
      factions: [
        {name: "NCR", description: "The NCR emphasizes and strives to support a plethora of old world values, such as democracy, personal liberty, and the rule of law. It also aims to restore general order to the wasteland, the improvement and development of infrastructure and economic systems, and overarching peace between people. Similar to institutions of the old world it seeks to emulate, continued expansion has created challenges with territorial control, loyalty, and corruption that plague the Republic and serve to hinder its goals. The NCR is often criticized by residents of the Mojave wasteland as well as other factions for being hawkish, imperialistic, poorly managed and over-extended in the region, and trying to attempt to emulate old world values that led to nuclear holocaust in the first place."},
        {name: "The Legion", description:"Caesar's Legion is an imperialistic, ultra-reactionary totalitarian dictatorship based on large scale slavery. Founded in 2247 by Edward Sallow, who then renamed himself Caesar, and Joshua Graham (also known as the Malpais Legate). The Legion uses trappings of the ancient Roman Empire as part of a unifying identity imposed on its tribes but does not recreate any cultural, social, or political institutions of ancient Rome. The Legion itself is simply a slave army built on ruthlessly utilitarian principles, supported by several tributary populations."},
        {name: "Mr. House", description:"Robert Edwin House is the self-styled president, CEO, and sole proprietor of the New Vegas Strip in the Mojave Wasteland in the year 2281. Prior to the Great War, House was an ever-alluring, reclusive enigma to the world and a veritable celebrity with various tabloids and news articles covering his every move in business and private life. His founding of RobCo Industries propelled him to the top through business savvy using mathematical prediction algorithms; gaining the envy of other roboticists and corporations through sheer success. As such, RobCo technology became ubiquitous across the former United States both in the civilian and military sectors, and shaping the technological progression of it."},
        {name: "Yes Man", description:"Yes Man was originally a generic securitron robot programmed to work for Mr. House like all the other securitrons found on the Strip. He was recovered by Benny and several of the Chairmen after being damaged by a pulse grenade. Following this incident, Followers of the Apocalypse member Emily Ortal examined the securitron in order to learn Mr. House's secrets in exchange for reprogramming him for Benny's personal use. The reprogramming resulted in Yes Man doing exactly as he was told. Yes Man will help you take down House and rule New Vegas in your stead."}
      ],
      traits: [
        {name: "Built to Destroy", description: "+3% weapon critical hit chance; but weapon condition decays 15% faster."},
        {name: "Claustrophobia", description: "+1 to all SPECIAL attributes while outside; but -1 when indoors."},
        {name: "Early Bird", description: "+2 to all SPECIAL attributes from 6am to 12pm; but -1 from 6pm to 6am."},
        {name: "Fast Shot", description: "Guns and energy weapons you fire are 20% quicker, Action Point cost for your guns and energy weapons are 20% lower; but guns and energy weapons are 20% less acurate."},
        {name: "Four Eyes", description: "+2 Perception when wearing glasses, bonus does not apply when determining Perk requirements; but -1 permanent perception reduction."},
        {name: "Good Natured", description: "Increase Speech, Medicine, Repair, Science and Barter skill +5; but decreases Energy Weapons, Explosives, Guns, Melee Weapons and Unarmed skills by 5."},
        {name: "Heavy Handed", description: "Melee and Unarmed do 20% more damage; but Melee and Unarmed criticals do 60% less damage."},
        {name: "Hoarder", description: "+25 lbs to total carry weight; but -1 to all SPECIAL attributes while current equipment weight is below 160 lbs."},
        {name: "Hot Blooded", description: "+15% damage while below 50% health; but -2 Perception and Agility while below 50% health."},
        {name: "Kamikaze", description: "+10 Action Points; but -2 damage threshold."},
        {name: "Logan's Loophole", description: "Chems last twice as long and addiction rates are set to zero; but locks the level cap at 30."},
        {name: "Loose Cannon", description: "Attack speed with thrown weapons is increased by 30%; but thrown weapons have 25% less range."},
        {name: "Skilled", description: "+5 to every skill, but 10% less experience gained."},
        {name: "Small Frame", description: "+1 Agility; but 25% extra limb damage."},
        {name: "Trigger Discipline", description: "Guns and Energy Weapons you fire are 20% more accurate, but Guns and Energy weapons you fire are 20% slower and Action Points cost for your guns and energy weapons are 20% higher."},
        {name: "Wild Wasteland", description: "Adds additional 'wacky' content and modifies existing content and special encounters"}
      ],
      // Keeping track of chosen skills/traits/ faction
      selectedSkills: [],
      selectedTraits: [],
      selectedFaction: null,
      // Booleans to make sure certain traits are reversible.
      selectedFourEyes: false,
      selectedHoarder: false,
      selectedSmallFrame: false,
    }
  },
  methods:{
    // Upgrading SPECIAL stats.
    upStrength: function() {
      if(this.strength < 10 && this.remainingPoints > 0){
        this.strength++;
        this.remainingPoints--;
      }
      this.updateAll()
    },
    downStrength: function() {
      if(this.strength > 1){
        this.strength--;
        this.remainingPoints++;
      }
      this.updateAll()
    },
    upPerception: function() {
      if(this.perception < 10 && this.remainingPoints > 0){
        this.perception++;
        this.remainingPoints--;
      }
      this.updateAll()
    },
    downPerception: function() {
      if(this.perception > 1){
        this.perception--;
        this.remainingPoints++;
      }
      this.updateAll()
    },
    upEndurance: function() {
      if(this.endurance < 10 && this.remainingPoints > 0){
        this.endurance++;
        this.remainingPoints--;
      }
      this.updateAll()
    },
    downEndurance: function() {
      if(this.endurance > 1){
        this.endurance--;
        this.remainingPoints++;
      }
      this.updateAll()
    },
    upCharisma: function() {
      if(this.charisma < 10 && this.remainingPoints > 0){
        this.charisma++;
        this.remainingPoints--;
      }
      this.updateAll()
    },
    downCharisma: function() {
      if(this.charisma > 1){
        this.charisma--;
        this.remainingPoints++;
      }
      this.updateAll()
    },
    upIntelligence: function() {
      if(this.intelligence < 10 && this.remainingPoints > 0){
        this.intelligence++;
        this.remainingPoints--;
      }
      this.updateAll()
    },
    downIntelligence: function() {
      if(this.intelligence > 1){
        this.intelligence--;
        this.remainingPoints++;
      }
      this.updateAll()
    },
    upAgility: function() {
      if(this.agility < 10 && this.remainingPoints > 0){
        this.agility++;
        this.remainingPoints--;
      }
      this.updateAll()
    },
    downAgility: function() {
      if(this.agility > 1){
        this.agility--;
        this.remainingPoints++;
      }
      this.updateAll()
    },
    upLuck: function() {
      if(this.luck < 10 && this.remainingPoints > 0){
        this.luck++;
        this.remainingPoints--;
      }
      this.updateAll()
    },
    downLuck: function() {
      if(this.luck > 1){
        this.luck--;
        this.remainingPoints++;
      }
      this.updateAll()
    },
    traitDescription: function(name) {
      for (var i=0; i < this.traits.length; i++) {
        if (this.traits[i].name === name) {
            return this.traits[i].description;
        }
      }
    },
    updateSkills: function(){
      this.barter = Math.ceil(2 + (2 * this.charisma) + (this.luck / 2));
      this.energy = Math.ceil(2 + (2 * this.perception) + (this.luck / 2));
      this.explosives = Math.ceil(2 + (2 * this.perception) + (this.luck / 2));
      this.guns = Math.ceil(2 + (2 * this.agility) + (this.luck / 2));
      this.lockpick = Math.ceil(2 + (2 * this.perception) + (this.luck / 2));
      this.medicine = Math.ceil(2 + (2 * this.intelligence) + (this.luck / 2));
      this.melee = Math.ceil(2 + (2 * this.strength) + (this.luck / 2));
      this.repair = Math.ceil(2 + (2 * this.intelligence) + (this.luck / 2));
      this.science = Math.ceil(2 + (2 * this.intelligence) + (this.luck / 2));
      this.sneak = Math.ceil(2 + (2 * this.agility) + (this.luck / 2));
      this.speech = Math.ceil(2 + (2 * this.charisma) + (this.luck / 2));
      this.survival = Math.ceil(2 + (2 * this.endurance) + (this.luck / 2));
      this.unarmed = Math.ceil(2 + (2 * this.endurance) + (this.luck / 2));
      this.ap = Math.ceil(65 + (3 * this.agility));
      this.carry = Math.ceil(150 + (this.strength * 10));
      this.hp = Math.ceil(100+(this.endurance * 5) + ((this.level - 1) * 5));
    },
    toggleSkill: function(event){
      if(this.selectedSkills.length < 3 || this.selectedSkills.includes(event.target.id)){
        if(this.selectedSkills.includes(event.target.id)){
          const index = this.selectedSkills.indexOf(event.target.id);
          this.selectedSkills.splice(index, 1);
          document.getElementById(event.target.id).classList.remove("bold");
        } else {
          this.selectedSkills.push(event.target.id);
          document.getElementById(event.target.id).classList.add("bold");
        }
        this.updateAll();
      }
    },
    updateAll: function(){
      this.updateSkills();
      this.updateTags();
      this.updateTraits();
      this.checkLvlUpAvailable();
    },
    updateTags: function(){
      for(var i = 0; i < this.selectedSkills.length; i++){
        switch(this.selectedSkills[i]){
          case "barter":
            this.barter += 15;
            break;
          case "energy":
            this.energy += 15;
            break;
          case "explosives":
            this.explosives += 15;
            break;
          case "guns":
            this.guns += 15;
            break;
          case "lockpick":
            this.lockpick += 15;
            break;
          case "medicine":
            this.medicine += 15;
            break;
          case "melee":
            this.melee += 15;
            break;
          case "repair":
            this.repair += 15;
            break;
          case "science":
            this.science += 15;
            break;
          case "sneak":
            this.sneak += 15;
            break;
          case "speech":
            this.speech += 15;
            break;
          case "survival":
            this.survival += 15;
            break;
          case "unarmed":
            this.unarmed += 15;
            break;
        }
      }
    },
    updateTraits: function(){
      for(var i = 0; i < this.selectedTraits.length; i++){
        switch(this.selectedTraits[i]){
          case "Four Eyes":
            if(!this.selectedFourEyes && this.perception < 10 && this.perception > 1){
              this.perception -= 1;
              this.selectedFourEyes = true;
            }
            break;
          case "Good Natured":
            this.speech += 5;
            this.medicine += 5;
            this.repair += 5;
            this.science += 5;
            this.barter += 5;
            this.energy -= 5;
            this.explosives -= 5;
            this.guns -= 5;
            this.melee -= 5;
            this.unarmed -= 5;
            break;
          case "Hoarder":
            if(!this.selectedHoarder && this.strength > 1 && this.perception > 1 && this.endurance > 1 
              && this.charisma > 1 && this.intelligence > 1 && this.agility > 1 && this.luck > 1){
              this.equip += 25;
              this.strength -= 1;
              this.perception -= 1;
              this.endurance -= 1;
              this.charisma -= 1;
              this.intelligence -= 1;
              this.agility -= 1;
              this.luck -= 1;
              this.selectedHoarder = true;
            }
            break;
          case "Kamikaze":
            this.ap += 10;
            break;
          case "Skilled":
            this.barter += 5;
            this.energy += 5;
            this.explosives += 5;
            this.guns += 5;
            this.lockpick += 5;
            this.medicine += 5;
            this.melee += 5;
            this.repair += 5;
            this.science += 5;
            this.sneak += 5;
            this.speech += 5;
            this.survival += 5;
            this.unarmed += 5;
            break;
          case "Small Frame":
            if(!this.selectedSmallFrame && this.agility < 10){
              this.agility += 1;
              this.selectedSmallFrame = true;
            }
            break;
        }
      }
      // Check if Four Eyes, Hoarder or Small Frame were selected and are no longer selected. Reverts back stats if so.
      if(this.selectedFourEyes && this.selectedTraits[0] != "Four Eyes" && this.selectedTraits[1] != "Four Eyes"){
        this.selectedFourEyes = false;
        this.perception += 1;
      }
      if(this.selectedHoarder && this.selectedTraits[0] != "Hoarder" && this.selectedTraits[1] != "Hoarder"){
        this.selectedHoarder = false;
        this.equip -= 25;
        this.strength += 1;
        this.perception += 1;
        this.endurance += 1;
        this.charisma += 1;
        this.intelligence += 1;
        this.agility += 1;
        this.luck += 1;
      }
      if(this.selectedSmallFrame && this.selectedTraits[0] != "Small Frame" && this.selectedTraits[1] != "Small Frame"){
        this.selectedSmallFrame = false;
        this.agility -= 1;
      }
    },
    checkLvlUpAvailable: function(){
      if(this.remainingPoints == 0 && this.selectedSkills.length == 3){
        let hidden = document.getElementsByClassName("hidden");
        [].forEach.call(hidden, function (hide) {
          hide.style.display = "block";
        });
      }
      if(this.level == 1 && (this.remainingPoints != 0 || this.selectedSkills.length != 3)){
        let hidden = document.getElementsByClassName("hidden");
        [].forEach.call(hidden, function (hide) {
          hide.style.display = "none";
        });
      }
    },
    levelUp: function(){
      // WATCH OUT.
      // THE GAME REMEMBERS 0.5, SO LVL 2 you can get 13 skill points, while at lvl 3 you can get 14 without raising your int.
      if(this.lvlUpPoints == 0){
        this.lvlUpPoints = 10 + Math.floor(this.intelligence/2);
      }
    }
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
  display: table;
}
.row{
  display: table-row;
}
.special{
  background-color: #363027;
  text-align: left;
  display: inline-block;
  padding: 5px;
  border: 1px solid #666666;
  width: 32%;
  margin-top: 10px;
  display: table-cell;
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
.lvlUp{
  background-color: #ffb642;
  color: #4d4336;
  border: #666666;
  float: right;
  padding: 5px;
  border-radius: 8px;
}
.hidden{
  display: none;
}
.header{
    font-size: 12px;
    font-weight: bold;
    margin-top: 10px;
    margin-bottom: 10px;
    border-bottom: 2px solid #ffb642;
}
.barrier{
  width: 21.5px;
  height: 2px;
  float: right;
}
.bold{
  font-weight: bold;
  font-style: italic;
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
