<script lang="ts">
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  let searchTerm: string = "";

  const onSearch = (event) => {
    searchTerm = event.target.value;
    if (searchTerm) {
      dispatch("search", {
        searchTerm,
      });
    } else {
      dispatch("clear", {});
    }
  };
</script>

<div>
  <input
    type="text"
    placeholder="Search Movie"
    value={searchTerm}
    on:keyup={onSearch}
  />
</div>

<style>
  div {
    width: 100%;
    margin-bottom: 32px;
  }

  input {
    width: 100%;
    margin-bottom: 16px;
  }
</style>
