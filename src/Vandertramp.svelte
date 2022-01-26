<script>
    export let letter;
    export let isActive;
    export let verb;
    export let canUseEtre;
</script>

{#if isActive}
    <strong>
        <span>
            {letter.toUpperCase()}
        </span>
    </strong>



{:else}
    <span>{letter.toUpperCase()}</span>
{/if}



