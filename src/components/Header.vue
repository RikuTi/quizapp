<template>
    <div>
        <b-nav tabs>
        <b-nav-item disabled><b>Kysymyksiä</b></b-nav-item>
        <b-nav-item disabled>Oikein: {{numCorrect}}/{{numTotal}}</b-nav-item>
        </b-nav>
    </div>
</template>


<script>
export default {
    props: [
        'numCorrect',
        'numTotal'
    ]
}
</script>