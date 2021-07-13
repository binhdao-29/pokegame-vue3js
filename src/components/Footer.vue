<template>
  <div class="footer-container">
    <div class="subheading">
      The Pokemon Mememories games by BinhChan
      <a href="https://www.facebook.com/phanhhh1910" target="_blank"
        >View more
      </a>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss">
.footer-container {
  margin-top: 3rem;
  margin-bottom: 1rem;

  @media screen and (min-width: 576px) {
    position: absolute;
    bottom: 0;
  }

  .subheading {
    font-size: 1.5rem;
  }

  a {
    color: #f4dc26;
  }
}
</style>
