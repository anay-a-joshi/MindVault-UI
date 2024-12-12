<script>
  import { fade } from 'svelte/transition';

  const features = [
    {
      icon: "📄",
      title: "Unlimited entries",
      description: "Write as much and as often as you like, all for free.",
      detailedInfo:
        "Our platform allows you to create an unlimited number of journal entries without any restrictions. Whether you want to write daily, weekly, or sporadically, you have the freedom to express yourself without worrying about hitting a limit or having to pay for additional entries.",
    },
    {
      icon: "📱",
      title: "Mobile apps",
      description: "Write in your journal on the go with our mobile apps.",
      detailedInfo:
        "Our iOS and Android apps allow you to take your journaling experience anywhere. Sync your entries seamlessly across devices and never miss a moment of inspiration.",
    },
    {
      icon: "💾",
      title: "Saves as you go",
      description: "Your work is saved automatically as you type.",
      detailedInfo:
        "With our auto-save feature, you never have to worry about losing your progress. Whether you're writing on your computer or mobile device, your entries are securely saved in real time.",
    },
    {
      icon: "📚",
      title: "Custom journals",
      description: "Personalize your journals with unique designs.",
      detailedInfo:
        "Choose from a variety of covers, backgrounds, fonts, and layouts to make each journal truly yours. Tailor your journaling experience to reflect your personality and style.",
    },
    {
      icon: "⏰",
      title: "Reminders",
      description: "Set reminders to stay consistent with journaling.",
      detailedInfo:
        "Never forget to write in your journal again. Set daily, weekly, or custom reminders to keep up with your journaling habits and make it a part of your routine.",
    },
    {
      icon: "❤️",
      title: "So much more...",
      description:
        "Enjoy encryption, tagging, prompts, and more features.",
      detailedInfo:
        "Our platform offers a wide range of features designed to enhance your journaling experience, including encryption for privacy, tagging for organization, writing prompts for inspiration, and much more.",
    },
  ];

  let selectedFeature = null;

  function showPopup(feature) {
    selectedFeature = feature;
  }

  function closePopup() {
    selectedFeature = null;
  }
</script>

<div id="feature" class="features-section">
  <h2>Key Features</h2>
  <div class="features-grid">
    {#each features as feature}
      <div
        class="feature-item"
        on:click={() => showPopup(feature)}
        data-description={feature.description}
      >
        <div class="icon">{feature.icon}</div>
        <div class="title">{feature.title}</div>
        <p class="hover-description">{feature.description}</p>
      </div>
    {/each}
  </div>

  {#if selectedFeature}
  <div class="popup-overlay" on:click={closePopup}>
    <div class="popup-box" in:fade out:fade on:click|stopPropagation>
      <button class="close-btn" on:click={closePopup} aria-label="Close">×</button>
      <div class="popup-icon">{selectedFeature.icon}</div>
      <h3>{selectedFeature.title}</h3>
      <p>{selectedFeature.detailedInfo}</p>
    </div>
  </div>
{/if}

</div>

<style>
  .features-section {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 2rem;
    background-color: #ff6347;
    font-family: 'Arial', sans-serif;
    margin-bottom: 50px;
  }

  .features-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2rem;
    max-width: 1200px;
    width: 100%;
  }

  .feature-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    background-color: #ffffff;
    padding: 1.5rem;
    border-radius: 10px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    position: relative; /* For hover effect */
    cursor: pointer;
    overflow: hidden; /* Hide hover text overflow */
    transition: transform 0.3s ease;
  }

  .feature-item:hover {
    transform: translateY(-5px);
  }

  .icon {
    font-size: 2.5rem;
    margin-bottom: 1rem;
    color: #007bff;
  }

  .title {
    font-size: 1.2rem;
    font-weight: bold;
    margin-bottom: 0.5rem;
    color: #333;
  }

  .hover-description {
    font-size: 0.9rem;
    color: #555;
    line-height: 1.4;
    margin-top: auto; /* Push description to bottom */
  }

  /* Popup Styles */
  .popup-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    backdrop-filter: blur(5px);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
  }

  .popup-box {
    background-color: #fff;
    border-radius: 10px;
    padding: 2rem;
    text-align: center;
    box-shadow: 0 8px 20px rgba(0,0,0,0.2);
    max-width: 400px;
    width: calc(100% - 2rem);
    position: relative;
  }

  .close-btn {
    position: absolute;
    top: 10px;
    right: 10px;
    background: transparent;
    border: none;
    font-size: 1.5rem;
    cursor: pointer;
    color: #333;
    transition: color 0.3s ease;
  }

  .close-btn:hover {
    color: #ff6347;
  }

  </style>

