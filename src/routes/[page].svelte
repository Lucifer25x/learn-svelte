<script>
    export let page;
    import Movie from "../components/Movie.svelte";
    const api_key = "04c35731a5ee918f014970082a0088b1";
    const api_url = `https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=${api_key}&page=${page}`;
    let movies = [];
    let loading = false;
    async function loadMovies() {
        await fetch(api_url)
            .then((res) => res.json())
            .then((data) => {
                let results = data.results;
                console.log(results)
                results.forEach(result => {
                    let movie = {
                        id: result.id,
                        img: result.backdrop_path,
                        title: result.title,
                        overview: result.overview,
                        poster_img: result.poster_path,
                        release_date: result.release_date,
                        vote_average: result.vote_average,
                        page: page
                    };
                    movies.push(movie);
                });
            });

        loading = true;
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

<a href={`/page/${page + 1}`}>Page {page + 1}</a>

<style>
    h1 {
        font-size: 3em;
        letter-spacing: 5px;
        color: white;
    }
    main {
        width: 80%;
        margin: 0 auto;
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
        margin-bottom: 15px;
    }
    button {
        margin: 10px auto;
    }
    a {
        font-size: 1.2em;
        color: white;
        font-weight: bold;
    }
</style>
