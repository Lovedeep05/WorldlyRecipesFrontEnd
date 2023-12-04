<script>
    import Recipe from "./Recipe.svelte";
    export let category;
    export let results=[];
    console.log(results)
  </script>
  
  
  
    {#if results != undefined && results!=[]}
        <h1 style={"display:flex; justify-content:center"}>{category}</h1>
        <Recipe recipes={results}/>
    {/if}
    
    
    <style>
    </style>
    