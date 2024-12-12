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

    export let waterIntake = 0; // Add this to handle two-way binding

    $: progress.set(waterIntake / 5);  // Update progress when waterIntake changes (assuming 5L as the max goal)

    export function addWater(amount) {
        if (waterIntake + amount <= 5) { // Cap water intake at 5L
            waterIntake += amount;
            progress.set(waterIntake / 5);
        } else {
            alert("You've reached the recommended daily hydration limit!");
        }
    }

    export function subtractWater(amount) {
        if (waterIntake - amount >= 0) { // Ensure water intake does not go below 0
            waterIntake -= amount;
            progress.set(waterIntake / 5);
        } else {
            alert("Water intake cannot be less than 0!");
        }
    }

    export function resetWaterIntake() {
        waterIntake = 0;
        progress.set(waterIntake / 5);
    }
</script>

<div class="water-intake">
    <h3>Track Your Water Hydration for Today</h3>
    <br>
    <progress value={$progress} max="1"></progress>
    <!-- <br> -->
    <div class="water-buttons">
        <button on:click={() => addWater(0.25)}> +250ml </button>
        <button on:click={() => addWater(0.5)}> +500ml </button>
        <button on:click={() => addWater(1)}> +1 Liter </button>
        <button on:click={() => addWater(2)}> +2 Liters </button>
        <button on:click={() => addWater(3)}> +3 Liters </button>
    </div>

    <div class="adjust-buttons">
        <button on:click={() => subtractWater(0.5)}> -500ml </button>
        <button on:click={() => subtractWater(1)}> -1 Liter </button>
        <button on:click={resetWaterIntake}> Reset </button>
    </div>
    <br><br>
    <div class="water-summary">
        <p>Your total water intake today: <strong>{waterIntake.toFixed(2)} Liters</strong></p>
        <p>Keep it up! Hydration is key to a healthy body and mind. 🚰</p>
    </div>
</div>

<style>
    .water-intake {
        text-align: center;
        font-family: 'Arial', sans-serif;
        color: #1D3557;
    }

    .water-buttons, .adjust-buttons {
        display: flex;
        justify-content: center;
        gap: 1rem; /* Add consistent spacing between buttons */
        margin-top: 1rem;
    }

    .water-buttons button, .adjust-buttons button {
        flex: none;
        padding: 0.5rem 1rem;
        border: none;
        border-radius: 8px;
        cursor: pointer;
        background-color: #FF6347;
        color: white;
        font-size: 1rem;
        font-weight: bold;
        transition: background 0.3s ease;
    }

    .water-buttons button:hover, .adjust-buttons button:hover {
        background-color: #1D3557;
    }

    progress {
        display: block;
        width: 100%;
        height: 25px;
        margin: 1rem 0;
        border-radius: 12px;
        overflow: hidden;
        background-color: #E0E0E0;
    }

    progress::-webkit-progress-bar {
        background-color: #E0E0E0;
    }

    progress::-webkit-progress-value {
        background-color: #457B9D;
        transition: width 0.3s ease;
    }

    .water-summary {
        margin-top: 1rem;
        font-size: 1rem;
    }

    .water-summary p {
        margin: 0.5rem 0;
    }
</style>
