<script>

  import Header from './Header.svelte';
  import HomePage from './HomePage.svelte';
  
  import Footer from "./Footer.svelte";



  let data;
  async function getData(){
    const response = await fetch('https://raw.githubusercontent.com/Lovedeep05/svelteDataset-Assets/main/dataset.json?token=GHSAT0AAAAAACKY3BCVH7OQON5UOORAMLH2ZLCPINQ');
    let data = await response.json();
    console.log(data)
    if (response.ok) {
			return data;
		} else {
			throw new Error("errore nella richiesta");
		}
  }
  data = getData();


  let viewProfile = false;
  let viewHomePage = true;
  let viewLoginPage = false;
  let viewSignupPage = false;
  let viewSearchPage = true;
  let viewRecipes=true;
  let viewCategoriesPage=false;
  let viewCategories;
  let viewBanner=true;

  let loginStatus = 1;
  let searchTerm ="";

</script>


{#await getData()}

	<p>Fetching resources</p>
{:then data}
    <Header bind:viewBanner={viewBanner} bind:viewCategoriesPage={viewCategoriesPage} bind:viewCategories={viewCategories} bind:viewRecipes={viewRecipes} bind:viewProfile={viewProfile} bind:viewHomePage={viewHomePage} bind:searchTerm={searchTerm} loginStatus={loginStatus} data={data}/>
  {#if viewHomePage}
    <HomePage bind:viewBanner={viewBanner} bind:viewRecipes={viewRecipes} bind:viewCategories={viewCategories} bind:viewCategoriesPage={viewCategoriesPage} bind:viewHomePage={viewHomePage} data={data}/>
  {/if}
{:catch error}
	<p>{error.message}</p>
{/await}
<Footer/>

<style>
</style>