<script>
    export let title = "";
    export let startYear;
    export let endYear;
    export let quickDesc = "";
    export let frenchEquivalent = "";
    export let link = "";
</script>
<style type="text/scss">
</style>

<div>
    <h3>{title}</h3>
    <p>Period : {startYear}-{endYear}</p>
    <p>{quickDesc}</p>
    <p>{frenchEquivalent}</p>
    <a href="{link}">Link here</a>
</div>