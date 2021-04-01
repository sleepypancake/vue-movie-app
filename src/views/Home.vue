<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <img src="https://animego.org/upload/anime/images/5a3fbf0c1fd3c.jpg" 
        alt="Наруто" class="featured-img">
        <div class="detail">
          <h3>Наруто</h3>
          <p> Наруто грезит всю жизнь – стать Х
             окагэ – вождем деревни, что скрыта в листве. Много соперников встретит юнец, но это путь ниндзя! Путь Узумаки! Путь настоящего Хокагэ!</p>
        </div>
      </router-link>
    </div>
  </div>
</template>

<script>

export default {

}

</script>

<style lang="scss">
 .home {
   .feature-card {
     position: relative;
   }

   .featured-img {
     display: block;
     width: 100%;
     height: 300px;
     object-fit: cover;
     position: relative;
     z-index: 0;
   }

   .detail {
     position: absolute;
     left: 0;
     right: 0;
     bottom: 0;
     background-color: rgba(0, 0, 0, 0.6);
     padding: 16px;
     z-index: 1;
   }

   h3 {
     color: #fff;
     margin-bottom: 16px;
   }

   p {
     color: #fff;
   }
 }
</style>