<script>
    import Recipe from "./Recipe.svelte";
    export let recipes;
    export let searchTerm="";
</script>
<div class=main>
    <h1>Results:</h1>
    {#if recipes!=undefined}
    <Recipe recipes={recipes}/>
    {/if}
</div>
<style>
.main{
    padding: 0px;
    border-radius: 10px;
    width: 100%;
    height: auto;
    background: #f8ad9d;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  
</style>