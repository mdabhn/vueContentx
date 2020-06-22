<template>
  <div class="container" style="margin-top:20px">
    <h1 class="text-center">Monster Slayer</h1>
    <div class="d-flex flex-top p-2 bd-highlight">
      <div class="flex-fill">
        <h4 class="text-center">You</h4>
        <div class="yourhealt mx-auto">
          <div class="yourhealt-now" :style="{ width: myCurrentStatus + '%' }">
            <p class="text-center" style="font-size:20px; color:white">
              {{ myCurrentStatus }}
            </p>
          </div>
        </div>
      </div>
      <div class="flex-fill">
        <h4 class="text-center">Monster</h4>
        <div class="monsterhealth mx-auto">
          <div
            class="monsterhealth-now"
            :style="{ width: monsterCurrentStatus + '%' }"
          >
            <p class="text-center" style="font-size:20px; color:white">
              {{ monsterCurrentStatus }}
            </p>
          </div>
        </div>
      </div>
    </div>
    <div class="d-flex justify-content-around w-25 mx-auto mt-4">
      <button class="btn btn-success" @click="heal">Heal</button>
      <button class="btn btn-success" @click="attack">Attack</button>
      <button class="btn btn-success" @click="powerHit">Power Hit</button>
    </div>
    <div class="d-flex justify-content-center mx-auto mt-2">
      <button class="btn btn-success" @click="resetGame">Restart</button>
    </div>

    <div class="overflow-auto" style="max-height: 300px" v-chat-scroll>
      <ul
        class="list-group w-50 mx-auto mt-4"
        v-for="(log, i) in logs"
        :key="i"
      >
        <li
          v-if="log.type == 'attack'"
          class="list-group-item list-group-item-success"
        >
          You Attacked {{ -log.monster }} health
        </li>
        <li
          v-if="log.type == 'attack'"
          class="list-group-item list-group-item-danger"
        >
          Monster Attacked {{ -log.me }} health
        </li>

        <li
          v-if="log.type == 'heal'"
          class="list-group-item list-group-item-success"
        >
          You healed By {{ +log.me }}
        </li>
        <li
          v-if="log.type == 'heal'"
          class="list-group-item list-group-item-danger"
        >
          Monster healed By {{ +log.monster }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Main',
    data() {
      return {
        myCurrentStatus: 100,
        monsterCurrentStatus: 100,
        attakUnit: 11,
        healUnit: 9,
        powerAttackunit: 20,
        logs: [],
      }
    },
    methods: {
      attack() {
        if (this.myCurrentStatus > 0 && this.monsterCurrentStatus > 0) {
          let myCal = Math.floor(Math.random() * this.attakUnit)

          this.myCurrentStatus = this.myCurrentStatus - myCal

          let monsterCal = Math.floor(Math.random() * this.attakUnit)

          this.monsterCurrentStatus = this.monsterCurrentStatus - monsterCal

          this.logs.push({
            me: myCal,
            monster: monsterCal,
            type: 'attack',
          })

          if (this.myCurrentStatus <= 0) {
            this.myCurrentStatus = 0
            alert('Monster Wins')
            this.resetGame()
          }

          if (this.monsterCurrentStatus <= 0) {
            this.monsterCurrentStatus = 0
            alert('You Win')
            this.resetGame()
          }
        }
      },
      heal() {
        if (this.myCurrentStatus < 100) {
          let myCal = Math.floor(Math.random() * this.healUnit)

          this.myCurrentStatus = this.myCurrentStatus + myCal

          let monsterCal = Math.floor(Math.random() * this.healUnit)

          this.monsterCurrentStatus = this.monsterCurrentStatus + monsterCal
          this.logs.push({
            me: myCal,
            monster: monsterCal,
            type: 'heal',
          })

          if (this.myCurrentStatus >= 100) {
            this.myCurrentStatus = 100
          }

          if (this.monsterCurrentStatus >= 100) {
            this.monsterCurrentStatus = 100
          }
        }
      },
      powerHit() {
        if (this.monsterCurrentStatus > 0) {
          let myCal = Math.floor(Math.random() * this.powerAttackunit)

          this.myCurrentStatus = this.myCurrentStatus - myCal

          let monsterCal = Math.floor(Math.random() * this.powerAttackunit)

          this.monsterCurrentStatus = this.monsterCurrentStatus - monsterCal
          this.logs.push({
            me: myCal,
            monster: monsterCal,
            type: 'attack',
          })
          if (this.myCurrentStatus <= 0) {
            this.myCurrentStatus = 0
            alert('Monster Wins')
            this.resetGame()
          }

          if (this.monsterCurrentStatus <= 0) {
            this.monsterCurrentStatus = 0
            alert('You Win')
            this.resetGame()
          }
        }
      },
      resetGame() {
        this.myCurrentStatus = 100
        this.monsterCurrentStatus = 100
        this.logs = []
      },
    },
  }
</script>

<style>
  .yourhealt {
    height: 30px;
    width: 80%;
    background-color: wheat;
    border-radius: 25px;
  }
  .monsterhealth {
    height: 30px;
    width: 80%;
    background-color: wheat;
    border-radius: 25px;
  }

  .yourhealt-now {
    height: 30px;
    transition-timing-function: 0.4s ease-in-out;
    background-color: green;
    border-radius: 25px;
  }
  .monsterhealth-now {
    height: 30px;
    transition-timing-function: 0.4s ease-in-out;
    background-color: rgb(180, 0, 0);
    border-radius: 25px;
  }

  @media only screen and (max-width: 600px) {
    .btn {
      height: 36px;
      margin: 2px;
    }
    .list-group {
      width: 100vw !important;
    }
  }
</style>
