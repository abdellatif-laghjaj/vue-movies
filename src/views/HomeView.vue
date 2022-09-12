<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0388629">
        <img class="featured-image"
          src="https://w0.peakpx.com/wallpaper/525/657/HD-wallpaper-one-piece-brook-one-piece-chopper-predator-franky-one-piece-jinbe-one-piece-monkey-d-luffy-nami-one-piece-nico-robin-roronoa-zoro-sanji-one-piece-usopp-one-piece.jpg"
          alt="One piece">
        <div class="detail">
          <h3>One Piece</h3>
          <p>
            Follows the adventures of Monkey D. Luffy and his pirate crew in order to find the greatest treasure ever
            left by the legendary Pirate, Gold Roger. The famous mystery treasure named One Piece.
          </p>
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
  .home{
    .feature-card{
      position: relative;

      .featured-image{
        display: block;
        width: 100%;
        height: 300px;
        object-fit: cover;
        position: relative;
        z-index: 0;
      }
    }
  }
</style>