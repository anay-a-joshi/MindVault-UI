<script>
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';

  let testimonials = [
    {
      name: "Sarah Johnson",
      username: "@sarahj",
      image: "https://randomuser.me/api/portraits/women/1.jpg",
      content: "MindScribe has transformed my journaling experience. It's intuitive, beautiful, and helps me stay consistent!",
      rating: 5
    },
    {
      name: "Michael Chen",
      username: "@mikechen",
      image: "https://randomuser.me/api/portraits/men/2.jpg",
      content: "As a busy professional, MindScribe helps me reflect on my day and set goals. It's become an essential part of my routine.",
      rating: 4
    },
    {
      name: "Emily Rodriguez",
      username: "@emrod",
      image: "https://randomuser.me/api/portraits/women/3.jpg",
      content: "I love how MindScribe offers prompts and templates. It's helped me overcome writer's block and explore new aspects of myself.",
      rating: 5
    }
  ];

  let currentIndex = 0;
  let interval;

  onMount(() => {
    interval = setInterval(() => {
      currentIndex = (currentIndex + 1) % testimonials.length;
    }, 5000);

    return () => clearInterval(interval);
  });

  function setTestimonial(index) {
    currentIndex = index;
    clearInterval(interval);
  }
</script>

<div id="testimonials" class="testimonials-section">
  <h2 class="title">Loved by millions worldwide</h2>
  <div class="testimonial-carousel">
    {#key currentIndex}
      <div class="testimonial-card" in:fly="{{ y: 50, duration: 500 }}" out:fade>
        <div class="user-info">
          <img src={testimonials[currentIndex].image} alt="{testimonials[currentIndex].name}'s picture" />
          <div class="name">{testimonials[currentIndex].name}</div>
          <div class="username">{testimonials[currentIndex].username}</div>
        </div>
        <p class="content">"{testimonials[currentIndex].content}"</p>
        <div class="rating">
          {#each Array(5) as _, i}
            <span class={i < testimonials[currentIndex].rating ? 'star filled' : 'star'}>★</span>
          {/each}
        </div>
      </div>
    {/key}
  </div>
  <div class="carousel-dots">
    {#each testimonials as _, i}
      <button class="dot {i === currentIndex ? 'active' : ''}" on:click={() => setTestimonial(i)}></button>
    {/each}
  </div>
</div>

<style>
  .testimonials-section {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 4rem 2rem;
    background: linear-gradient(135deg, #fff5f0, #ffdddd); /* Matching the background gradient */
    font-family: 'Arial', sans-serif;
    position: relative;
    overflow: hidden;
  }

  .testimonials-section:before {
    content: '';
    position: absolute;
    top: -50%;
    left: 50%;
    width: 200%;
    height: 200%;
    background: radial-gradient(circle, rgba(255, 99, 71, 0.2) 20%, transparent 70%);
    transform: translate(-50%, 0);
    z-index: 0;
  }

  .title {
    font-size: 2.5rem;
    font-weight: bold;
    margin-bottom: 3rem;
    color: #ff6347; /* Primary color */
    text-align: center;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
    z-index: 1;
  }

  .testimonial-carousel {
    width: 100%;
    max-width: 700px;
    margin: 0 auto;
    z-index: 1;
  }

  .testimonial-card {
    background: transparent; /* Remove solid background */
    padding: 2rem;
    text-align: center;
    border: none;
    box-shadow: none;
    transform: scale(0.95);
    transition: transform 0.3s ease, opacity 0.3s ease;
    opacity: 0.8; /* Slight transparency for non-active cards */
  }

  .testimonial-card.active {
    transform: scale(1);
    opacity: 1; /* Full visibility for the active card */
  }

  .user-info {
    margin-bottom: 1rem;
  }

  .user-info img {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    object-fit: cover;
    border: 3px solid #ffc107; /* Accent color */
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  }

  .name {
    font-size: 1.4rem; /* Increased for clarity */
    font-weight: bold;
    color: #333; /* Darker color for better contrast */
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2); /* Subtle shadow to pop text */
    margin-top: 0.5rem;
  }

  .username {
    font-size: 1rem;
    color: #555; /* Slightly darker for readability */
    margin-bottom: 1rem;
  }

  .content {
    font-size: 1.2rem; /* Increased for better visibility */
    color: #444; /* Slightly darker for contrast */
    line-height: 1.6;
    margin: 1.5rem 0;
    font-style: italic;
    text-shadow: 0.5px 0.5px 1px rgba(0, 0, 0, 0.1); /* Subtle shadow to lift text */
  }

  .rating {
    font-size: 1.5rem;
    display: flex;
    justify-content: center;
    gap: 0.2rem; /* Space between stars */
  }

  .star {
    opacity: 0.3; /* Non-filled stars */
    transition: color 0.3s ease, transform 0.2s ease;
  }

  .star.filled {
    opacity: 1;
    background: linear-gradient(45deg, #ff6347, #ffc107); /* Gradient color for filled stars */
    -webkit-background-clip: text; /* Clip the gradient to the text */
    -webkit-text-fill-color: transparent; /* Make the text transparent */
  }

  .star:hover {
    transform: scale(1.2); /* Add a hover effect for interactivity */
  }

  .rating .star.filled:hover {
    color: #03a9f4; /* Change color on hover for filled stars */
  }

  .carousel-dots {
    display: flex;
    justify-content: center;
    margin-top: 2rem;
    z-index: 1;
  }

  .dot {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    background-color: rgba(51, 51, 51, 0.3); /* Lighter dots */
    margin: 0 5px;
    border: none;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.3s ease;
  }

  .dot.active {
    background-color: #ff6347; /* Primary color for active dot */
    transform: scale(1.2);
  }

  @media (max-width: 768px) {
    .title {
      font-size: 2rem;
    }

    .content {
      font-size: 1.1rem; /* Adjust for smaller screens */
    }

    .user-info img {
      width: 80px;
      height: 80px;
    }

    .testimonial-card {
      padding: 1.5rem;
    }
  }
</style>
