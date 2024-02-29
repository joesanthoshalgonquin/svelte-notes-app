<script lang="ts">
  import Modal from "@/components/Modal.svelte";
  import { createEventDispatcher } from "svelte";

  export let id: number | undefined = undefined;
  export let title: string | undefined = undefined;

  const dispatch = createEventDispatcher();
</script>

<Modal on:closeModal={() => dispatch("close")}>
  <div slot="title" class="deleteModal__title">Confirm Delete</div>
  <div slot="body" class="deleteModal__body">
    Are you sure you want to delete "{title}"?
  </div>
  <div slot="footer" class="deleteModal__footer">
    <button
      class="btn deleteBtn"
      on:click|stopPropagation={() => dispatch("delete", id)}
    >
      Delete
    </button>
    <button class="btn" on:click|stopPropagation={() => dispatch("close")}>
      Cancel
    </button>
  </div>
</Modal>

<style lang="scss">
  .deletModal {
    &__body {
      padding: 30px 15px;
      width: 330px;
    }

    &__footer {
      padding: 0 15px;
      text-align: right;

      .btn {
        height: 30px;
        padding: 0 10px;
        text-align: center;
        box-sizing: content-box;
        border-radius: 3px;
        border: 1px solid #000;

        &:active {
          background-color: #b9b7b7;
        }

        &.deleteBtn {
          background-color: #e81414;
          color: #fff;

          &:active {
            background-color: #b11111;
          }
        }
      }
    }
  }
</style>
