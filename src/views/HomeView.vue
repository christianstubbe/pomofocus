<template>
  <v-container class="mt-16">
    <v-row justify="space-around">
      <v-btn
        :active="activeSessionType == 'long-session'"
        @click="setSession('long-session')"
        >Long Session</v-btn
      >
      <v-btn
        :active="activeSessionType == 'short-session'"
        @click="setSession('short-session')"
        >Short Session</v-btn
      >
      <v-btn
        :active="activeSessionType == 'long-break'"
        @click="setSession('long-break')"
        >Long Break</v-btn
      >
      <v-btn
        :active="activeSessionType == 'short-break'"
        @click="setSession('short-break')"
        >Short Break</v-btn
      >
    </v-row>
    <v-row justify="center">
        <h1>{{ timerMin }} : {{ timerSeconds }}</h1> 
    </v-row>
    <v-row justify="center">
      <v-btn v-if="!isSessionActive" size="x-large" color="primary" @click="startTimer">Start</v-btn>
      <v-btn v-if="isSessionActive" size="x-large" color="secondary" @click="pauseTimer">Pause</v-btn>
    </v-row>
  </v-container>
</template>


<script lang="ts">

export default {
  data() {
    return {
      timer: 10,
      timerInterval: 0,
      activeSessionType: "long-session",
      isSessionActive: false,
    }
  },

  computed: {
    timerMin() {
      const minutes = Math.floor(this.timer / 60);
      return (minutes < 10 ? "0" : "") + minutes;
    },
    timerSeconds() {
      const seconds = Math.floor(this.timer % 60);
      return (seconds < 10 ? "0" : "") + seconds;
    },
  },

  methods: {

    startTimer() {
      if (this.isSessionActive) {
        this.stopTimer();
      }
      this.isSessionActive = true;
      this.timerInterval = setInterval(() => {
        if (this.timer > 0) {
          this.timer--;
        } else {
          this.stopTimer();
        }
      }, 1000);
    },

    stopTimer() {
      this.isSessionActive = false;
      if (this.timerInterval) {
        clearInterval(this.timerInterval);
        this.timerInterval = 0;
      }
    },

    pauseTimer() {
      this.stopTimer();
    },


    setSession(name: string) {
      this.activeSessionType = name;
      switch (name) {
        case "long-session":
          this.timer = 50 * 60;
          break;
        case "short-session":
          this.timer = 25 * 60;
          break;
        case "long-break":
          this.timer = 15 * 60;
          break;
        case "short-break":
          this.timer = 5 * 60;
          break;
      }
    },
  },
};
</script>

