<script>
	import CategoryPage from './CategoryPage.svelte';
	export let viewRecipes;
	export let categories=[]
	export let recipes=[];
	export let viewCategoriesPage=false;
	export let viewCategories=true;
	let results=[]	
	let category1="";
	async function setCategory(category){
		console.log(category)
		results = await recipes.filter((recipe)=>recipe["type"].toLowerCase().includes(category.toLowerCase()))
		category1=category
		viewCategories=false;
		viewRecipes=false;
		viewCategoriesPage=true;
	}
</script>
{#if viewCategories}
<div class="slider">
	<!-- svelte-ignore a11y-click-events-have-key-events -->
	<!-- svelte-ignore a11y-click-events-have-key-events -->
	{#each categories as category}
		<!-- svelte-ignore a11y-no-static-element-interactions -->
		<div class="glass-box" on:click={()=>{setCategory(category["name"])}}>
			<div class="glass-icon">
				<img src="{category["img"]}" alt="categoryImg">
      </div>
			<p class="titolo">{category["name"]}</p>
		</div>
	{/each}
</div>
{/if}

{#if results!=[] && viewCategoriesPage}
  <CategoryPage category={category1} results={results}/>
{/if}
<style>	
	.glass-box {
		background-color:#f08080;
    	border-radius:3rem;
		padding: 0;
		width: 17vw;
		height: 20vw;
		scroll-snap-align: start;
		text-align: center;
		position: relative;
		margin:5px;
	}
	.glass-box:hover {
		background-color: #f8ad9d;
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
		margin-top:1.5vw;
	}
	.slider {
		scroll-snap-type: x mandatory;	
		display: flex;
		-webkit-overflow-scrolling: touch;
		overflow-x: scroll;
	}
	/* width */
	::-webkit-scrollbar {
	width: 5vw;
	}

	/* Track */
	::-webkit-scrollbar-track {
	box-shadow: inset 0 0 5px grey; 
	border-radius: 1rem;
	}
	
	/* Handle */
	::-webkit-scrollbar-thumb {
	background: #f08080; 
	border-radius: 10px;
	}

	/* Handle on hover */
	::-webkit-scrollbar-thumb:hover {
	background: #f4978e; 
	}
</style>

