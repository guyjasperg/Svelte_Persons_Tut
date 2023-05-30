<script>
	import Modal from "./modal.svelte";
	import AddPersonForm from "./AddPersonForm.svelte";

	let showModal = false;

	let people = [
		{ name: "yoshi", beltColour: "black", age: 25, id: 1 },
		{ name: "mario", beltColour: "orange", age: 45, id: 2 },
		{ name: "Luigi", beltColour: "brown", age: 35, id: 3 },
	];

	const btnDelete = (id) => {
		//delete person
		console.log(id);
		people = people.filter((person) => person.id != id);
	};

	const toggleModal = () => {
		showModal = !showModal;
	};

	const addPerson = (e) => {
		console.log(e.detail);
		const person = e.detail;
		people = [...people, person];
		showModal = false;
	};
</script>

<Modal {showModal} on:click={toggleModal}>
	<AddPersonForm on:addPerson={addPerson} />
</Modal>
<main>
	<button on:click={toggleModal}>Add New Person</button>
	<div style="padding: 1em;">
		{#each people as person (person.id)}
			<div class="person">
				<h4>{person.name}</h4>
				{#if person.beltColour === "black"}
					<p><strong>Master Ninja</strong></p>
				{/if}
				<!-- skills -->
				<p>{person.age} years old, {person.beltColour} belt.</p>
				{#if person.skills}
					<p>{person.skills}</p>
				{:else}
					<p>No Skills</p>
				{/if}

				<button on:click={() => btnDelete(person.id)}>Delete</button>
			</div>
			<!-- <br /> -->
		{:else}
			<p>There are no people to show...</p>
		{/each}
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 2em;
		max-width: 240px;
		margin: 0 auto;
		/* background-color: white; */
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}

	div.person {
		border: 1px solid darkgray;
		margin-bottom: 1em;
	}
</style>
