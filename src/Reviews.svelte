<script>
    import ReviewContent  from "./ReviewContent.svelte";
    let items;
    $: fetch('http://localhost:7878/reviews')
		.then(r => r.json())
		.then(data => {
			items = data;
		});
</script>
{#if items}
    {#each items as item}
        <ReviewContent content={item}/>
    {/each}
{:else}
    <div class="loading">loading...</div>
{/if}
