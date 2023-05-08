<template>
  <div class="about ">
    <div class="hero  is-info">
      <div class="hero-body notehome has-text-centered">
        <h1 class="title ">About</h1>
      </div>
    </div>

    <section class="section">
      THis is the about page
    </section>
  </div>
</template>

<script>
export default {
  mounted() {
    document.title = 'About | StudyNet'
  }
}
</script>

<style>
  .notehome {
      text-align: center;
   
      height: 80px;
      background: -webkit-linear-gradient(left, #24a0ed, #607d8b);
      color: #fff;
      font-weight: bold;
      line-height: 80px;
    }

</style>