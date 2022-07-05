<script>
  import Movie from "../components/Movie.svelte";
  const api_key = "04c35731a5ee918f014970082a0088b1";
  let page = 1;
  const api_url =
    `https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=${api_key}`;
  let movies = [];
  let loading = false;
  async function loadMovies() {
    await fetch(api_url + `&page=${page}`)
      .then((res) => res.json())
      .then((data) => {
        let results = data.results;
        results.forEach((result) => {
          let movie = {
            id: result.id,
            img: result.backdrop_path,
            title: result.title,
            overview: result.overview,
            poster_img: result.poster_path,
            release_date: result.release_date,
            vote_average: result.vote_average,
          };
          movies.push(movie);
        });
      });

    loading = true;
  }

  function loadMore(){
    page += 1;
    loading = false;
    loadMovies();
  }
</script>

<h1>Movies App</h1>
<main>
  {#if loading}
    {#each movies as movie}
      <Movie data={movie} />
    {/each}
  {:else}
    <button on:click={loadMovies}>Load Movies</button>
  {/if}
</main>
{#if loading}
<button on:click={loadMore}>Load More Movies</button>
{/if}

<style>
  h1 {
    font-size: 3em;
    letter-spacing: 5px;
    text-align: center;
    color: white;
  }
  main {
    width: 80%;
    margin: 0 auto;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
  }
  button {
    margin: 10px auto;
  }
</style>
