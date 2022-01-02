<script lang="ts">
  import type { Movie } from "./types";

  export let movies: Movie[];
</script>

{#each movies as movie (movie.title)}
  <div class="movie">
    <h3>{movie.title}</h3>
    <p>Your rating: {movie.rating}</p>
  </div>
{/each}

<style>
  .movie {
    text-align: left;
    border-bottom: 1px solid black;
  }
</style>
