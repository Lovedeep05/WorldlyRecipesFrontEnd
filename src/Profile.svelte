<script>
  import Recipe from "./Recipe.svelte";
  export let recipes;
  export let users=[];
  export let user; 

  const userRecipes = recipes.filter((recipe) => recipe["user"]==user["user"]);
</script>

<div class="main">
  <div class="infoBox">
    <div class="info1">
      <p style={"font-weight: bold;background:#f8ad9d; border-radius:1rem; padding-right:20vw;padding-left:1vw;height:3vw; display:flex;align-items:center;"}>@{user["user"]}</p>
      <img class="profilePic" src={user["profilePicture"]} alt="profilePic"/>
    </div>
  <div style={"background:#f8ad9d; border-radius:1rem; display:flex; margin:auto"}>
    <div class="info2">
      <p style={"font-weight: bold;"}>Personal information</p>
      <div style="display: flex; justify-content: space-between;">
        <p style={"font-weight: bold;"}>Email</p>
      <p>{user["email"]}</p>
      </div>
      <div style="display: flex; justify-content: space-between;">
        <p style={"font-weight: bold;"}>First Name</p>
        <p>{user["firstName"]}</p>  
      </div>
      <div style="display: flex; justify-content: space-between;">
        <p style={"font-weight: bold;"}>Last Name</p>
        <p>{user["lastName"]}</p>
      </div>
    </div>
    <div class="info2">
      <p>‎</p>
      <div style="display: flex; justify-content: space-between;">
        <p style={"font-weight: bold;"}>Posts</p>
        <p>{user["numberOfPosts"]}</p>
      </div>
      <div style="display: flex; justify-content: space-between;">
        <p style={"font-weight: bold;"}>Followers</p>
        <p>{user["nFollowers"]}</p>
      </div>
      <div style="display: flex; justify-content: space-between;">
        <p style={"font-weight: bold;"}>Following</p>
        <p>{user["nFollowing"]}</p>
      </div>
    </div>
  </div>
  </div>
  <div class="posts">
    <p style={"font-weight: bold;"}>{user["user"]}'s recipes</p>
    <Recipe recipes={userRecipes}/>
   </div>
</div>



<style>
  .main{
    padding: 0px;
    border-radius: 10px;
    width: 100%;
    text-align: center;
    padding-top: 2vw;
    padding-bottom: 2vw;
    background: #f8ad9d;
  }

  .infoBox{
    display: flex;
    justify-content:center;
    font-size: large;
    background: #f08080;
    margin-left:10vw;
    margin-right:10vw;
    padding-bottom: 3vw;
    border-radius: 1rem;
    overflow: hidden;
    width: 80vw;
    height: auto;

  }

  img{
    height:25vw;
    width:25vw;
    border-radius: 10px
  }

  .info1{
    margin-left: 5vw;
    display: flex;
    align-items: start;
    flex-direction: column;
    margin-right: 2vw;
    text-align: left;
  }
  .info2{
    margin-left: 2vw;
    margin-right: 2vw;
    width: 15vw;
  }
</style>