<template>
  <header>
    <div class="header-container container">
    <router-link :to="{ name: 'Home' }"><img src="../assets/desktop/logo.svg" /></router-link>
    <div class="toggle">
      <img src="../assets/desktop/icon-sun.svg" />
        <input v-on:click="switchMode" type="checkbox" id="mode-btn" /><label for="mode-btn"></label>
      <img src="../assets/desktop/icon-moon.svg" />
    </div>
    </div>
  </header>
</template>

<script>
export default {
    data() {
        return {
            isDay: true
        }
    },
    methods: {
        switchMode() {
            if (this.isDay) {
                  document.documentElement.setAttribute('data-theme', 'dark');
                  localStorage.setItem('theme', 'dark');
            }
            else {
                  document.documentElement.setAttribute('data-theme', 'light');
                  localStorage.setItem('theme', 'light');
                }    

            this.isDay = !this.isDay
        }
    }
};
</script>

<style lang="scss" scoped>
@import '../assets/css/main.scss';

header {
  height: 136px;
  background: url("../assets/mobile/bg-pattern-header.svg");
  background-size: cover;
  background-repeat: no-repeat;

  img {
      cursor: pointer;
  }

  @include mq(tablet) {
    height: 160px;
    background: url('../assets/tablet/bg-pattern-header.svg');
    background-size: cover;
    background-repeat: no-repeat;
  }

  @include mq(desktop) {
    height: 162px;
    background: url('../assets/desktop/bg-pattern-header.svg');
    background-repeat: no-repeat;
  }
}

.header-container {
  height: 100%;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  padding-top: 32px;

  @include mq(tablet) {
    padding-top: 42px;
  }
}

.toggle {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 16px;
}

input[type="checkbox"] {
    display: none;
}

label {
  cursor: pointer;
  display: block;
  width: 48px;
  height: 24px;
  background: white;
  border-radius: 12px;
  position: relative;
}

label::before {
  content: "";
  position: absolute;
  height: 14px;
  width: 14px;
  background: #5964e0;
  top: 5px;
  left: 5px;
  border-radius: 50%;
  transition: 0.3s;
}

input:checked + label::before {
  left: calc(100% - 5px);
  transform: translateX(-100%);
}
</style>
