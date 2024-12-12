<script>

    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    export let didYoga;
    export let yogaDuration;
</script>

<div class="meditation-session">
    <h3>Meditation Tracker</h3>

    <div class="yes-no-buttons">
        <label>
            <input type="radio" bind:group={didYoga} value={true}> Yes
        </label>
        <label>
            <input type="radio" bind:group={didYoga} value={false}> No
        </label>
    </div>

    {#if didYoga}
        <div class="meditation-slider">
            <label for="meditation">Duration of your meditation today (Minutes):</label>
            <input type="range" id="meditation" bind:value={yogaDuration} min="0" max="120" step="5">
            <p>🧘 Wonderful! You've devoted <span>{yogaDuration}</span> minutes to meditation today.</p>
        </div>
    {/if}
</div>

<style>
    .meditation-session {
        font-family: 'Arial', sans-serif;
        margin-bottom: 1.5rem;
        color: #1D3557;
    }

    .yes-no-buttons {
        display: flex;
        justify-content: center;
        gap: 1rem;
        margin-top: 1rem;
        color: #FF6347;
    }

    .yes-no-buttons:hover {
        color: #1D3557;
    }

    .yes-no-buttons label {
        padding: 0.5rem 1rem;
        background-color: #FF6347;
        color: white;
        border-radius: 5px;
        font-weight: bold;
        cursor: pointer;
        transition: background 0.3s ease;
    }

    .yes-no-buttons label:hover {
        background-color: #1d3557;
    }

    .meditation-slider {
        margin-top: 1rem;
        text-align: center;
    }

    .meditation-slider label {
        display: block;
        margin-bottom: 0.5rem;
        font-size: 1rem;
        color: #457B9D;
    }

    .meditation-slider input[type="range"] {
        width: 80%;
        margin: 0 auto;
        display: block;
        color: #1D3557;
    }

    .meditation-slider p {
        margin-top: 0.5rem;
        font-size: 1rem;
        color: #1D3557;
        font-weight: bold;
    }

    .meditation-slider span {
        color: #FF6347;
    }
</style>
