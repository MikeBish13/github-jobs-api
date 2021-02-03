<template>
    <div>
        <div class="job-card">
            <div class="job-img"><img v-bind:src="job.company_logo" /></div>
            <p class="job-date-type">{{ job.created_at | moment("from") }}  <span>.</span>  {{ job.type }}</p>
            <h1 class="job-title"><router-link :to="{ name: 'JobPage', params: {job}}">{{ job.title }}</router-link></h1>
            <p class="job-company">{{ job.company }}</p>
            <p class="job-location">{{ job.location }}</p>
    </div>
    </div>
</template>

<script>
export default {
    name: 'Job',
    props: ['job']
}
</script>

<style lang="scss">
@import '../assets/css/main.scss';

.job-card {
    list-style: none;
    margin: 0;
    padding: 0;
    position: relative;
    padding: 49px 32px 32px 32px;
    background: var(--secondary-color);
    margin-bottom: 49px;
    border-radius: 6px;
    min-height: 228px;

    li {
    margin: 0;
    padding: 0;
    }
}

.job-img {
    position: absolute;
    top: 0;
    transform: translateY(-50%);
}

.job-img > img {
    height: 50px;
    width: 50px;
    border-radius: 6px;
    object-fit: cover;
}

.job-date-type, .job-company {
    font-size: 16px;
    font-weight: 300;
    color: #6E8098;
    margin-bottom: 16px;
}

.job-date-type span {
    font-size: 20px;
    font-weight: bold;
    display: inline-block;
    margin: 0 5px;
}

.job-title {
    font-size: 20px;
    font-weight: 900;
    margin-bottom: 16px;

    a {
        text-decoration: none;
        color: var(--header-color);
    }
}

.job-location {
    font-size: 14px;
    line-height: 18px;
    font-weight: 900;
    color: #5964E0;
}


</style>