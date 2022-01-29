<script>
    export let letter;
    export let isActive;

</script>

<span class:active={isActive}>
    {letter.toUpperCase()}
</span>

<style>
    span {
        font-size: calc(1.5rem + 1vw);
        text-align: center;

    }
    .active {
        font-weight: bold;
    }
</style>

