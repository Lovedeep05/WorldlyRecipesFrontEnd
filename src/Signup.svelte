<script>
    export let users;
    let username,password,firstName,lastName,email,location;
    export let viewLoginPage = false;
    export let viewSignupPage = true;
    const handleLogin = ()=>{
        let user1={
            bio:"new user",
            email:email,
            firstName: firstName,
            followers:[],
            following:[],
            lastName:lastName,
            likedPosts:[],
            location:location,
            nFollowers: 0,
            nFollowing: 0,
            numberOfPosts:0,
            profilePicture: null,
            savedRecipes:[],
            user:username,
            password:password,
        }
        users.push(user1)
        console.log(users)
        viewLoginPage=true; viewSignupPage=false
    }
</script>
{#if viewSignupPage} 
<div class=main>
    <img class="logo" src="images/logo.webp" alt="logo"/>
    <h1>Sign up</h1>
    <form on:submit|preventDefault={handleLogin}>
        <input type="text" name="FirstName" placeholder="First Name" bind:value={firstName}>
        <input type="text" name="LastName" placeholder="Last Name" bind:value={lastName}>
        <input type="text" name="Location" placeholder="Location (city)" bind:value={location}>
        <input type="email" name="email" placeholder="Email" bind:value={email}>
        <input type="text" name="username" placeholder="Username" bind:value={username}>
        <input type="password" name="password" placeholder="Password" bind:value={password}>
        
        <br>
        <div style={"margin-left=2vw"}>
            <button class="button-5">Sign up</button>
        </div>
    </form>

    <div style="display: flex; justify-content: space-between; align-items:center">
        <hr style="height: 1px; width: 10vw;  border: 1px solid #ff0000; "  />
        <p style={"font-weight: bold; color:red; margin:1vw"}>OR</p>
        <hr style="height: 1px; width: 10vw;  border: 1px solid #ff0000;" />
    </div>
    <button class="button-5" on:click={()=>{viewLoginPage=true; viewSignupPage=false}}>Log in</button>
</div>
{/if}
<style>
.main{
    
    padding: 0px;
    border-radius: 10px;
    width: 100%;
    height: auto;
    padding-top:1vw;
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
    border-radius: 10px
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

    margin: 1vw;
    }
input:focus{
        border: 3px solid ff0000;
    }
</style>