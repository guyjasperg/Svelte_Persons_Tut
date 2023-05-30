<script>
    import { createEventDispatcher } from "svelte";

    let dispatch = createEventDispatcher();

    let name;
    let beltColour;
    let age;
    let skills = [];

    const handleSubmit = () => {
        // console.log(name, beltColour, age, skills);
        const person = {
            name: name,
            beltColour: beltColour,
            age: age,
            id: Math.random(),
            skills: skills,
        };

        dispatch("addPerson", person);
    };
</script>

<form on:submit|preventDefault={handleSubmit}>
    <input type="text" placeholder="name" bind:value={name} />
    <input type="number" placeholder="Age" bind:value={age} />
    <!-- svelte-ignore a11y-label-has-associated-control -->
    <label>Skills:</label>
    <input type="checkbox" bind:group={skills} value="fighting" />
    fighting<br />
    <input type="checkbox" bind:group={skills} value="sneaking" />
    sneaking<br />
    <input type="checkbox" bind:group={skills} value="running" /> running<br />
    <select bind:value={beltColour}>
        <option value="black">black</option>
        <option value="orange">orange</option>
        <option value="brown">brown</option>
        <option value="white">white</option>
    </select>
    <button>Add Person</button>
</form>

<style>
</style>
