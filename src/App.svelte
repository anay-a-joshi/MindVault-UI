<script>
  import Navbar from "./components/navigation_bar.svelte";
  import Hero from "./components/landing_overview.svelte";
  import JournalEntryForm from "./components/mindvault_journal.svelte";
  import Features from "./components/key_features.svelte";
  import Testimonials from "./components/customer_reviews.svelte";
  import Footer from "./components/footer.svelte";
  import Login from "./components/login.svelte";

  import { onMount } from 'svelte'; // Import lifecycle hook

  let isLoggedIn = false;
  let username = '';

  // Check for stored username on app load
  onMount(() => {
    const storedUsername = localStorage.getItem('username');
    if (storedUsername) {
      username = storedUsername;
      isLoggedIn = true;
    }
  });

  const handleLogin = (event) => {
    isLoggedIn = true;
    username = event.detail.username; // Get the username from the login event
    localStorage.setItem('username', username); // Store username in localStorage
  };

  const handleLogout = () => {
    isLoggedIn = false;
    username = '';
    localStorage.removeItem('username'); // Clear username from localStorage
  };
</script>

<Navbar />

{#if !isLoggedIn}
  <Login on:login={handleLogin} />
{/if}

{#if isLoggedIn}
  <Hero
    title={`Welcome, ${username}`}
    description="Mental health is a state of mental well-being that enables people to cope with the stresses of life, realize their abilities, learn well and work well, and contribute to their community."
  />
  <!-- <button on:click={handleLogout} class="logout-button">Logout</button> Add Logout Button -->
  <Features />
  <JournalEntryForm {username} />
  <button on:click={handleLogout} class="logout-button">Logout</button> <!-- Add Logout Button -->
  <br>
{/if}

<Testimonials />
<Footer />

<style>
  .logout-button {
    margin: 1rem auto;
    display: block;
    padding: 0.8rem 2rem;
    font-size: 1rem;
    color: white;
    background: #ff6347;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-weight: bold;
    transition: background 0.3s ease;
  }

  .logout-button:hover {
    background: #e5533f;
  }
</style>
