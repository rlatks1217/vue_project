<template>
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h1 class="modal-title fs-5" id="exampleModalLabel">{{detailMovie.movieNm}}{{"("+detailMovie.prdtYear+"년)"}}</h1>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <ul>
          <li>영어제목 : {{detailMovie.movieNmEn}}</li>
          <li v-for="name in detailMovie.directors" :key="name.peopleNm">감독 : {{name.peopleNm}}{{"("+name.peopleNmEn+")"}}</li>
          <li>상영시간 : {{detailMovie.showTm + "분"}}</li>
          <li v-for="nation in detailMovie.nations" :key="nation.nationNm">제작국가 : {{nation.nationNm}}</li>
          <li>유형 : {{detailMovie.typeNm}}</li>
          <li>출연진 : <span v-for="actor in detailMovie.actors" :key="actor.peopleNm">{{actor.peopleNm+" "}}</span></li>
          </ul>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        </div>
      </div>
    </div>
</div>
</template>
<script>
import eventBus from './eventBus.js';
export default {
    data() {
        return {detailMovie : {}}
    },
    created: function() {
        eventBus.$on('showModal', function(selectDetail) {
            this.detailMovie = selectDetail;
        }.bind(this));
    }
}
</script>

<style>

</style>