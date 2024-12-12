<script>
    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    import { tweened } from 'svelte/motion';
    import { cubicOut } from 'svelte/easing';

    const progress = tweened(0, {
        duration: 400,
        easing: cubicOut
    });

    let selectedFruits = [];

    export let fruitIntake = 0;

    // Function to update the protein sources selected
    function selectFruit(protein) {
        if (!selectedFruits.includes(protein)) {
            selectedFruits = [...selectedFruits, protein];
            fruitIntake = selectedFruits.length; // Update the count of proteins
            progress.set(fruitIntake / 5); // Assuming a max of 5 servings for the progress bar
        }
    }

    // Function to remove a selected protein source
    function removeFruit(protein) {
        selectedFruits = selectedFruits.filter(f => f !== protein);
        fruitIntake = selectedFruits.length;
        progress.set(fruitIntake / 5);
    }
</script>

<div class="protein-intake">
    <h3>Monitor and Record the Protein Sources</h3>
    <p>Select the protein sources you consumed today:</p>
    <progress value={$progress} max="1"></progress>

    <div class="protein-buttons">
        <button on:click={() => selectFruit('Eggs 🥚')}>Eggs 🥚</button>
        <button on:click={() => selectFruit('Chicken 🍗')}>Chicken 🍗</button>
        <button on:click={() => selectFruit('Fish 🐟')}>Fish 🐟</button>
        <button on:click={() => selectFruit('Tofu 🥡')}>Tofu 🥡</button>
        <button on:click={() => selectFruit('Lentils 🌱')}>Lentils 🌱</button>
    </div>

    {#if selectedFruits.length > 0}
        <div class="selected-proteins">
            <h4>Selected Protein Sources:</h4>
            <ul>
                {#each selectedFruits as protein}
                    <li>{protein} <button on:click={() => removeFruit(protein)}>Remove</button></li>
                {/each}
            </ul>
        </div>
    {/if}
</div>

<style>
    .protein-intake {
        text-align: center;
        margin: 1.5rem;
        font-family: 'Arial', sans-serif;
    }

    .protein-intake h3 {
        color: #1d3557;
    }

    .protein-intake p {
        color: #457b9d;
    }

    .protein-buttons {
        display: flex;
        justify-content: space-around;
        margin-top: 1rem;
        flex-wrap: wrap;
    }

    .protein-buttons button {
        margin: 5px;
        padding: 0.6rem;
        border: none;
        border-radius: 8px;
        cursor: pointer;
        background-color: #ff6347;
        color: white;
        font-size: 0.9rem;
        transition: background 0.3s ease;
    }

    .protein-buttons button:hover {
        background-color: red;
    }

    .selected-proteins {
        margin-top: 1.5rem;
    }

    .selected-proteins ul {
        list-style: none;
        padding: 0;
    }

    .selected-proteins li {
        display: flex;
        justify-content: space-between;
        margin: 0.5rem 0;
        padding: 0.5rem;
        background-color: #f1f1f1;
        border-radius: 5px;
        border: 1px solid #ccc;
    }

    .selected-proteins button {
        background-color: #f44336;
        color: white;
        border: none;
        padding: 0.3rem 0.5rem;
        border-radius: 4px;
        cursor: pointer;
    }

    .selected-proteins button:hover {
        background-color: red;
    }

    progress {
        width: 100%;
        height: 1rem;
        margin-top: 1rem;
        border-radius: 8px;
    }

    progress::-webkit-progress-bar {
        background-color: #e0e0e0;
        border-radius: 8px;
    }

    progress::-webkit-progress-value {
        background-color: #ff6347;
        border-radius: 8px;
    }
</style>
