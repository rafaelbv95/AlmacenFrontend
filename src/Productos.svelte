<script>
    import { getContext, onMount } from "svelte";
    import { jsonData } from "./store";
    import Producto from "./Producto.svelte";
    import Buscar from "./Buscar.svelte";
    import Boton from "./Boton.svelte";

    const URL = getContext("URL");
    let busqueda = "";
    let producto = {};

    onMount(() => {
        fetch(URL.productos)
            .then((response) => response.json())
            .then((data) => ($jsonData = data));
    });

    $: regexp = new RegExp(busqueda, "i");
    $: datos = busqueda
        ? $jsonData.filter((item) => regexp.test(item.nombre))
        : $jsonData;
</script>

<h1>Productos</h1>

<Buscar bind:busqueda={busqueda}/>
<Producto bind:producto={producto}>
    <Boton tipo="insertar" coleccion="productos" documento={producto}/>
</Producto>

{#each datos as producto}
    <Producto {producto}>
        <Boton tipo="modificar" coleccion="productos" documento={producto} />
        <Boton tipo="eliminar" coleccion="productos" documento={producto} />
    </Producto>
{/each}
