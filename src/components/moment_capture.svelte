<script>
    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    export let image;
</script>

<div class="image-upload-container">
    <h3>Capture the Essence of Your Day</h3>
    <p class="instruction">Upload a photo that reflects your mood or activities today.</p>
    <input type="file" bind:value={image} accept="image/*" class="file-input">
</div>

<style>
    .image-upload-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 1.5rem;
        border: 1px solid #ccc;
        border-radius: 10px;
        background-color: #fefefe;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        font-family: 'Arial', sans-serif;
    }

    .image-upload-container h3 {
        font-size: 1.5rem;
        color: #1d3557;
        margin-bottom: 0.5rem;
        text-align: center;
    }

    .image-upload-container p{
        color: #457b9d;
    }

    .instruction {
        font-size: 1rem;
        color: #666;
        margin-bottom: 1rem;
        text-align: center;
    }

    .file-input {
        width: 100%;
        max-width: 300px;
        padding: 0.8rem;
        border: 2px dashed #aaa;
        border-radius: 12px;
        background-color: #f9f9f9;
        font-size: 1rem;
        color: #555;
        cursor: pointer;
        text-align: center;
        transition: border-color 0.3s, background-color 0.3s;
    }

    .file-input:hover {
        border-color: #4caf50;
        background-color: #f3fef3;
    }

    .file-input:focus {
        outline: none;
        border-color: #4caf50;
        background-color: #e8fbe8;
    }
</style>
