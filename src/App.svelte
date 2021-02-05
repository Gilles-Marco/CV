<script>

import { Router, Route} from "svelte-routing"
import Home from "./views/MainView.svelte"

export let url = ""

</script>

<style global lang="postcss">
	/* purgecss start ignore */
	@tailwind base;
	@tailwind components;
	/* purgecss end ignore */
	
	@tailwind utilities;
</style>

<Router url="{url}">
	<div>
		<Route path="/"><Home /></Route>
	</div>
</Router>