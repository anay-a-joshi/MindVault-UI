<script>
    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    export let skillPractice;
    export let skill; 
</script>

<div class="skill-practice">
    <h3>Track Your {skill} Hours</h3>
    <p>Keep a log of the time you've spent honing your {skill} skills today.</p>
    <label for="skill-input">Hours dedicated:</label>
    <input
        type="number"
        id="skill-input"
        bind:value={skillPractice}
        min="0"
        max="24"
        placeholder="Enter hours (e.g., 2)"
    >
</div>

<style>
    .skill-practice {
        font-family: 'Arial', sans-serif;
        margin-bottom: 1.5rem;
    }

    .skill-practice h3 {
        color: #1d3557;
        margin-bottom: 0.5rem;
    }

    .skill-practice p {
        font-size: 0.9rem;
        color: #457b9d;
        margin-bottom: 1rem;
    }

    label {
        display: block;
        margin-bottom: 0.3rem;
        color: #1d3557;
        font-size: 0.9rem;
    }

    input[type="number"] {
        width: 100%;
        padding: 0.6rem;
        border: 1px solid #ddd;
        border-radius: 8px;
        font-size: 1rem;
        transition: border-color 0.3s ease, box-shadow 0.3s ease;
    }

    input[type="number"]:focus {
        border-color: #ff6347;
        box-shadow: 0 0 5px rgba(255, 99, 71, 0.5);
        outline: none;
    }
</style>
