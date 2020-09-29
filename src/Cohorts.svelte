<script lang="ts">
	let query: string;

	interface CohortInfo {
		cohort: string;
		choice: string;
		seat: string;
	}

	import cohorts2021, { date } from "./cohorts.20200929";
	let cohortMap = new Map<string, CohortInfo>();
	for (let row of cohorts2021) {
		let osis = row[0];

		let info: CohortInfo = {
			choice: row[1],
			cohort: row[2],
			seat: row[3],
		};
		cohortMap.set(osis, info);
	}

	$: lookupResult = cohortMap.get(query);

	const seatRef = {
		LHA: "Lecture Hall A (Theater)",
		LHB: "Lecture Hall B (Theater)",
		GYM3: "Gym - 3rd Floor",
		GYM6: "Gym - 6th Floor",
		CAFE: "Cafeteria",
	};

	function transformSeatStr(seat: string): string {
		let parts = seat.split(':');
		let desc: string = seatRef[parts[0].trim()];
		return `${desc} -${parts[1]}`;
	}
</script>

<style>
	main {
		text-align: center;
		padding: 1em;
		/* max-width: 240px; */
		margin: 0 auto;
	}

	span {
		color: green;
	}

	section {
		font-size: 2rem;
		padding: 1.5rem 2rem;
		border-radius: 0.2rem;
		margin: 0 auto;
	}

	input {
		font-family: "Roboto", sans-serif;
		color: #333;
		font-size: 1rem;
		margin: 0 auto;
		padding: 1.5rem 2rem;
		border-radius: 0.2rem;
		background-color: rgb(255, 255, 255);
		/* border: none; */
		width: 90%;
		display: block;
		/* border-bottom: 0.3rem solid black; */
		transition: all 0.3s;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
</style>

<svelte:head>
	<title>Cohort Lookup 2020-2021</title>
</svelte:head>

<main>
	<h1>Hello Stuy!</h1>
	<p>
		[UNOFFICIAL] Get your cohort for 2020-2021. Lasted updated with official
		data on {date.getFullYear()}-{date.getMonth() + 1}-{date.getDate()}.
	</p>
	<input type="text" placeholder="Your OSIS here" bind:value={query} />
	<section>
		{#if lookupResult}
			<code>Your group is: <span>{lookupResult.cohort}</span></code>
			<br />
			<code>Your survey choice was: <span>{lookupResult.choice}</span></code>
			{#if lookupResult.cohort !== 'Remote'}
				<br/>
				<code>Your seat is: <span>{transformSeatStr(lookupResult.seat)}</span></code>
			{/if}
		{:else}
			<p>OSIS not found</p>
		{/if}
	</section>
	<p>
		Note: You can switch to remote at any time by completing <a target="_blank" href="https://www.nycenet.edu/surveys/learningpreference">this
			survey</a>
	</p>

	<p>
		Original spreedsheet & more descriptions <a target="_blank" href="https://tinyurl.com/Stuy-Blended">here</a>
	</p>
</main>
