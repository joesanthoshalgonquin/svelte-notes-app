<script lang="ts">
  import logo from "@/assets/svelte.svg";
</script>

<header class="header">
  <div class="headerApp">
    <img src={logo} alt="Logo" class="logo" />
    <div class="headerApp__title">Notes App</div>
  </div>
</header>

<style lang="scss">
  .header {
    background-color: #313131;
    height: 56px;
    color: white;
    padding: 15px;
    box-sizing: border-box;

    .headerApp {
      display: flex;
      align-items: center;
      height: 100%;

      .logo {
        height: 100%;
        margin-right: 5px;
      }

      .title {
        font-weight: bold;
      }
    }
  }
</style>
