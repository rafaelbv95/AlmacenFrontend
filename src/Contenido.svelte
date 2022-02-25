<script>
    import { Route } from "svelte-routing";    
    import Inicio from "./Inicio.svelte"; 
    import Productos from "./Productos.svelte"; 
    import Distribuidores from "./Distribuidores.svelte"; 
</script>

<main>
   <Route path="/" component={Inicio} />
   <Route path="/productos" component={Productos} />
   <Route path="/distribuidores" component={Distribuidores} />
</main>