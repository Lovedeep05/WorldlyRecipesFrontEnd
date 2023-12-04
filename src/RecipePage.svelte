<script>
  export let recipe;
  console.log(recipe);
</script>



  {#if recipe != undefined}
  <div class="main">
    <div class="box1">
      <div class="infoBox"> 
        <h1 style={"font-weight: bold;background:#f08080; border-radius:1rem;padding-left:1vw;height:3vw; display:flex;align-items:center;margin-left: 1vw;margin-right:1vw"}>{recipe["nameOfDish"]}</h1>
        <img src="{recipe["dishImage"]}" alt="dishImage">
        <p style={"background:#f08080; border-radius:1rem;padding-left:1vw;height:3vw; display:flex;;margin-left: 1vw;margin-right:1vw;height:18vw;padding-top:1vw"}>{recipe["description"]}</p>
      </div>
        <div class="infoBox"> 
        <p style={"font-weight: bold;background:#f08080; border-radius:1rem;padding-left:1vw;height:3vw; display:flex;align-items:center;margin:1vw"}>Ingredients</p>

          <div class="info1">
            <ul>
            {#each recipe["ingredients"] as line}
              <li>{line}</li>
            {/each}
            </ul>
          </div>
        <p style={"font-weight: bold;background:#f08080; border-radius:1rem;padding-left:1vw;height:3vw; display:flex;align-items:center;margin:1vw"}>Instructions</p>
        <div class="info1">
          <ol>
          {#each recipe["instructions"] as line}
            <li>{line}</li>
          {/each}
          </ol>
        </div>
      </div>
    </div>
  </div>
{/if}


<style>
.main{
  padding: 0px;
  border-radius: 10px;
  width: 100%;
  text-align: center;
  background: #f8ad9d;
  overflow: hidden;
}

.box1{
  display: flex;
}

.infoBox{
    display: flex;
    justify-content:start;
    font-size: large;
    margin:1vw;
    padding-bottom: 1vw;
    border-radius: 1rem;
    overflow: hidden;
    flex-direction: column;
    width: 45vw;
  }

img{
  height:25vw;
  width:auto;
  object-fit: cover;  
  border-radius: 10px;
  margin-left:1vw;
  margin-right:1vw;
}

.info1{
  width: 44vw;
  margin:1vw;
  display: flex;
  align-items: start;
  flex-direction: column;
  margin-right: 5vw;
  text-align: left;
  background: #f08080;
  border-radius: 2rem;
}
</style>