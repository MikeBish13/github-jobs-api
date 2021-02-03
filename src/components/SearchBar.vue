<template>
    <div>
        <form @submit="startSearch" class="form-container container">
            <div class="primary-search">
                <input type="text" v-model="title" class="title-input" name="title" placeholder="Filter by title, companies, expertise...">
                <div class="title-icons">
                <svg v-on:click="showLocationBar" class="filter" width="24" height="24" xmlns="http://www.w3.org/2000/svg"><path d="M19.108 0H.86a.86.86 0 00-.764.455.833.833 0 00.068.884l6.685 9.202.007.01c.242.32.374.708.375 1.107v7.502a.825.825 0 00.248.594.865.865 0 00.942.18l3.756-1.4c.337-.1.56-.41.56-.784v-6.092c0-.399.132-.787.375-1.108l.007-.009 6.685-9.202c.19-.26.217-.6.068-.884A.86.86 0 0019.108 0z" fill="#6E8098" fill-rule="nonzero"/></svg>
                <button class="search-icon" @click="startSearch"><svg width="20" height="20" xmlns="http://www.w3.org/2000/svg"><path d="M17.112 15.059h-1.088l-.377-.377a8.814 8.814 0 002.15-5.784A8.898 8.898 0 008.898 0 8.898 8.898 0 000 8.898a8.898 8.898 0 008.898 8.899c2.211 0 4.23-.808 5.784-2.143l.377.377v1.081l6.845 6.832 2.04-2.04-6.832-6.845zm-8.214 0A6.16 6.16 0 118.9 2.737a6.16 6.16 0 010 12.322z" fill="#fff" fill-rule="nonzero"/></svg></button>
                </div>
            </div>
            <div class="secondary-search">
                <input type="text" v-model="location" class="location-input" name="location" placeholder="Filter by location">
                <div v-if="windowSize"><input class="fullTime-check" type="checkbox" v-model="fullTime" name="fullTime" id="job-type"><label class="fullTime-label" for="job-type">Full Time Only</label></div>
                <div v-else><input class="fullTime-check" type="checkbox" v-model="fullTime" name="fullTime" id="job-type"><label class="fullTime-label" for="job-type">Full Time</label></div>
                <input v-on:click="startSearch" class="btn btn-primary" type="submit" value="Search">
            </div>
        </form>
    </div>
</template>

<script>
export default {
    name: 'SearchBar',
    data() {
        return {
            title: '',
            location: '',
            fullTime: false,
            windowSize: window.innerWidth < 700
        }
    },
    methods: {
        startSearch(e) {
            const searchTerms = {
                title: this.title,
                location: this.location,
                fullTime: this.fullTime
            }
            e.preventDefault();
            this.$emit('start-search', searchTerms);
            this.title = '';
            this.location = '';
            if (e.target.value == 'Search' && window.innerWidth < 700) {
                this.showLocationBar();
            }  
        },
        showLocationBar: function() {
        let searchBox = document.querySelector('.secondary-search');
        searchBox.style.visibility == 'visible' ? searchBox.style.visibility = 'hidden' : searchBox.style.visibility = 'visible';
        let bgWrapper = document.querySelector('.wrapper');
        bgWrapper.style.display == "block" ? bgWrapper.style.display = 'none' : bgWrapper.style.display = "block";
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../assets/css/main.scss';

.form-container {
    @include mq(tablet) {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin: -30px auto 57px;
    }

    @include mq(desktop) {
        margin-bottom: 80px;
    }
}

.primary-search {
    height: 80px;
    width: 100%;
    border-radius: 6px;
    margin: -30px auto 57px;
    display: block;
    background: var(--secondary-color);
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 24px 16px 16px 16px;

    @include mq(tablet) {
        width: 30%;
        margin: 0;
        border-radius: 0px;
        border-top-left-radius: 6px;
        border-bottom-left-radius: 6px;
        padding: 0;
        border-right: 1px solid #6e809838;
    }

     @include mq(desktop) {
        width: 40%;
    }
}

.title-input {
    border: none;
    font-size: 16px;
    width: 60%;
    outline: transparent;
    color: #19202D;
    background: var(--secondary-color);

    @include mq(tablet) {
        width: 100%;
        height: 90%;
        margin-right: 0;
        padding: 0 24px 0 64px;
        background-image: url('../assets/desktop/icon-search.svg');
        background-repeat: no-repeat;
        background-position: 8% 50%;
    }

}

.title-input::placeholder {
    color: var(--font-color);
}

.title-icons {
    display: flex;
    justify-content: space-between;
    align-items: center;

    @include mq(tablet) {
        display: none;
    }
}

.filter {
    cursor: pointer;
}

.search-icon {
    cursor: pointer;
    margin-left: 24px;
    width: 48px;
    height: 48px;
    border: none;
    outline: transparent;
    background: #5964E0;
    border-radius: 6px;

    &:hover {
        background: #939BF4;
    }
}

.secondary-search {
    visibility: hidden;
    z-index: 50;
    position: absolute;
    top: 249px;
    width: 87%;
    height: 217px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 0 24px 24px 24px;
    border-radius: 6px;
    background: var(--secondary-color);

    @include mq(tablet) {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        visibility: visible !important;
        position: relative;
        top: 0;
        width: 70%;
        height: 80px;
        padding: 0;
        padding-right: 16px;
        border-radius: 0;
        border-top-right-radius: 6px;
        border-bottom-right-radius: 6px;
    }

     @include mq(desktop) {
        width: 60%;
    }
}

.location-input {
    background: url('../assets/desktop/icon-location.svg');
    background-repeat: no-repeat;
    background-position: left;
    height: 72px;
    outline: transparent;
    border: none;
    padding-left: 33px;
    font-size: 16px;
    color: #19202D;
    border-bottom: 1px solid #6E8098;
    margin-bottom: 24px;
    width: 100%;

    &::placeholder {
        color: var(--font-color);
    }

    @include mq(tablet) {
        border-bottom: none;
        padding: 0;
        margin: 0;
        border-right: 1px solid #6e809838;
        height: 100%;
        width: 50%;
        padding-left: 60px;
        background-position: 5% 50%;
    }
}


label {
    font-size: 16px;
    font-weight: 900;
    color: var(--header-color);
    position: relative;
    padding-left: 42px;
    margin-bottom: 24px;

    @include mq(tablet) {
        margin: 0;
        padding-left: 30px;
    }
}

input[type=checkbox] {
    visibility: hidden;
    height: 0;
    width: 0;
}

label::after {
    content: '';
    height: 24px;
    width: 24px;
    display: block;
    border-radius: 3px;
    border: none;
    cursor: pointer;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    left: 0;
    background: #c0c0c0;
}

input[type=checkbox]:checked + label::after {
        background-image: url('../assets/desktop/icon-check.svg');
        background-repeat: no-repeat;
        background-position: center;
        background-size: 12px 9px;
        background-color: #5964E0;
        
}

.btn {
    width: 100%;

    @include mq(tablet) {
        padding: 14px 16px;
        width: 80px;
        margin: 0;
    }
}


</style>