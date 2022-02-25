<script>
    import { getContext, onMount } from "svelte";
    import { jsonData } from "./store";
    import Distribuidor from "./Distribuidor.svelte";
    import Buscar from "./Buscar.svelte";
    import Boton from "./Boton.svelte";

    const URL = getContext("URL");
    let busqueda = "";
    let distribuidor = {};

    onMount(() => {
        fetch(URL.distribuidores)
            .then((response) => response.json())
            .then((data) => ($jsonData = data));
    });

    $: regexp = new RegExp(busqueda, "i");
    $: datos = busqueda
        ? $jsonData.filter((item) => regexp.test(item.nombre))
        : $jsonData;
</script>

<h1>Distribuidores</h1>

<Buscar bind:busqueda={busqueda}/>
<Distribuidor bind:distribuidor={distribuidor}>
    <Boton tipo="insertar" coleccion="distribuidores" documento={distribuidor}/>
</Distribuidor>

{#each datos as distribuidor}
    <Distribuidor {distribuidor}>
        <Boton tipo="modificar" coleccion="distribuidores" documento={distribuidor} />
        <Boton tipo="eliminar" coleccion="distribuidores" documento={distribuidor} />
    </Distribuidor>
{/each}
