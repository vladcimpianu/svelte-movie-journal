<script lang="ts">
  import MovieInput from "./MovieInput.svelte";
  import MovieList from "./MovieList.svelte";
  import Search from "./Search.svelte";
  import type { Movie } from "./types";

  let movies: Movie[] = localStorage.getItem("movies")
    ? JSON.parse(localStorage.getItem("movies")!)
    : [];

  const submitMovie = (movie: Movie) => {
    const updatedMovies = [...movies, movie];
    localStorage.setItem("movies", JSON.stringify(updatedMovies));
    movies = updatedMovies;
  };

  const clearSearch = () => {
    movies = localStorage.getItem("movies")
      ? JSON.parse(localStorage.getItem("movies")!)
      : [];
  };

  const handleSearch = (searchTerm: string) => {
    const items = localStorage.getItem("movies")
      ? JSON.parse(localStorage.getItem("movies"))
      : [];

    movies = items.filter(({ title }) =>
      title.toLowerCase().includes(searchTerm.toLowerCase())
    );
  };
</script>

<svelte:head>
  <link
    rel="stylesheet"
    href="https://unpkg.com/mono-icons@1.0.5/iconfont/icons.css"
  />
</svelte:head>
<div class="main">
  <h1>Welcome to your movie journal!</h1>

  <Search
    on:search={(ev) => handleSearch(ev.detail.searchTerm)}
    on:clearSearch={clearSearch}
  />
  <MovieInput on:submitMovie={(ev) => submitMovie(ev.detail.movie)} />
  <MovieList {movies} />
</div>

<style>
  .main {
    width: 500px;
    max-width: 100%;
    padding: 1em;
    margin: auto;
    text-align: center;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }
</style>
