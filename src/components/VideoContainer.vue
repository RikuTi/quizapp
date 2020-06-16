<template>
    <div>
        <h1>Hyvää 50v syntymäpäivää!!!</h1>

       <div class="embed-responsive embed-responsive-16by9">
        <iframe class="embed-responsive-item" width="1280" height="720" src="https://www.youtube.com/embed/0gHKtxL9KS4?rel=0&amp;controls=1&amp;showinfo=0&amp;autoplay=1" 
        frameborder="0" 
        allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
        allowfullscreen
        autoplay="1">
        </iframe>

        </div>

    </div>
</template>


<script>
export default {
    props: [

    ]
}
</script>


<style scoped>

iframe {
  margin: auto;
  position: relative;
  width: 150%;
  padding: 10px;
  left: -100px;
}

h1{
    color:lightblue;
    background-color: red;
}

</style>