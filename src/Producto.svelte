<script>
    export let producto = {};
</script>

<div>
    <input type="text" bind:value={producto.nombre} />
    <input type="text" bind:value={producto.precio} />
    <slot/>
</div>