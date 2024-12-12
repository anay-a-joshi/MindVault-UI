<script>
    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    export let habitProgress = 0;
    export let habitName = '';
</script>

<div class="progress-container">
    <p>{habitName}: Keep it up! You're {habitProgress}% closer to your goal!</p>
    <progress value={habitProgress} max="100"></progress>
</div>

<style>
    .progress-container {
        margin: 1.5rem 0;
        font-family: 'Roboto', sans-serif;
        color: #1d3557; /* Neutral text color */
        text-align: center;
    }

    .progress-container p {
        color: #1d3557;
    }
    p {
        font-size: 1rem;
        font-weight: 500;
        margin-bottom: 0.5rem;
        color: #333; /* Updated text color */
    }

    progress {
        width: 100%;
        height: 1.2rem;
        border-radius: 12px;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        appearance: none; /* Ensures cross-browser compatibility */
        border: 1px solid #ddd; /* New border for definition */
        overflow: hidden;
    }

    progress::-webkit-progress-bar {
        background: #e0e0e0; /* Softer neutral background */
    }

    progress::-webkit-progress-value {
        background: linear-gradient(90deg, #1d3557, #45739d);
    }

    progress::-moz-progress-bar {
        background: linear-gradient(90deg, #1d3557, #45739d);
    }
</style>
