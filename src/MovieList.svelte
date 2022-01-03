<script lang="ts">
  import type { Movie } from "./types";

  export let movies: Movie[];

  const handleDeleteMovie = (title: string) => {
    const updatedMovies = movies.filter((movie) => movie.title !== title);
    localStorage.setItem("movies", JSON.stringify(updatedMovies));
    movies = updatedMovies;
  };
</script>

{#each movies as movie (movie.title)}
  <div class="movie">
    <h3>
      <button on:click={() => handleDeleteMovie(movie.title)}>
        <i class="mi mi-delete icon" />
      </button>
      {movie.title}
    </h3>
    <p class="rating">Your Rating: {movie.rating}</p>
  </div>
{/each}

<style>
  h3 {
    align-items: center;
    justify-content: center;
    justify-items: center;
    text-transform: uppercase;
    font-weight: 200;
    color: #ff3e00;
  }
  button {
    padding: 0;
    border: none;
    background: inherit;
    cursor: pointer;
  }
  .movie {
    display: space-between;
    flex-direction: row;
    text-align: left;
    border-bottom: 1px solid black;
    align-items: center;
  }

  .icon {
    padding: 8px;
    color: red;
    width: 48px;
    height: 48px;
  }

  .rating {
    margin-left: 38px;
  }
</style>
