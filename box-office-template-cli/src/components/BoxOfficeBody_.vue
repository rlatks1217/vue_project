<template>
    <div class="table-responsive">
        <table class = "col-md-9 ms-sm-auto col-lg-10 px-md-4" style="margin-left:0!important; width: 1200px">
    <thead>
    <tr>
    <th scope="col">CHECK</th>
    <th scope="col">순위</th>
    <th scope="col">포스터</th>
    <th scope="col">영화제목</th>
    <th scope="col">관람객수</th>
    <th scope="col">개봉일</th>
    <th scope="col">삭제</th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="(movie, i) in movieData" v-bind:key="i">
    <td><input type="checkbox" v-model="checked[i]" /></td>
    <td>{{movie.rank}}</td>
    <td><img v-bind:src="movie.poster" /></td>
    <td>
    <a v-on:click="movieDetail(movie.movieCd)" data-bs-toggle="modal" data-bs-target="#exampleModal" href="#myModal">{{movie.movieNm}}</a>
    </td>
    <td>{{movie.audiCnt}}</td>
    <td>{{movie.openDt}}</td>
    <td ><button class="btn btn-danger" v-on:click="deleteMovie(movie.rnum)">삭제</button></td>
    </tr>
    </tbody>
    <button v-on:click="selectAndDelete" class="btn btn-warning" v-show="showButton">선택 삭제</button>
    </table>
    </div>
</template>
<script>
import eventBus from './eventBus.js';
export default {
    data() {
        return {
            movieData: [],
            checked: Array(10),
            showButton: false
            }
    },
    methods: {
        //선택 삭제
        selectAndDelete() {
            for (let i = 0; i < this.checked.length; i++) {
                if (this.checked[i] == true) {
                    this.movieData.splice(i, 1);
                    this.checked.splice(i, 1);
                    i--;
                }
            }
        },
        //행 삭제
        deleteMovie(rnum) {
            this.checked.splice(rnum - 1, 1); //해당 행의 체크값 삭제
            this.movieData.splice(rnum - 1, 1); //해당 행 삭제
        },
        //modal에 출력할 정보 검색
        movieDetail(movieCode) {
            axios({
                url: 'http://www.kobis.or.kr/kobisopenapi/webservice/rest/movie/searchMovieInfo.json',
                method: 'GET',
                params: {
                    key: 'a1f9efcab49f40a4d70f3cd3a99f77a7', movieCd: movieCode
                },
                responseType: 'json'
            }).then(function (result) {
                let movieDetail = result.data.movieInfoResult.movieInfo;
                console.log(movieDetail);
                eventBus.$emit('showModal', movieDetail);
            })
        }
    },
    created: function(){
        //검색 성공 후 rendering
        eventBus.$on('sendData',function(movieList, show) {
            this.movieData = movieList;
            this.showButton = show;
        }.bind(this));
        //this = eventBus / this가 이 component가 되도록 binding
    }
}
</script>

<style>

</style>