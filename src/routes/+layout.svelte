<script>
  import "../app.postcss";
</script>

<slot />

<style>
  @import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@400&display=swap");

  :global(body) {
    font-family: "Montserrat", sans-serif;
    background-image: radial-gradient(circle at top right, #ff0080 -2000rem, #131316);
    background-repeat: no-repeat;
    background-size: cover;
    background-attachment: fixed;
    color: #fff;
  }
</style>
