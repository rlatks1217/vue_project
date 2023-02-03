<template>
    <div>



      <BoxOfficeHeader></BoxOfficeHeader>
        <div class="container-fluid">


          <div class="row">
            <nav id="sidebarMenu" class="col-md-3 col-lg-2 d-md-block bg-light sidebar collapse">
              <div class="position-sticky pt-3 sidebar-sticky">
                <ul class="nav flex-column">
                  <li class="nav-item">
                    <a class="nav-link active" aria-current="page" href="#">
                      <span data-feather="home" class="align-text-bottom"></span>
                      날짜별 BoxOffice 순위
                    </a>
                  </li>
                </ul>
                
              </div>
            </nav>


            <main class="col-md-9 ms-sm-auto col-lg-10 px-md-4">
              
              <h2>영화순위</h2>
              <BoxOfficeBody></BoxOfficeBody>
                <Modal></Modal>
            </main>


          </div>
        </div>
    </div>
</template>

<script>
// import eventBus from './components/eventBus.js';
import BoxOfficeHeader from "./components/BoxOfficeHeader_.vue";
import BoxOfficeBody from "./components/BoxOfficeBody_.vue";
import Modal from "./components/Modal.vue";
export default {
  components: {
    BoxOfficeHeader,
    BoxOfficeBody,
    Modal
  }
}
</script>

<style>

</style>
