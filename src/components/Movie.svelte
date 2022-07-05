<script>
    const img_url = 'https://image.tmdb.org/t/p/original';
    export let data;

    function readMore(){
        alert(data.overview)
    }
</script>

<div>
    <img src={img_url + data.poster_img} alt={data.title}>
    <h2>{data.title}</h2>
    {#if data.overview.length > 200}
        <p>{data.overview.slice(0,200)}...</p>
        <span on:click={readMore}>Read More</span>
    {:else}
        <p>{data.overview}</p>
    {/if}
</div>

<style>
    div {
        width: 200px;
        display: flex;
        flex-direction: column;
        text-align: center;
        align-items: center;
        padding: 10px;
        background-color: rgb(61, 73, 109);
        padding: 15px;
        margin-top: 20px;
        margin-left: 15px;
        border-radius: 15px;
        box-shadow: 0 0 10px rgba(0,0,0,.5);
        transition: .3s ease all;
        cursor: pointer;
        color: #eee;
    }
    div:hover {
        transform: translateY(-10px);
        background-color: rgb(44, 53, 80);
        transition: .3s ease all;
    }
    img {
        width: 150px;
        border-radius: 15px;
    }
    h2 {
        font-size: 1.2em;
    }
    p {
        font-size: .8em;
    }
    span {
        color: rgb(199, 132, 132);
        text-decoration: underline;
        font-weight: bold;
    }
    span:hover {
        color: rgb(163, 105, 105);
    }
</style>