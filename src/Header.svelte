<script>
  import Login from "./Login.svelte";
  import Recipe from "./Recipe.svelte";
  import Search from "./Search.svelte";
  import Profile from "./Profile.svelte";

  export let data={};
  export let viewHomePage;
  export let viewProfile = false;
  export let loginStatus = 1;
  export let searchTerm="";
  export let viewCategoriesPage=false;
  export let viewRecipes= true;
  export let viewCategories=true;
  export let viewBanner=true;


  let user;

  let searchToggle=true;


  let viewSearchPage = false;
  let viewLoginPage = false;

  console.log(loginStatus);

  const setTrue = ()=>{
    console.log("profile:"+viewProfile)
    viewProfile=true;
    viewHomePage=false;
    console.log(viewHomePage)
  }
  let results=[];
  async function startSearchComponent(){
    results=[];
    let recipes=data["Recipes"];
    results = await recipes.filter((recipe)=>recipe["nameOfDish"].toLowerCase().includes(searchTerm.toLowerCase()) &&searchTerm!="")
    console.log(results)
    return results;
  }

  function searchToggleF(){
    if(searchTerm=="")
      searchToggle=!searchToggle
    if(!searchToggle && searchTerm!=""){
      startSearchComponent()
      searchTerm = ""
      viewSearchPage=true;
      viewProfile=false;
      viewHomePage=false;
      console.log(viewHomePage)
    }
  }

  function vHomePage(){
    viewHomePage=true;
    viewProfile=false;
    viewLoginPage=false;
    viewSearchPage=false;
    viewRecipes=true;
    viewCategoriesPage=false;
    viewCategories=true;  
  }

  function vRecipes(){
    viewHomePage=true;
    viewBanner=false;
    viewProfile=false;
    viewLoginPage=false;
    viewSearchPage=false;
    viewRecipes=true;
    viewCategoriesPage=false;
    viewCategories=false;  
  }

</script>


<div class="header flexbox">
  <img class="logo" src="images/logo.webp" alt="logo" on:click={()=>vHomePage()} style={"border-radius:1rem"}/>
  <h1 on:click={()=>vHomePage()}>Worldly Recipes</h1>

  <div class="align-right flexbox">
    <a style={"font-weight: bold;"} on:click={()=>vRecipes()} >RECIPES</a>
    <div class="divider"></div>
    <a style={"font-weight: bold;"} target="_blank" href="https://instagram.com/lovedeep.25" >HOLIDAY</a>
    <div class="divider"></div>
    <a style={"font-weight: bold;"} target="_blank" href="https://instagram.com/lovedeep.25" >INGREDIENTS</a>
    <div class="divider"></div>
    <a style={"font-weight: bold;"} target="_blank" href="https://instagram.com/lovedeep.25" >ABOUT US</a>
    <div class="divider"></div>
  </div>
  
  
  {#if loginStatus==0 && searchToggle}
    <p style={"font-weight: bold;"} on:click={()=> setTrue() }>@{user["user"]}</p>
    <img class="profilePic" src={user["profilePicture"]} alt="profilePic" on:click={()=> setTrue() }/>
  {/if}
  {#if loginStatus!=0 && searchToggle}
    <button class="button-5" on:click={()=>{viewLoginPage=true;viewHomePage=false;}}>LOGIN</button>
  {/if}
  <form on:submit|preventDefault={()=>{searchToggleF()}}>
    {#if !searchToggle}
      <input type="text" name="searchTerm" bind:value={searchTerm}>
    {/if}
    <button class="button-5">&#x1F50E;&#xFE0E;</button>
  </form>
</div>

{#await startSearchComponent()}
	<p>Fetching resources</p>
{:then}
  {#if viewSearchPage}
    <Search recipes={results} searchTerm={searchTerm}/>
  {/if}
{/await}

{#if viewLoginPage && (loginStatus==1 || loginStatus==2)}
  <Login bind:loginStatus={loginStatus} bind:user={user} bind:viewHomePage={viewHomePage} users={data["Users"]}/>
{/if}

{#if viewProfile}
  <Profile recipes={data["Recipes"]} users={data["Users"]} user={user}/>
{/if}


<style>
  input{
    border: 3px solid #f08080;
    border-radius: 1rem;
    height: 50px;
    line-height: normal;
    color: #f08080;
    width: 100%;
    box-sizing: border-box;
    user-select: auto;
    font-size: 16px;
    padding: 0 6px;
    padding-left: 12px;
    width: 10vw;

    margin: 0vw;
  }
.header{
  background-color: #f8ad9d;
  border-radius: 1rem;
  height: 100px;
  width: 98%;
  padding-right: 2%;
  margin-bottom: 1vw;
}
.flexbox{
  display: flex;
  align-items: center;
}

a{
  color: black;
  text-decoration: none;
}
a:hover {
  text-decoration: underline;
}



.logo{
  height:70px;
  width:70px;
  margin:15px;
}
.profilePic{
  height:50px;
  width:50px;
  margin:15px;
  border-radius: 10px
}



.align-right{
  margin-left: auto;
}

.divider {
  border-left: 2px solid black;
  height: 25px;
  margin:5px
}
</style>