<script>
    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    export let wantsToRemove = false;
    export let activityToRemove = '';

    // Function to handle activity removal and show alert
    const handleRemoveActivity = () => {
        if (wantsToRemove && activityToRemove.trim() !== '') {
            alert(`🛠️ Removal Underway!\n\nYour request to remove "${activityToRemove}" has been forwarded for verification. Please allow some time for updates to reflect in your account. Thank you! 🙏`);
        }
    };
</script>

<div class="remove-activity">
    <h3>Refine Your Activity List</h3>
    <p>Is there an activity you no longer wish to track?</p>

    <div class="yes-no-buttons">
        <label>
            <input type="radio" bind:group={wantsToRemove} value={true}> Yes
        </label>
        <label>
            <input type="radio" bind:group={wantsToRemove} value={false}> No
        </label>
    </div>

    {#if wantsToRemove}
        <div class="remove-activity-entry">
            <label for="remove-activity">Enter the activity you wish to remove:</label>
            <input type="text" id="remove-activity" bind:value={activityToRemove} placeholder="E.g., Running, Yoga">
        </div>

        <!-- Submit button for removing activity -->
        <button on:click={handleRemoveActivity} class="submit-button">
            Submit Removal Request
        </button>
    {/if}
</div>


<style>
    .remove-activity {
        margin-bottom: 1.5rem;
        font-family: 'Arial', sans-serif;
    }

    .remove-activity h3 {
        color: #1d3557;
        margin-bottom: 0.5rem;
    }

    .remove-activity p {
        color: #457b9d;
        font-size: 0.9rem;
        margin-bottom: 1rem;
    }

    /* Flexbox for Yes/No buttons */
    .yes-no-buttons {
        display: flex;
        justify-content: space-around;
        margin: 1rem 0;
    }

    .yes-no-buttons label {
        display: inline-flex;
        align-items: center;
        justify-content: center;
        padding: 0.5rem 1rem;
        background-color: #ff6347;
        color: white;
        border-radius: 5px;
        cursor: pointer;
        transition: background 0.3s ease;
        font-size: 0.9rem;
    }

    .yes-no-buttons label:hover {
        background-color: red;
    }

    .remove-activity-entry {
        margin-top: 1rem;
    }

    .remove-activity-entry label {
        display: block;
        margin-bottom: 0.5rem;
        color: #1d3557;
    }

    .remove-activity-entry input[type="text"] {
        width: 100%;
        padding: 0.6rem;
        border: 1px solid #ddd;
        border-radius: 4px;
        font-size: 0.9rem;
    }

    .submit-button {
        display: block;
        margin: 1rem auto 0;
        padding: 0.6rem 1.2rem;
        background-color: #ff6347;
        border: none;
        color: white;
        border-radius: 5px;
        font-size: 1rem;
        cursor: pointer;
        transition: background 0.3s ease;
    }

    .submit-button:hover {
        background-color: red;
    }
</style>
