<script>
	import Nav from "./Nav.svelte";
	import Contenido from "./Contenido.svelte";
	import { Router } from "svelte-routing";

	import { setContext } from "svelte";

	const URL = {
		productos: "https://almacen-2daw.herokuapp.com/api/productos/",
		distribuidores: "https://almacen-2daw.herokuapp.com/api/distribuidores/",
	};

	setContext("URL", URL);
</script>

<Router>
	<Nav />
	<Contenido />
</Router>
