<script lang="ts">
export default {
  name: "HomeView",

  data() {
    return {
      timer: 50 * 60,
      activeSessionType: "long-session",
    };
  },

  methods: {
    startTimer() {
      setInterval(() => {
        this.timer--;
      }, 1000);
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

  computed: {
    timerValue(): number {
      return this.timer;
    },
  },
};
</script>

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
        >Long Session</v-btn
      >
      <v-btn
        :active="activeSessionType == 'short-break'"
        @click="setSession('short-break')"
        >Short Session</v-btn
      >
    </v-row>
    <v-row class="my-16" justify="center">
      <span class="text-h1">{{ timerValue }}</span>
    </v-row>
    <v-row justify="center">
      <v-btn color="primary" @click="startTimer">Start</v-btn>
    </v-row>
  </v-container>
</template>
