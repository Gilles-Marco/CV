<script>
	import moment from "moment";
	import Diploma from "./components/Diploma.svelte";
	import { sortBy } from "lodash"

	$: age = moment.duration(moment() - moment("1999-03-28")).years();

	let diplomas = [
		{
			title: "High school Degree in sciences",
			startYear: 2014,
			endYear: 2017,
			quickDesc: "",
			frenchEquivalent: "Baccalauret Scientifique",
			link: ""
		},
		{
			title: "Two years degree diploma in IT",
			startYear: 2017,
			endYear: 2019,
			quickDesc: "",
			frenchEquivalent: "DUT Informatique",
			link: ""
		},
		{
			title: "Master of Business Informatics",
			startYear: 2019,
			endYear: 2022,
			quickDesc: "",
			frenchEquivalent: "MIAGE",
			link: ""
		}
	]
</script>

<style type="text/scss">
</style>


<h1>Marco GILLES</h1>

<section>
	<h2>Presentation</h2>
	<div>
		<div>
			<img src="./assets/marcogillesphoto.png" height="100%" width="100%"/>
		</div>
		<div>
			<h3>FullStack Developer</h3>
			<p>{age} years old student in apprenticeship</p>
			<p>Currently studying for my Master of Business Informatics</p>
		</div>
	</div>
</section>

<section>
	<h2>Professionnal Career</h2>
	<h3>Current position</h3>
	<p>Working as FullStack developer at <a href="https://www.himydata.com/fr/">Himydata</a></p>
</section>

<section>
	<h2>Interesting projects</h2>
</section>

<section>
	<h2>Academic Background</h2>
	{#each sortBy(diplomas, "startYear", "dsc").reverse() as diploma}
		<Diploma {...diploma} />
	{/each}
</section>

<footer>
	<a href="https://github.com/Gilles-Marco/CV">Source code is available here</a>
</footer>