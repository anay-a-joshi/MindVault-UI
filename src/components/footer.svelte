<script>
  const links = {
    MindScribe: [
      { name: "Free signup", href: "#", info: "Sign up for free and start your journaling journey today!" },
      { name: "MindScribe PRO", href: "#", info: "Unlock advanced features with our premium subscription." },
      { name: "Login", href: "#", info: "Access your personal journaling space." },
      { name: "Support", href: "#", info: "Get help and answers to your questions." },
      { name: "Terms & conditions", href: "#", info: "Read our terms of service." },
      { name: "Privacy policy", href: "#", info: "Learn how we protect your data and privacy." },
    ],
    journals: [
      { name: "Journal prompts", href: "#", info: "Get inspired with our daily writing prompts." },
      { name: "What is a journal?", href: "#", info: "Learn about the benefits and types of journaling." },
      { name: "Pregnancy journal", href: "#", info: "Document your pregnancy journey." },
      { name: "Reflective journal", href: "#", info: "Enhance self-awareness through reflective writing." },
      { name: "Bible journal", href: "#", info: "Combine faith and journaling for spiritual growth." },
      { name: "Dream journal", href: "#", info: "Record and analyze your dreams." },
      { name: "Journal examples", href: "#", info: "See sample entries to inspire your writing." },
      { name: "Five year journal", href: "#", info: "Track your growth over a five-year period." },
    ],
    diaries: [
      { name: "Secret diary", href: "#", info: "Keep your thoughts private and secure." },
      { name: "Electronic diary", href: "#", info: "Digital journaling for the modern age." },
      { name: "Diary templates", href: "#", info: "Customizable templates for various diary styles." },
      { name: "Wedding diary", href: "#", info: "Capture memories of your special day." },
      { name: "School diary", href: "#", info: "Stay organized throughout the academic year." },
      { name: "Health diary", href: "#", info: "Track your wellness journey." },
      { name: "Food diary", href: "#", info: "Monitor your eating habits and nutritional intake." },
    ],
  };

  function showPopup(info) {
    alert(info);
  }
</script>

<div id="contact" class="footer">
  <div class="footer-content">
    <!-- Branding -->
    <div class="footer-header">
      <h1>MindScribe</h1>
      <div class="span">
        <h3>The #1 choice for journaling...</h3>
      </div>
    </div>

    <!-- Links -->
    <div class="footer-links">
      <div>
        <h4>MindScribe (Future Work)</h4>
        <ul>
          {#each links.MindScribe as link}
            <li><a href={link.href} on:click|preventDefault={() => showPopup(link.info)}>{link.name}</a></li>
          {/each}
        </ul>
      </div>
      <div>
        <h4>Journals (Future Work)</h4>
        <ul>
          {#each links.journals as link}
            <li><a href={link.href} on:click|preventDefault={() => showPopup(link.info)}>{link.name}</a></li>
          {/each}
        </ul>
      </div>
      <div>
        <h4>Diaries (Future Work)</h4>
        <ul>
          {#each links.diaries as link}
            <li><a href={link.href} on:click|preventDefault={() => showPopup(link.info)}>{link.name}</a></li>
          {/each}
        </ul>
      </div>
    </div>
  </div>

  <!-- Footer Bottom -->
  <div class="footer-bottom">
    <span>© 2024 MindScribe Inc. Empowering journeys, one word at a time.</span>
    <div class="social-icons">
      <a href="#" aria-label="Twitter" on:click|preventDefault={() => showPopup("Follow us on Twitter for daily journaling tips!")}>🐦 Twitter</a>
      <a href="#" aria-label="Facebook" on:click|preventDefault={() => showPopup("Join our Facebook community for journaling enthusiasts!")}>📘 Facebook</a>
      <a href="#" aria-label="Instagram" on:click|preventDefault={() => showPopup("Get inspired by beautiful journal spreads on our Instagram!")}>📸 Instagram</a>
      <a href="#" aria-label="LinkedIn" on:click|preventDefault={() => showPopup("Connect with us on LinkedIn for professional journaling insights!")}>🔗 LinkedIn</a>
      <a href="#" aria-label="YouTube" on:click|preventDefault={() => showPopup("Watch our YouTube channel for journaling tutorials and tips!")}>📺 YouTube</a>
    </div>
  </div>
</div>




<style>
  .footer {
    background-color: #ff6347;
    margin-top: 100px;
    padding: 2rem;
    font-family: "Arial", sans-serif;
    color: #555;
  }

  .footer-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 2rem;
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 1rem;
  }

  .footer-header {
    text-align: center;
    color: black;
    margin-bottom: 1rem;
  }

  .footer-header h1 {
    margin-bottom: 0.5rem;
  }

  .span {
    color: ghostwhite;
  }

  .footer-links {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    width: 100%;
    gap: 2rem;
  }

  .footer-links > div {
    flex: 1;
    min-width: 200px;
  }

  .footer-links h4 {
    font-size: 1.1rem;
    font-weight: bold;
    margin-bottom: 1rem;
    color: black;
  }

  .footer-links ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  .footer-links ul li {
    margin-bottom: 0.5rem;
  }

  .footer-links ul li a {
    text-decoration: none;
    color: ghostwhite;
    font-size: 0.9rem;
    transition: color 0.3s ease;
  }

  .footer-links ul li a:hover {
    color: #007bff;
    text-decoration: underline;
  }

  .footer-bottom {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    max-width: 1200px;
    margin: 2rem auto 0;
    padding-top: 1rem;
    border-top: 1px solid rgba(255, 255, 255, 0.2);
    font-size: 0.9rem;
    color: black;
    text-align: center;
    gap: 1rem;
  }

  .social-icons {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin-top: 1rem;
  }

  .social-icons a {
    text-decoration: none;
    font-size: 1rem;
    color: black;
    transition: color 0.3s ease;
  }

  .social-icons a:hover {
    color: #ffffff;
  }

  @media (max-width: 768px) {
    .footer-links {
      flex-direction: column;
    }

    .footer-links > div {
      width: 100%;
    }
  }
  
</style>

