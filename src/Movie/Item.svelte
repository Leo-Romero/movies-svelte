<script>
  export let title, overview, poster_path

  $: coverURL = `https://image.tmdb.org/t/p/w185_and_h278_bestv2${poster_path}`
</script>

<div class="card">
  <img src={coverURL} class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">{title}</h5>
    <p class="card-text">{overview}</p>
    <div class="text-center">
      <button class="btn btn-primary">Votar</button>
    </div>
  </div>
</div>
