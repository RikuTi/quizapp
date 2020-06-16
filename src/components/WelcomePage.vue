<template>
    <div>
       <h1>Vanhetessa viisastuu, vai viisastuuko?</h1>

        <div class="pt-2 pb-4">
            <b-button class="btn btn-primary btn-lg " @click="setStarted" variant="success">
                Aloita
            </b-button>
        </div>
    </div>
</template>


<script>
export default {
   props : {
    setStarted: Function
  },
}
</script>


<style scoped>

</style>