<template>
  <div class="about">
    <h1>Альт</h1>
    <h2>{{ this.randomNote.name + this.randomNote.octave }}</h2>
    <p>Счет: {{ this.score }}</p>
    <p>Ошибки: {{ this.mistakes }}</p>

    <div class="center">
      <div class="staff-container">
        <div class="staff">
          <div class="staff-line"></div>
          <div class="staff-line"></div>
          <div class="staff-line"></div>
          <div class="staff-line"></div>
          <div class="staff-line"></div>
          <div
            class="note"
            :class="this.randomNote.name + this.randomNote.octave"
          ></div>
        </div>
      </div>
    </div>

    <div>
      <button
        @click="checkResult('c')"
        class="button-primary delimiter-vertical"
      >
        C
      </button>
      <button
        @click="checkResult('d')"
        class="button-primary delimiter-vertical"
      >
        D
      </button>
      <button
        @click="checkResult('e')"
        class="button-primary delimiter-vertical"
      >
        E
      </button>
      <button
        @click="checkResult('f')"
        class="button-primary delimiter-vertical"
      >
        F
      </button>
      <button
        @click="checkResult('g')"
        class="button-primary delimiter-vertical"
      >
        G
      </button>
      <button
        @click="checkResult('a')"
        class="button-primary delimiter-vertical"
      >
        A
      </button>
      <button
        @click="checkResult('b')"
        class="button-primary delimiter-vertical"
      >
        B
      </button>
    </div>
  </div>
  <div class="delimiter-horizontal">
    <button @click="restartPractice" class="button-primary">
      Начать заново
    </button>
  </div>
</template>

<script>
export default {
  name: "ViolaPractice",
  data() {
    return {
      score: 0,
      mistakes: 0,
      randomNote: {
        C: {
          name: "c",
          ru_name: "до",
          octave: 1,
        },
      },
      notes: {
        C: {
          name: "c",
          ru_name: "до",
        },
        D: {
          name: "d",
          ru_name: "ре",
        },
        E: {
          name: "e",
          ru_name: "ми",
        },
        F: {
          name: "f",
          ru_name: "фа",
        },
        G: {
          name: "g",
          ru_name: "соль",
        },
        A: {
          name: "a",
          ru_name: "ля",
        },
        B: {
          name: "b",
          ru_name: "си",
        },
      },
    };
  },
  created() {
    this.getRandomNote();
  },
  methods: {
    getNoteImg(noteName) {
      return require(`@/assets/${noteName}2.png`);
    },
    getRandomNote() {
      const keys = Object.keys(this.notes);
      const randomKey = keys[Math.floor(Math.random() * keys.length)];
      const randomNumber = Math.floor(Math.random() * 2) + 1;

      if (this.randomNote === this.notes[randomKey]) {
        this.randomNote = this.notes[randomKey];
        this.randomNote.octave = randomNumber;
      } else {
        this.randomNote = this.notes[randomKey];
        this.randomNote.octave = randomNumber;
      }
    },
    checkResult(noteName) {
      if (noteName === this.randomNote.name) {
        this.score = this.score + 1;
        this.getRandomNote();
      } else {
        this.mistakes = this.mistakes + 1;
        this.getRandomNote();
      }
    },
    restartPractice() {
      this.score = 0;
      this.mistakes = 0;
      this.getRandomNote();
    },
  },
};
</script>
