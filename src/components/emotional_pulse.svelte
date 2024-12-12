<!-- Feelings.svelte -->
<script>

    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    export let feelings;
</script>

<div class="feelings">
    <h3>What's your emotional landscape today? (Pick all that resonate)</h3>
    {#each feelings as feeling, index}
        <label>
            <input type="checkbox" bind:checked={feelings[index].checked}>
            {feeling.mood}
        </label>
        <p class="description">{feeling.description}</p> <!-- Add description here -->
    {/each}
</div>

<style>
    .feelings {
        display: flex;
        flex-direction: column;
    }

    .feelings h3 {
        color: #1d3557;
    }

    .feelings label {
        display: flex;
        align-items: center;
        color: #457b9d;
        margin-bottom: 0.2rem;
        font-size: 1.2rem;
    }

    input[type="checkbox"] {
        margin-right: 0.5rem;
        width: 16px;
        height: 16px;
    }

    .description {
        font-size: 0.9rem; /* Smaller font size for the description */
        color: #666; /* Lighter text color for the description */
        margin-left: 24px; /* Align description with checkbox */
        margin-bottom: 1rem; /* Space between each feeling */
    }
</style>
