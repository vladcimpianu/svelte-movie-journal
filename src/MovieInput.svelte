<script lang="ts">
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  let title = "";
  let rating = 1;

  const onTitleChange = (e) => {
    title = e.target.value;
  };

  const onRatingSelect = (e) => {
    rating = e.target.value;
  };

  const onSubmit = () => {
    if (title) {
      dispatch("submitMovie", {
        movie: {
          title,
          rating,
        },
      });
      title = "";
      rating = 1;
    }
  };
</script>

<div class="main">
  <input
    placeholder="Movie Title"
    type="text"
    value={title}
    on:keyup={onTitleChange}
  />

  <!-- svelte-ignore a11y-no-onchange -->
  <select value={rating} on:change={onRatingSelect}>
    <option value={1}>1</option>
    <option value={2}>2</option>
    <option value={3}>3</option>
    <option value={4}>4</option>
    <option value={5}>5</option>
  </select>

  <button on:click={onSubmit} disabled={!title}>Submit</button>
</div>

<style>
  .main {
    width: 100%;
    display: flex;
    margin-bottom: 32px;
  }

  .main input {
    width: 50%;
    height: 32px;
  }

  .main select {
    width: 25%;
    margin: 0 10px;
    height: 32px;
  }

  .main button {
    width: 25%;
    height: 32px;
  }
</style>
