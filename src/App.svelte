<script>
	import Review from './Review.svelte';
	import Reviews from './Reviews.svelte';
	import Login from './Login.svelte';
	let cookie = document.cookie;
	function isLoggedIn(cookie){
		let found = false;
		if(typeof(cookie) == "string"){
			const info = cookie.split(";");
			const response = fetch("http://localhost:7878/login", {
				method: 'POST',
				headers: {
				'Content-Type': 'application/json'            
				},
				body: JSON.stringify({"username": info[0], "password" : info[1]})
			});
			response.then(function(processedResponse){
				if (processedResponse.ok) {
					found = true;
				}
				else{
					found = false;
				}
			}).catch(e => {
				found = false;
			});
		}
		return found;
	}
</script>

<main>
	{#if isLoggedIn(cookie)}
		<Review/>
		<Reviews/>
	{:else}
		<Login/>
	{/if}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}
	:global(body){
        background: linear-gradient(rgba(196, 102, 0, 0.8),rgb(103,46,46, 0.8));
    }
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>