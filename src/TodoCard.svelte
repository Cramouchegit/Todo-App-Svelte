<script>
  import { createEventDispatcher } from "svelte";
  import { slide } from "svelte/transition";
  export let content, listName, index;

  const dispatch = createEventDispatcher();

  function handleDeleteCard() {
    dispatch("deleteCard", { index });
  }

  function handleMoveRight() {
    dispatch("moveRight", { index });
  }

  function handleMoveLeft() {
    dispatch("moveLeft", { index });
  }
</script>

<div class="card mb-3 has-background-primary-light" transition:slide>
  <div class="card-content">
    <div class="columns is-mobile">
      <div class="column is-narrow">
        {#if listName != "Tasks"}
          <span class="icon has-text-primary" on:click={handleMoveLeft}>
            <i class="fa fa-chevron-left"></i>
          </span>
        {/if}
      </div>
      <div class="column">
        <p class="content">{content}</p>
      </div>
      <div class="column is-narrow" on:click={handleDeleteCard}>
        <span class="icon has-text-danger">
          <i class="fa fa-trash"></i>
        </span>
      </div>
      <div class="column is-narrow">
        {#if listName != "Done"}
          <span class="icon has-text-primary" on:click={handleMoveRight}>
            <i class="fa fa-chevron-right"></i>
          </span>
        {/if}
      </div>
    </div>
  </div>
</div>

<style>
  .card {
    padding: 1rem;
  }

  .icon {
    cursor: pointer;
  }

  @media (max-width: 768px) {
    .card {
      padding: 0.8rem;
    }
    .icon {
      font-size: 1.2rem;
    }
  }

  @media (max-width: 480px) {
    .card {
      padding: 0.5rem;
    }
    .icon {
      font-size: 1rem;
    }
  }
</style>
