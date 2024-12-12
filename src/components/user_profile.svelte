<script>
    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    export let user; 
    let currentDate = new Date(); // Current date for user information
    let startDate = new Date('2024-11-29'); // User's start date as a Date object
    let daysActive = Math.floor((currentDate.getTime() - startDate.getTime()) / (1000 * 60 * 60 * 24)); // Difference in days
</script>

<section class="user-info">
    <h1>Hello, <span class="username">{user.username}</span>!</h1>
    <p>Today's date: <span class="highlight">{currentDate.toDateString()}</span></p>
    <p>Current time: <span class="highlight">{new Date().toLocaleTimeString()}</span></p>
    <p>Your journey with us began on <span class="highlight">November 29, 2024</span>.</p>
    <p>You've actively engaged with the platform for <span class="highlight">{daysActive} days</span>. Keep up the great work!</p>
</section>

<style>
    section.user-info {
        font-family: 'Arial', sans-serif;
        font-size: 1rem;
        color: #457b9d; /* Deep blue for text */
        line-height: 1.5;
        /* padding: 1.5rem; */
        text-align: center;

    }

    .user-info h1 {
        font-size: 2.5rem;
        font-weight: bold;
        margin-bottom: 1rem;
        color: #1d3557; /* Lighter blue for headings */
    }

    .user-info h1 .username {
        color: #1d3557;
    }

    .user-info p {
        margin: 0.5rem 0;
    }

    .user-info .highlight {
        color: #1d3557; /* Accent color for highlights */
        font-weight: bold;
    }

    /* Add subtle transitions */
    .user-info h1:hover {
        color: #1d3557;
        transition: color 0.3s ease;
    }

    .user-info p:hover .highlight {
        color: #ff6347; /* Match highlight hover effect with heading */
        transition: color 0.3s ease;
    }

    /* Remove containers but keep spacing balanced */
    body {
        margin: 0;
        padding: 0;
        background-color: #f0f4f8; /* Light background for contrast */
    }
</style>
