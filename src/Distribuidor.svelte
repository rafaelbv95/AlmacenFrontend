<script>
    export let distribuidor = {};
</script>

<div>
    <input type="text" bind:value={distribuidor.nombre} />
    <input type="text" bind:value={distribuidor.apellidos} />
    <slot/>
</div>