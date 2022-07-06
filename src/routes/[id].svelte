<script>
    export let id;
    export let page;

    const img_url = "https://image.tmdb.org/t/p/original";
    const api_key = "04c35731a5ee918f014970082a0088b1";
    const api_url = `https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=${api_key}&page=${page}`;
    let movie = {
        adult: null,
        backdrop_path: null,
        original_title: null,
        overview: null,
        release_date: null,
        vote_average: null,
        poster_img: null
    };
    let loading = false;
    async function loadMovie() {
        await fetch(api_url)
            .then((res) => res.json())
            .then((data) => {
                let results = data.results;
                results.forEach((result) => {
                    if (result.id == id) {
                        movie.adult = result.adult;
                        movie.backdrop_path = result.backdrop_path;
                        movie.original_title = result.original_title;
                        movie.overview = result.overview;
                        movie.release_date = result.release_date;
                        movie.vote_average = result.vote_average;
                        movie.poster_path = result.poster_path;
                    }
                });
            });
        loading = true;
    }
</script>

{#if !loading}
    <button on:click={loadMovie}>Load Movie</button>
{:else}
    <main style="background-image: url({img_url + movie.backdrop_path})">
        <div class="info">
            <img src={img_url + movie.poster_path} alt={movie.original_title}/>
            <h1>{movie.original_title} {movie.adult ? '18+' : ''}</h1>
            <span id="vote">{movie.vote_average}</span>
            <p>{movie.overview}</p>
            <br/>
            <span id="date">{movie.release_date}</span>
        </div>
    </main>
{/if}

<style>
    main {
        width: 100vw;
        height: 100%;
        position: fixed;
        top: 0;
        left: 0;
        background-position: bottom;
        background-size: cover;
        background-repeat: no-repeat;
        background-attachment: fixed;
    }
    .info {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%,-50%);
        border-radius: 15px;
        padding: 20px 15px;
        color: white;
        background-color: rgba(61, 73, 109, .4);
        margin: 0 auto;
    }
    .info p {
        max-width: 100ch;
        margin: 0 auto;
    }
    .info img {
        width: 50%;
        min-width: 150px;
        max-width: 250px;
        border-radius: 15px;
    }
    .info span {
        background-color: rgb(211, 130, 130);
        padding: 5px 10px;
        border-radius: 5px;
        position: absolute;
        top: 15px;
    }
    .info #vote {
        left: 15px;
    }
    .info #date {
        right: 15px;
    }
</style>
