<script>
  import { Router, Route } from "svelte-routing";
  import Page from "./routes/[page].svelte";
  import Movie from "./routes/[id].svelte";
  export let url = "";
</script>

<Router {url}>
  <div>
    <Route path="page/:id" let:params>
      <Page page={parseInt(params.id)} />
    </Route>
    <Route path="movies/:page/:id" let:params>
      <Movie page={params.page} id={parseInt(params.id)}/>
    </Route>
    <Route path="/">
      <Page page={1}/>
    </Route>
  </div>
</Router>
