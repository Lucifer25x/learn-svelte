<script>
  const api_key = '04c35731a5ee918f014970082a0088b1';
  const api_url = 'https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=';
  const url = api_url + api_key;
  fetch(url)
    .then(res => res.json())
    .then(data => console.log(data))
</script>

<p>Hello World {url}</p>