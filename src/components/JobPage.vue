<template>
  <div>
    <Header />
    <div class="container">
      <div class="company-box">
        <div class="company-box-left">
          <img v-bind:src="job.company_logo" />
          <div class="company-box-details">
            <h1>{{ job.company }}</h1>
            <p>{{ job.company_url }}</p>
          </div>
        </div>
        <a v-bind:href="job.company_url">Company Site</a>
      </div>

      <div class="main-box">
        <div class="main-box-header">
          <div class="main-box-header-left">
            <p class="jobPage-date-type">
              {{ job.created_at | moment("from") }} <span>.</span>
              {{ job.type }}
            </p>
            <p class="jobPage-title">{{ job.title }}</p>
            <p class="jobPage-location">{{ job.location }}</p>
          </div>
          <a v-bind:href="job.company_url" class="btn btn-primary">Apply Now</a>
        </div>
        <p class="job-desc" v-html="job.description"></p>
      </div>

      <div class="apply-box">
        <h2>How to apply</h2>
        <p v-html="job.how_to_apply"></p>
      </div>
    </div>
    <div class="footer-box">
      <div class="footer-box-container">
        <div class="footer-box-left">
          <h1>{{ job.company }}</h1>
          <p>{{ job.company_url }}</p>
        </div>
        <a v-bind:href="job.company_url" class="btn btn-primary">Apply Now</a>
      </div>
    </div>
  </div>
</template>

<script>
import Header from "../layout/Header";
export default {
  name: "JobPage",
  components: {
    Header,
  },
  props: ["job"],
};
</script>

<style lang="scss">
@import "../assets/css/main.scss";

.company-box {
  position: relative;
  padding: 49px 9px 32px 9px;
  background: var(--secondary-color);
  border-radius: 6px;
  max-width: 730px;
  margin: -14px auto 13px;

  @include mq(tablet) {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0;
    padding-right: 43px;
    margin-top: -42px;
  }

  .company-box-left {
    @include mq(tablet) {
      text-align: left;
      display: flex;
      flex-direction: row;
      gap: 40px;
      width: 70%;
    }
  }

  img {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translate(-50%, -50%);
    height: 50px;
    width: 50px;
    border-radius: 6px;

    @include mq(tablet) {
      position: initial;
      top: 0;
      left: 0;
      transform: initial;
      height: 140px;
      width: 140px;
      border-radius: 0;
      border-top-left-radius: 6px;
      border-bottom-left-radius: 6px;
    }
  }

  .company-box-details {
    @include mq(tablet) {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      justify-content: center;
      gap: 13px;
    }
  }

  h1 {
    font-size: 20px;
    font-weight: 900;
    text-align: center;
    color: var(--header-color);
  }

  p {
    font-size: 16px;
    font-weight: 300;
    color: #6e8098;
    text-align: center;
  }

  a {
    display: block;
    text-decoration: none;
    background: var(--secondary-btn-color);
    color: var(--primary-color);
    width: 147px;
    margin: 24px auto 0;
    padding: 16px 20px;
    border-radius: 6px;
    font-size: 16px;
    font-weight: 900;

    &:hover {
      background: var(--secondary-btn-color-hover);
    }

    @include mq(tablet) {
      margin: 0;
    }
  }
}

.main-box {
  background: var(--secondary-color);
  border-radius: 6px;
  padding: 40px 24px;
  max-width: 730px;
  margin: 0 auto;

  .main-box-header {
      @include mq(tablet) {
          display: flex;
          justify-content: space-between;
          align-items: center;
      }
  }

  .main-box-header-left {
      @include mq(tablet) {
          width: 70%;
      }
  }

  .jobPage-date-type {
    font-size: 16px;
    font-weight: 300;
    color: #6e8098;
    margin-bottom: 16px;

    span {
      font-size: 20px;
      font-weight: bold;
      display: inline-block;
      margin: 0 5px;
    }
  }
  .jobPage-title {
    font-size: 20px;
    font-weight: 900;
    margin-bottom: 17px;
    color: var(--header-color);

    a {
      text-decoration: none;
      color: var(--header-color);
    }
  }

  .jobPage-location {
    font-size: 14px;
    line-height: 18px;
    font-weight: 900;
    color: #5964e0;
  }

  .btn {
    margin-top: 32px;
    width: 100%;
    text-align: center;

    @include mq(tablet) {
        width: 141px;
        padding: 16px 28px;
    }
  }

  .job-desc {
    margin: 32px 0;
    font-size: 16px;
    font-weight: 400;
    color: var(--font-color);

    p,
    li {
      margin-bottom: 16px;
      line-height: 26px;
    }

    h1,
    h2,
    h3,
    h4 {
      font-size: 20px;
      color: var(--header-color);
      margin: 1em 0;
    }

    a {
      font-size: 16px;
      font-weight: 900;
      color: #5964e0;
      line-height: 1;
    }
  }
}

.apply-box {
  margin: 32px auto 40px;
  background: url("../assets/mobile/bg-pattern-detail-footer.svg");
  background-repeat: no-repeat;
  background-size: cover;
  color: white;
  padding: 32px;
  border-radius: 6px;
  max-width: 730px;

  a {
    color: white;
    font-weight: 900;
    line-height: 26px;
  }

  h2 {
    margin-bottom: 1em;
    color: white;
  }
}

.footer-box {
  background: var(--secondary-color);
  padding: 25px;

  a {
    text-align: center;

    @include mq(tablet) {
      margin-right: 0;
    }
  }

  .footer-box-container {
    max-width: 730px;
    margin: 0 auto;

    @include mq(tablet) {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
  }

  .footer-box-left {
    display: none;
    h1 {
      font-size: 20px;
      margin-bottom: 12px;
      color: var(--header-color);
    }
    p {
      font-size: 16px;
      color: #6e8098;
    }
    @include mq(tablet) {
      display: block;
    }
  }
}
</style>
