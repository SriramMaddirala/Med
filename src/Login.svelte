{#if signup}
    <button class="loginButton" on:click={toggleLogin}>Switch to Sign Up</button>
    <form class="signUpForm">
        <p>Fill out the following fields</p>
        <input type="text" name="username" placeholder="Your username" bind:value={username}>
        <input type="text" name="password" placeholder="Your password" bind:value={password}>
        <button class="formButton" on:click={loggedIn}> Done </button>
    </form>
{:else}
    <button class="loginButton" on:click={toggleLogin}>Switch to Login</button>
    <form class="loginForm">
        <p>Fill out the following fields</p>
        <input type="text" name="username" placeholder="Your username" bind:value={username}>
        <input type="text" name="password" placeholder="Your password" bind:value={password}>
        <input type="text" name="email" placeholder="Your email address" bind:value={email}>
        <button class="formButton" on:click={signedUp}> Done </button>
    </form>
{/if}
<script>
    let username = "";
    let password = "";
    let email = "";
    let signup = false;
    function toggleLogin(){
        signup = !signup;
    }
    function signedUp(event){
        event.preventDefault();
        const response = fetch("http://localhost:3000/signup", {
            method: 'POST',
            headers: {
            'Content-Type': 'application/json'            
            },
            body: JSON.stringify({"username": username, "password" : password, "email": email})
        });
        response.then(function(processedResponse){
            if (processedResponse.ok) {
                alert("Signed up");
            }
        }).catch(e => {
            throw new Error(`HTTP error! status: ${e.status}`);
        });
    }
    function loggedIn(event){
        event.preventDefault();
        const response = fetch("http://localhost:3000/login", {
            method: 'post',
            headers: {
            'Content-Type': 'application/json'            
            },
            body: JSON.stringify({"username": username, "password" : password})
        });
        response.then(function(processedResponse){
            if (processedResponse.ok) {
                return true;
            }
            return false;
        }).catch(e => {
            throw new Error(`HTTP error! status: ${e.status}`);
        });
		
    }
</script>