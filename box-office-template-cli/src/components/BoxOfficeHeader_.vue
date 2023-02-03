<template>
    <header class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0 shadow">
        <a class="navbar-brand col-md-3 col-lg-2 me-0 px-3 fs-6" href="#">Company name</a>

        <button class="navbar-toggler position-absolute d-md-none collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#sidebarMenu" aria-controls="sidebarMenu" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <input class="form-control form-control-dark w-100 rounded-0 border-0" type="text" v-model="selectDate" placeholder="Search" aria-label="Search" v-on:keyup.enter="selectMovie">

        <div class="navbar-nav">
          <div class="nav-item text-nowrap">
            <a class="nav-link px-3" v-on:click="selectMovie" href="#">Search!!</a>
          </div>
        </div>
    </header>
</template>

<script>
import eventBus from './eventBus.js';
export default {
     data() {
        return {
            selectDate: '',
            }
     },
     methods: {
        selectMovie() {
            
            axios({

                url: 'https://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json',
                method: 'GET',
                params: {
                    key: 'a1f9efcab49f40a4d70f3cd3a99f77a7', targetDt: this.selectDate
                },
                responseType: 'json'

            }).then(function (result) {
                let movieList = result.data.boxOfficeResult.dailyBoxOfficeList;
                
                for (const idx in movieList) {
                    movieList[idx].poster = '';
                    axios({
                        url: 'https://dapi.kakao.com/v2/search/image',
                        method: 'GET',
                        headers: { Authorization: 'KakaoAK 28129ad995eebba2852f3ad70480cfaa' },
                        params: {
                            query: movieList[idx].movieNm
                        },
                        responseType: 'json'
                    }).then(function (result) {
                        let poster = result.data.documents[0].thumbnail_url;
                        movieList[idx].poster = poster;
                    })
                }
                eventBus.$emit('sendData', movieList, true);
                console.log('데이터 eventBus로 이동');
                this.selectDate = ''; //입력 칸 비우기
            }.bind(this));
        }

     }//End methods
}
</script>

<style>

</style>