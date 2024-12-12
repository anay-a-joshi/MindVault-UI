<script>
  export let links = [
    { name: "Features", href: "#feature", info: "Discover tools to enhance your journaling experience, from mood tracking to visual analytics." },
    { name: "Why Us", href: "#testimonials", info: "Trusted by thousands, our platform empowers mindful journaling and personal growth" },
    { name: "Contact", href: "#contact", info: "Facing issues? Contact our Helpdesk at helpdesk@mindscribe.com for quick resolutions." },
  ];

  let showPopup = false;
  let popupMessage = "";
  // let isDarkMode = false; // Dark mode toggle for navbar

  function handleLinkClick(link) {
    popupMessage = link.info;
    showPopup = true;
    setTimeout(() => {
      showPopup = false;
    }, 3000); // Show popup for 3 seconds
  }


  let isDarkMode = false; // Navbar and breathing circle dark mode state

  function toggleDarkMode() {
    isDarkMode = !isDarkMode;
    document.documentElement.style.setProperty(
      '--circle-color-light',
      isDarkMode ? 'rgba(0, 0, 0, 0.4)' : 'rgba(255, 255, 255, 0.2)'
    );
    document.documentElement.style.setProperty(
      '--navbar-bg-color',
      isDarkMode ? '#1c1c1c' : '#00ced1'
    );
  }
</script>



<style>
  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 2rem;
    background-color: var(--navbar-bg-color, #00ced1); /* Default to light mode */
    color: white;
    font-family: 'Arial', sans-serif;
    transition: background-color 0.3s ease;
  }

  .auth-buttons button {
    font-weight: bold;
    color: white;
    border: 1px solid white;
    padding: 0.5rem 1rem;
    border-radius: 5px;
    background: transparent;
    cursor: pointer;
    transition: background-color 0.3s, color 0.3s;
  }

  .auth-buttons button:hover {
    background-color: white;
    color: var(--navbar-bg-color, #ff6347);
  }


  :root {
    --navbar-bg-color: #00ced1; /* Light mode */
    --navbar-text-color: white;
  }

  [data-dark-mode="true"] {
    --navbar-bg-color: #333; /* Dark mode */
    --navbar-text-color: #f0fff0;
  }

  .logo {
    font-size: 2rem;
    font-weight: bold;
    cursor: pointer;
    transition: transform 0.3s ease, color 0.3s ease;
  }

  .logo:hover {
    color: #f0fff0;
    transform: scale(1.1);
  }

  ul {
    list-style: none;
    display: flex;
    gap: 2rem;
    margin: 0 auto; /* Center the list */
    padding: 0;
    justify-content: center; /* Align items in the center */
    width: 100%; /* Ensures the links stay centered across the navbar */
  }


  li a {
    text-decoration: none;
    color: var(--navbar-text-color);
    font-weight: bold;
    font-size: 1rem;
    transition: color 0.3s ease, transform 0.3s ease;
  }

  li a:hover {
    color: #f0fff0;
    transform: scale(1.1);
  }

  .auth-buttons {
    display: flex;
    gap: 1rem;
  }

  .auth-buttons button {
    font-weight: bold;
    color: var(--navbar-text-color);
    border: 2px solid var(--navbar-text-color);
    padding: 0.5rem 1.2rem;
    border-radius: 25px;
    background: transparent;
    cursor: pointer;
    transition: background-color 0.3s, color 0.3s, box-shadow 0.3s;
  }

  .auth-buttons button:hover {
    background-color: #f0fff0;
    color: var(--navbar-bg-color);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  }

  /* Popup styles */
  .popup {
    position: fixed;
    top: 10%;
    left: 50%;
    transform: translate(-50%, 0);
    background: white;
    color: black;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    padding: 1rem 2rem;
    font-size: 1rem;
    z-index: 1500;
    animation: fadeInOut 3s ease-in-out;
  }

  @keyframes fadeInOut {
    0%, 100% { opacity: 0; }
    20%, 80% { opacity: 1; }
  }

  .dark-mode-toggle {
    font-weight: bold;
    font-size: 1rem;
    color: var(--navbar-text-color);
    background: transparent;
    border: none;
    cursor: pointer;
    transition: color 0.3s ease;
  }

  .dark-mode-toggle:hover {
    color: #f0fff0;
  }
</style>

<!-- Navbar -->
<nav data-dark-mode={isDarkMode}>
  <div class="logo">MindScribe</div>
  <ul>
    {#each links as link}
      <li>
        <a href={link.href} on:click|preventDefault={() => handleLinkClick(link)}>{link.name}</a>
      </li>
    {/each}
  </ul>
  <div class="auth-buttons">
    <button on:click={() => window.open("https://github.com/your-repo", "_blank")}>GitHub</button>
    <button on:click={() => window.open("https://your-demo-link", "_blank")}>Demo Video</button>
    <button class="dark-mode-toggle" on:click={toggleDarkMode}>
      {isDarkMode ? "Light Mode" : "Dark Mode"}
    </button>
  </div>
</nav>

<!-- Popup -->
{#if showPopup}
  <div class="popup">{popupMessage}</div>
{/if}
