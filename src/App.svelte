<script lang="ts">
  import Header from "@/components/Header.svelte";
  import Home from "./pages/Home.svelte";
</script>

<Header />
<Home />

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    height: 100%;
  }
  :global(body) {
    /* this will apply to <body> */
    margin: 0;
    height: 100%;
    background-color: #fbfbfb;
  }
</style>
