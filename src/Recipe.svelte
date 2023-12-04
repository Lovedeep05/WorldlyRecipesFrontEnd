<script>

  import StarRating from "./StarRating.svelte";
  import RecipePage from "./RecipePage.svelte";

  export let recipes=[];
  

  /*function scroll(){
    const element = document.getElementById("recipePage");
    element.scrollIntoView();
  }*/

  let selectedRecipe = null;

  async function setRecipe(recipe){
    selectedRecipe=recipe;
    return ;
  }
  </script>

<div class="recipesBox">
	{#each recipes as recipe}
    <div class="glass-box">
    <div on:click={setRecipe(recipe)}>
			<div class="glass-icon" >
				<img src="{recipe["dishImage"]}" alt="dishImage">
      </div>
			<p class="titolo">{recipe["nameOfDish"]}</p>
      <p class="description">{recipe["description"]}</p>
    </div>
      <StarRating rating={recipe["rating"]}/>
		</div>
	{/each}
</div>

<div id="recipePage">
  {#await setRecipe()}
    <p>waiting selection</p>
  {:then recipe}
      <RecipePage recipe={selectedRecipe}/>
  {:catch error}
    <p>{error.message}</p>
  {/await}
</div>


<style>



.glass-box {
		background-color:#f08080;
    border-radius:3rem;
    padding: 0;
		width: 17vw;
		height: 27vw;
		scroll-snap-align: start;
		text-align: center;
		position: relative;
		margin:5px;
    overflow: hidden;
	}

.glass-box:hover {
  background-color: #f4978e;
}

	.glass-icon {
		border-radius: 30px 30px 0px 0px;
		width: 17vw;
		height: 15vw;
		overflow: hidden;
	}


  img {
    width: 17vw;
		height: 15vw;
    object-fit: cover;
    position: relative;
  }

.titolo {
  order:1;
  font-weight: bold;
  text-align: center;
  color: black;
}
.description{
  order:2;
  margin:0px;
}
.rating{
  order:3;
  margin:0px;

}

.recipesBox{
  display: flex;
  flex-wrap: wrap;
  justify-content:space-evenly;
  margin:20px;
}

</style>

