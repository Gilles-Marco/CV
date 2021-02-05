<script>
    export let text;
</script>

<style type="text/scss">

$border-width: 2px;

.appbar-button{
    @apply flex items-center md:mx-4 mx-2;

    height: 100%;

    p {
        white-space: nowrap;
    }
}
</style>

<div class="appbar-button">
    <p>{text}</p>
</div>