<script lang="ts">
  import Fa from "svelte-fa";
  import { faTimes } from "@fortawesome/free-solid-svg-icons";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
</script>

<div class="modalOverlay">
  <div class="modal">
    <div class="modalHeader">
      <slot name="title" />
      <!-- svelte-ignore a11y-click-events-have-key-events -->
      <!-- svelte-ignore a11y-no-static-element-interactions -->
      <div
        class="modalHeader__closeIcon"
        on:click={() => dispatch("closeModal")}
      >
        <Fa icon={faTimes} color="#afaeae" size="1x" />
      </div>
    </div>
    <slot name="body" />
    <slot name="footer" />
  </div>
</div>

<style lang="scss">
  .modalOverlay {
    position: absolute;
    top: 0;
    height: 100vh;
    width: 100vw;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: rgb(0, 0, 0, 0.4);

    .modal {
      background-color: white;
      padding: 15px 0;
      border-radius: 10px;
      box-shadow: rgb(0 0 0 / 24%) 0px 3px 8px;

      &Header {
        display: flex;
        justify-content: space-between;
        padding: 0 15px 10px;
        border-bottom: 3px solid #e2e2e2;

        &__closeIcon {
          cursor: pointer;
        }
      }
    }
  }
</style>
