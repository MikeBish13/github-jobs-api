<template>
<div>
  <div>

    <div v-if="jobs.length">
    <div class="job-container container">
        <div class="single-job" v-for="job in filterJobs" v-bind:key="job.id">
      <Job v-bind:job="job" />
    </div>
    </div>    
    <button class="btn btn-primary" @click="loadMore">Load More</button>
    </div>

    <!-- Loading animation courtesy of @aleksander351 - CodePen https://codepen.io/aleksander351/pen/KzgKPo -->
    <div v-else class="container">
        <div id="wrapper">
            <div class="profile-main-loader">
            <div class="loader">
            <svg class="circular-loader" viewBox="25 25 50 50" >
            <circle class="loader-path" cx="50" cy="50" r="20" fill="none" stroke="#5964E0" stroke-width="2" />
             </svg>
            </div>
        </div>
        </div>


    </div>
  </div>
</div>
</template>

<script>
import Job from "./Job";


export default {
  name: "Jobs",
  components: {
    Job
  },
  data() {
    return {
      jobCount: 10,
    };
  },
  props: ["jobs"],
  watch: {
      jobs: function() {
          this.jobCount = 10
      },
  },
  computed: {
    filterJobs() {
        return this.jobs.slice(0, this.jobCount)
      }
    },
    methods: {
        loadMore() {
            if (this.jobCount + 10 <= this.jobs.length) {
                this.jobCount += 10
            } else {
                this.jobCount = this.jobs.length;
            }
        }
    }
};
</script>

<style lang="scss" scoped>
@import '../assets/css/main.scss';

.job-container {
    @include mq(tablet) {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
        gap: 11px;
    }
}

button {
    margin-bottom: 62px;
}

// Loading animation courtesy of @aleksander351 - CodePen https://codepen.io/aleksander351/pen/KzgKPo
#wrapper{
    position:relative;
    height:100%;
}

.profile-main-loader{
    left: 50% !important;
    margin-left:-100px;
    position: fixed !important;
    top: 50% !important;
    margin-top: -100px;
    width: 45px;
    z-index: 9000 !important;
}

.profile-main-loader .loader {
  position: relative;
  margin: 0px auto;
  width: 200px;
  height:200px;
}

.profile-main-loader .loader:before {
  content: '';
  display: block;
  padding-top: 100%;
}

.circular-loader {
  -webkit-animation: rotate 2s linear infinite;
          animation: rotate 2s linear infinite;
  height: 100%;
  -webkit-transform-origin: center center;
      -ms-transform-origin: center center;
          transform-origin: center center;
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  margin: auto;
}

.loader-path {
  stroke-dasharray: 150,200;
  stroke-dashoffset: -10;
  -webkit-animation: dash 1.5s ease-in-out infinite, color 6s ease-in-out infinite;
          animation: dash 1.5s ease-in-out infinite, color 6s ease-in-out infinite;
  stroke-linecap: round;
}

@-webkit-keyframes rotate {
  100% {
    -webkit-transform: rotate(360deg);
            transform: rotate(360deg);
  }
}

@keyframes rotate {
  100% {
    -webkit-transform: rotate(360deg);
            transform: rotate(360deg);
  }
}
@-webkit-keyframes dash {
  0% {
    stroke-dasharray: 1,200;
    stroke-dashoffset: 0;
  }
  50% {
    stroke-dasharray: 89,200;
    stroke-dashoffset: -35;
  }
  100% {
    stroke-dasharray: 89,200;
    stroke-dashoffset: -124;
  }
}
@keyframes dash {
  0% {
    stroke-dasharray: 1,200;
    stroke-dashoffset: 0;
  }
  50% {
    stroke-dasharray: 89,200;
    stroke-dashoffset: -35;
  }
  100% {
    stroke-dasharray: 89,200;
    stroke-dashoffset: -124;
  }
}
@-webkit-keyframes color {
  0% {
    stroke: #5964E0;
  }
  40% {
    stroke: #5964E0;
  }
  66% {
    stroke: #5964E0;
  }
  80%, 90% {
    stroke: #5964E0;
  }
}
@keyframes color {
  0% {
    stroke: #5964E0;
  }
  40% {
    stroke: #5964E0;
  }
  66% {
    stroke: #5964E0;
  }
  80%, 90% {
    stroke: #5964E0;
  }
}


</style>
