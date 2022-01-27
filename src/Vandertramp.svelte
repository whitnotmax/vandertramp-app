<script>
    export let letter;
    export let isActive;

</script>

<span class:active={isActive}>
    {letter.toUpperCase()}
</span>

<style>
    span {
        font-size: 40px;
    }
    .active {
        font-weight: bold;
    }
</style>

