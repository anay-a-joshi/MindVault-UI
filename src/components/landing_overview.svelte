<script>
  export let title = "Your private 100% customizable online journal.";
  export let description = "Loved by users around the world, our app empowers you to track your thoughts and improve your mental well-being.";
  export let buttonLabel = "Start journaling now";
  export let imageUrl = "https://cdn.who.int/media/images/default-source/mental-health-and-substance-abuse/adobestock_178067240_preview.tmb-1920v.jpeg?sfvrsn=8c73c66c_6"; 
</script>

<style>
  .hero {
    display: flex;
    height: 100vh;
    justify-content: space-between;
    align-items: center;
    padding: 2rem 4rem;
    background-color: #fff5f0;
    font-family: 'Arial', sans-serif;
  }

  .content {
    flex: 1;
    max-width: 50%;
  }

  .title {
    font-size: 2.5rem;
    font-weight: bold;
    margin-bottom: 1rem;
    color: #333;
  }

  .description {
    font-size: 1.2rem;
    line-height: 1.6;
    margin-bottom: 2rem;
    color: #555;
  }

  .cta-button {
    display: inline-block;
    padding: 1rem 2rem;
    background-color: #ff6347;
    color: white;
    font-weight: bold;
    text-decoration: none;
    border-radius: 5px;
    transition: background-color 0.3s;
  }

  .cta-button:hover {
    background-color: #e5533f;
  }
</style>

<div class="hero">
  <div class="content">
    <h1 class="title">{title}</h1>
    <p class="description">{description}</p>
    <a href="#journal-entry-form" class="cta-button">{buttonLabel}</a>
  </div>
  <div class="hero-image">
    <!-- svelte-ignore a11y-img-redundant-alt -->
    <img src={imageUrl} alt="Journal Image" />
  </div>
</div>
