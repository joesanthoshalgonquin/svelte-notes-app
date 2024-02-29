<script lang="ts">
  import moment from "moment";
  import { createEventDispatcher, onMount } from "svelte";
  import Modal from "@/components/Modal.svelte";
  import { formatDate } from "@/libs/utils";

  export let id: number | undefined = undefined;
  export let title: string | undefined = undefined;
  export let date: string | undefined = undefined;
  export let content: string | undefined = undefined;
  export let isFavorite: boolean | undefined = undefined;
  export let tags: string[] | undefined = undefined;

  let tagString = tags && tags.length ? tags.join(",") : "";

  $: canSave = Boolean(title && content);

  const dispatch = createEventDispatcher();

  const saveNote = () => {
    if (!canSave) return;

    const newMemo = {
      id,
      title,
      content,
      date: moment().format("YYYYMMDDHHmmss"),
      isFavorite,
      tags: tagString
        .replace(/\s/g, "")
        .split(",")
        .filter((item) => item),
    };

    if (!newMemo.id) {
      newMemo.id = moment().valueOf();
    }

    dispatch("save", newMemo);
  };

  let textArea: HTMLElement;

  const onInput = () => {
    if (textArea) {
      textArea.style.height = "auto";
      textArea.style.height = `${textArea.scrollHeight}px`;
    }
  };

  onMount(() => {
    onInput();
  });
</script>

<Modal on:closeModal={() => dispatch("close")}>
  <div class="modalTitle" slot="title">{id ? "Edit" : "Create"} Post</div>
  <div class="modalBody" slot="body">
    <label for="title" class="modalBody__label">Title: </label>
    <input type="text" class="modalBody__input" id="title" bind:value={title} />
    <label for="tags" class="modalBody__label">Tags: </label>
    <input
      type="text"
      class="modalBody__input"
      id="tags"
      bind:value={tagString}
    />
    <label for="content" class="modalBody__label">Content: </label>
    <textarea
      class="modalBody__input"
      id="content"
      bind:value={content}
      bind:this={textArea}
      on:input={onInput}
    ></textarea>
    {#if date}
      <div class="modalBody__label">Last Updated:</div>
      <div class="modalBody__text">{formatDate(date)}</div>
    {/if}
  </div>
  <div slot="footer" class="modalFooter">
    <div class="modalFooter__deleteWrapper">
      {#if id}
        <button
          class="deleteBtn btn"
          on:click|stopPropagation={() => dispatch("delete", id)}
        >
          Delete
        </button>
      {/if}
    </div>
    <div class="modalFooter__buttonsWrapper">
      <button
        class="saveBtn btn {canSave ? 'disabled' : ''}"
        on:click|stopPropagation={saveNote}>Save</button
      >
      <button
        class="cancelBtn btn"
        on:click|stopPropagation={() => dispatch("close")}
      >
        Cancel
      </button>
    </div>
  </div>
</Modal>

<style lang="scss">
  .modalBody {
    width: 700px;
    padding: 20px 15px 10px;
    display: grid;
    grid-template-columns: 1fr 3fr;
    gap: 15px 0;

    &__label {
      grid-column: 1;
      line-height: 30px;
    }

    &__input {
      grid-column: 2;
      height: 30px;
      border-radius: 5px;
      border: 1px solid #c3c3c3;
    }

    &__text {
      height: 30px;
      color: #808080;
      display: flex;
      align-items: center;
    }
  }

  .modalFooter {
    padding: 0 15px;
    display: grid;
    grid-template-columns: 1fr 1fr;

    &__buttonsWrapper {
      height: 30px;
      padding: 0 10px;
      text-align: center;
      box-sizing: content-box;
      border-radius: 3px;
      border: 1px solid #000;

      &:active {
        background-color: #b9b7b7;
      }

      .saveBtn {
        background-color: #1dbd73;
        color: #fff;

        &:active {
          background-color: #1a8e56;
        }

        &.disabled {
          opacity: 0.5;

          &:active {
            background-color: #1dbd73;
          }
        }
      }

      .deleteBtn {
        background-color: #e81414;
        color: #fff;

        &:active {
          background-color: #b11111;
        }
      }
    }
  }

  #content {
    resize: vertical;
    height: fit-content;
    min-height: 30px;
  }
</style>
