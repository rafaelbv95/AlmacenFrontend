<script>
    import { onMount, getContext } from "svelte";
  import { jsonData }            from "./store.js";
  export let tipo = "insertar"; // insertar, modificar, eliminar
  export let coleccion = "articulos"; // articulos, clientes
  export let documento = {};
  
 
  let handler = () => {};  
  let clases = "";
  let url = "";
  const URL = getContext("URL"); 
  onMount(() => {
    switch (tipo) {
      case "insertar":
        clases = "insertar";
        handler = insertar;
       
        break;
      case "modificar":
        clases = "modificar";
        handler = modificar;
      
        break;
      case "eliminar":
        clases = "eliminar";
        handler = eliminar;
       
        break;
      default:
    }
    switch (coleccion) {
      case "productos": url=URL.productos; break;
      case "distribuidores": url=URL.distribuidores; break;
      default:
    }
  });
  function insertar() {
    if (
      Object.keys(documento).length > 1 &&
      Object.values(documento).every(x => x !== undefined && x != "")
    ) {
      fetch(url, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(documento)
      })
        .then(res => res.json())
        .then(data => {
          $jsonData = [...$jsonData, data];
          ok();
        })
        .catch(err => ko());
    }
  }
  function modificar() {
    fetch(url + documento._id, {
      method: "PUT",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(documento)
    })
      .then(res => res.json())
      .then(data => ok())
      .catch(err => ko());
  }
  function eliminar() {
    fetch(url + documento._id, { method: "DELETE" })
      .then(res => res.json())
      .then(data => {
        $jsonData = $jsonData.filter(x => x._id !== data._id);
        ok();
      })
      .catch(err => ko());
  }
</script>

<button class={clases} on:click={handler} />

<style>
    .insertar {
        background-color: lightgreen;
    }
    .insertar::after {
        content: "Insertar";
    }

    .modificar {
        background-color: lightskyblue;
    }
    .modificar::after {
        content: "Modificar";
    }

    .eliminar {
        background-color: lightcoral;
    }
    .eliminar::after {
        content: "Borrar";
    }
</style>
