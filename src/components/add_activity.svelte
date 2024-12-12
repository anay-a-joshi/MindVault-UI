<script>
    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    export let wantsToLogMore;
    export let newActivity = '';

    // Function to handle submission and show alert
    const handleActivitySubmission = () => {
        if (wantsToLogMore && newActivity.trim() !== '') {
            alert(`Thank you! 🌟\n\nYour request to add a new activity, "${newActivity}", has been submitted successfully. Our team will review and update your account shortly.`);
        }
    };
</script>

<div class="log-more">
    <h3>Expand Your Journey with New Activities</h3>
    <p>Would you like to log a different activity that's not currently available?</p>

    <div class="yes-no-buttons">
        <label>
            <input type="radio" bind:group={wantsToLogMore} value={true}> Yes
        </label>
        <label>
            <input type="radio" bind:group={wantsToLogMore} value={false}> No
        </label>
    </div>

    {#if wantsToLogMore}
        <div class="new-activity-entry">
            <label for="new-activity">Enter the activity you’d like to add:</label>
            <input type="text" id="new-activity" bind:value={newActivity} placeholder="E.g., Meditation, Painting">
        </div>

        <!-- Submit button -->
        <button on:click={handleActivitySubmission} class="submit-button">
            Submit Activity Request
        </button>
    {/if}
</div>

<style>
    .log-more {
        margin-bottom: 1.5rem;
        font-family: 'Arial', sans-serif;
    }

    .log-more h3 {
        color: #1d3557;
        margin-bottom: 0.5rem;
    }

    .log-more p {
        color: #457b9d;
        font-size: 0.9rem;
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

    .new-activity-entry {
        margin-top: 1rem;
    }

    .new-activity-entry label {
        display: block;
        margin-bottom: 0.5rem;
        color: #1d3557;
    }

    .new-activity-entry input[type="text"] {
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
