<script lang="ts">
  import Fa from "svelte-fa";
  import { faStar } from "@fortawesome/free-solid-svg-icons";
  import { createEventDispatcher } from "svelte";
  import { formatDate } from "@/libs/utils";

  export let id: number;
  export let title: string;
  export let content: string;
  export let date: string;
  export let isFavorite: boolean;
  export let tags: string[];

  const dispatch = createEventDispatcher();

  const trimContent = (content: string): string => {
    if (content.length > 100) {
      return `${content.substring(0, 100)}...`;
    }

    return content;
  };
</script>

<div class="note">
  <div class="noteTitle">{title}</div>
  <div class="ntoePreview">{trimContent(content)}</div>
  <div class="noteTag">
    {#each tags as tag (tag)}
      <div class="noteTag__title">{tag}</div>
    {/each}
  </div>
  <div class="noteFooter">
    <div class="noteFooter__date">{formatDate(date)}</div>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <div
      class="noteFooter__favIcon"
      on:click|stopPropagation={() => dispatch("toggleFavorite", id)}
    >
      <Fa icon={faStar} color={isFavorite ? "#ffda00" : "#afaeae"} />
    </div>
  </div>
</div>

<style lang="scss">
  .note {
    width: 150px;
    height: 195px;
    margin-right: 15px;
    background-color: #fff;
    padding: 15px;
    border-radius: 10px;
    box-shadow: rgb(0 0 0 / 24%) 0px 3px 8px;
    display: grid;
    grid-template-rows: 1fr 4fr 2fr 1fr;

    .noteTitle {
      font-weight: bold;
      margin-bottom: 10px;
    }

    .notePreview {
      font-size: 15px;
      word-break: break-word;
    }

    .noteTag {
      display: flex;
      align-items: flex-end;
      flex-wrap: wrap;

      &__title {
        background-color: #d6d2d2;
        padding: 2px 10px;
        border-radius: 20px;
        font-size: 12px;
        margin-right: 5px;
        height: 15px;
      }
    }

    .noteFooter {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;

      &__date {
        color: #afaeae;
        font-size: 14px;
      }

      &__favIcon {
        cursor: pointer;
      }
    }
  }
</style>
