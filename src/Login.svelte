<script>
  import Signup from "./Signup.svelte";
    export let users;
    let viewSignupPage = false;
    let viewLoginPage = true;
    export let viewHomePage;
    console.log(users)
    let username;
    let password;
    export let user;
    export let loginStatus=1;
    const handleLogin = ()=>{
        if(users!=undefined){
            console.log(users)
            users.forEach(u => {
               if(u["user"]==username && u["password"]==password){
                console.log(u["user"]  +" "+ u["password"])
                user=u;
                loginStatus=0
                viewHomePage=true;
               }
            });
        }
        if(loginStatus==1){
            loginStatus=2;
        }
    }
</script>
{#if viewLoginPage}
<div class=main>
    <img class="logo" src="images/logo.webp" alt="logo"/>
    <h1>Login</h1>
    <form on:submit|preventDefault={handleLogin}>
        <input type="text" name="username" placeholder="Username" bind:value={username}>
        <input type="password" name="password" placeholder="Password" bind:value={password}>
        <br>
        <div style={"margin-left=2vw"}>
            <button class="button-5">Login</button>
        </div>
    </form>
    {#if loginStatus==2}
        <p style={"font-weight: bold;"}>Incorrect password</p>
        <a href="nothing">reset your password</a>
    {/if}
    <div style="display: flex; justify-content: space-between; align-items:center">
        <hr style="height: 1px; width: 10vw;  border: 1px solid #ff0000; "  />
        <p style={"font-weight: bold; color:red; margin:1vw"}>OR</p>
        <hr style="height: 1px; width: 10vw;  border: 1px solid #ff0000;" />
    </div>
    <button class="button-5" on:click={()=>{viewSignupPage=true; viewLoginPage=false}}>Sign up</button>
</div>
{/if}
{#if viewSignupPage}
    <Signup bind:viewSignupPage={viewSignupPage} bind:viewLoginPage={viewLoginPage} bind:users={users} />
{/if}
<style>
.main{
    padding: 0px;
    border-radius: 10px;
    width: 100%;
    height: auto;
    padding-top: 1vw;
    padding-bottom: 1vw;
    background: #f8ad9d;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  form{
    flex-direction: column;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  img{
    height:13vw;
    width:13vw;
    border-radius: 1rem;
  }

  input{
    border: 3px solid #f08080;
    border-radius: 1rem;
    height: 50px;
    line-height: normal;
    color: #f08080;
    display: block;
    width: 100%;
    box-sizing: border-box;
    user-select: auto;
    font-size: 16px;
    padding: 0 6px;
    padding-left: 12px;
    width: 20vw;
    font-size: small;
    margin: 1vw;
    }
input:focus{
        border: 3px solid ff0000;
    }
</style>