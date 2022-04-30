<script>
    export let content;
</script>
<article class= "review">
    <header class= "reviewHeader">
        <h1>{content.service_rendered} {content.service_cost} $</h1>
      </header>
      <div class = "reviewInfo">
            I went with {content.doctor_name}
      </div>
</article>
<style>
    .review{
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .reviewHeader{
        background-color: rgb(255, 255, 255);
        width: 300px;
        height: 50px;
        border: 1px solid;
        padding: 2px;
    }
    .reviewInfo{
        background-color: rgb(255, 255, 255);
        width: 300px;
        height: 100px;
        border: 1px solid;
        padding: 2px;
    }
</style>