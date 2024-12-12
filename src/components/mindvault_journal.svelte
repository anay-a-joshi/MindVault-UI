<script>
  // Name: Anay Abhijit Joshi
  // CS 5167: User Interface 1
  // Level: Undergraduate Student

//   import Login from './user_login.svelte';
  import Feelings from './emotional_pulse.svelte';
  import ImageUpload from './moment_capture.svelte';
  import Reflection from './journaling.svelte';
  import SkillPractice from './skill_time.svelte';
  import YogaDuration from './meditation.svelte';
  import UserInfo from './user_profile.svelte';
  import WaterIntake from './body_hydration.svelte';
  import ProductivityChart from './visual_overview.svelte';
  import Progress from './activity_tracker.svelte';
  import LogMoreActivity from './add_activity.svelte'; // Import the new component
  import RemoveActivity from './delete_activity.svelte';
  import FruitTracker from './body_fuel.svelte';

  // Your existing variables and functions
  let wantsToRemove = false;
  let activityToRemove = '';
  let showActivityPopup = true; // Control the visibility of the popup

  export let username = ''; // Passed from App.svelte
  
  let skill = '';

  // const handleActivitySubmit = () => {
  //     if (skill.trim() === '') {
  //       alert('Please enter a valid skill!');
  //       return;
  //     }
  //     alert(`Great! You've set your focus on "${skill}".`);
  //     showActivityPopup = false;
  //   };

  const handleActivitySubmit = () => {
    if (skill.trim() === '') {
      alert('Please enter a valid skill!');
      return;
    }
    showActivityPopup = false; // Close the popup first
    setTimeout(() => {
      alert(`Great! You've set your focus on "${skill}".`);
    }, 100); // Delay the alert by 100ms to prevent the popup from closing too soon
  };


  let wantsToLogMore = false;  // Track if user wants to log more
  let newActivity = '';        // Variable for storing the new activity input

  // Theme toggle state
  let isDarkMode = false;

  let fruitIntake = 0; // Variable to track the fruit intake in App.svelte

  // Helper to toggle between themes
  const toggleTheme = () => {
      isDarkMode = !isDarkMode;
      document.documentElement.setAttribute('data-theme', isDarkMode ? 'dark' : 'light');
    };

  let loggedIn = false;  // Track if user is logged in
  let user = { username: username || '', startDate: new Date() };
  let currentDate = new Date();  // Current date for user information
  let selectedDate = new Date();  // Default is today's date
  let daysActive = 1;

  // Journal Data
  let feelings = [
  { mood: 'Energetic', description: 'Full of energy and ready to take on the day', checked: false },
  { mood: 'Calm', description: 'Feeling peaceful and free from stress', checked: false },
  { mood: 'Reflective', description: 'Deep in thought, contemplating life or choices', checked: false },
  { mood: 'Anxious', description: 'Experiencing worry or nervousness about something', checked: false },
  { mood: 'Content', description: 'Satisfied and at ease with life', checked: false },
  { mood: 'Frustrated', description: 'Feeling stuck or annoyed with a situation', checked: false },
  { mood: 'Thankful', description: 'Grateful for the small and big joys in life', checked: false },
  { mood: 'Lonely', description: 'Feeling isolated or disconnected from others', checked: false },
  { mood: 'Motivated', description: 'Driven to achieve goals and overcome challenges', checked: false },
  { mood: 'Exhausted', description: 'Physically or mentally worn out', checked: false },
  { mood: 'Hopeful', description: 'Feeling optimistic about the future and possibilities', checked: false },
  { mood: 'Creatively Inspired', description: 'Bursting with new ideas and artistic energy', checked: false }
];

  let image = '';
  let dailyReflection = '';
  let skillPractice = 0;
  let didYoga = false;
  let yogaDuration = 0;
  let waterIntake = 0;

  // Productivity data for chart
  let productivityData = [skillPractice * 60 , yogaDuration / 60 , waterIntake * 80];

  // Progress tracking logic
  let skillPracticeGoal = 5; // Example: 60 minutes skill practice per day
  let yogaGoal = 100; // Example: 30 minutes yoga per day
  let waterGoal = 4; // Example: 2000 ml water intake per day

  let skillPracticeProgress = (skillPractice / skillPracticeGoal) * 100;
  let yogaProgress = (yogaDuration / yogaGoal) * 4;
  let waterIntakeProgress = ((waterIntake) / waterGoal) * 4;

  // Helper function to format date as YYYY-MM-DD for input value
  const formatDateForInput = (date) => date.toISOString().split('T')[0];
  
  const onLoginSuccess = (event) => {
    user.username = event.detail.username;
    retrieveJournalData();
    setTimeout(() => {
      skill = prompt(`Hi ${user.username}, what specific skill would you like to focus on improving today? 🤔`) || 'Skill';
    }, 100);
  };

  const onDateChange = (event) => {
    selectedDate = new Date(event.target.value);
    retrieveJournalData();
  };

  // Save journal data in localStorage for the selected date
  const saveJournalData = () => {
      const journalData = {
        feelings,
        image,
        dailyReflection,
        skillPractice,
        didYoga,
        yogaDuration,
        waterIntake,
        wantsToLogMore,
        newActivity,
        wantsToRemove,
        activityToRemove,
        fruitIntake,
      };
  
      const formattedDate = formatDateForInput(selectedDate);
      const key = `${user.username}_journal_${formattedDate}`;
      localStorage.setItem(key, JSON.stringify(journalData));
  
      productivityData = [skillPractice, yogaDuration / 60, waterIntake];
      skillPracticeProgress = (skillPractice / skillPracticeGoal) * 100;
      yogaProgress = (yogaDuration / yogaGoal) * 100;
      waterIntakeProgress = (waterIntake / waterGoal) * 100;
  
      alert('Success! Journal has been saved. ✅');
    };

  // Retrieve journal data from localStorage and populate the fields for the selected date
  const retrieveJournalData = () => {
      const formattedDate = formatDateForInput(selectedDate);
      const key = `${user.username}_journal_${formattedDate}`;
      const savedData = localStorage.getItem(key);
  
      if (savedData) {
        const journalData = JSON.parse(savedData);
        ({ feelings, image, dailyReflection, skillPractice, didYoga, yogaDuration, waterIntake, wantsToLogMore, newActivity, wantsToRemove, activityToRemove, fruitIntake } = journalData);
  
        productivityData = [skillPractice, yogaDuration / 60, waterIntake];
        skillPracticeProgress = (skillPractice / skillPracticeGoal) * 100;
        yogaProgress = (yogaDuration / yogaGoal) * 100;
        waterIntakeProgress = (waterIntake / waterGoal) * 100;
      } else {
        resetFields();
      }
    };

    const resetFields = () => {
      feelings.forEach((feeling) => (feeling.checked = false));
      image = '';
      dailyReflection = '';
      skillPractice = 0;
      didYoga = false;
      yogaDuration = 0;
      waterIntake = 0;
      wantsToLogMore = false;
      newActivity = '';
      wantsToRemove = false;
      activityToRemove = '';
      fruitIntake = 0;
  
      productivityData = [0, 0, 0];
      skillPracticeProgress = 0;
      yogaProgress = 0;
      waterIntakeProgress = 0;
    };

  const handleJournalFetch = () => {
  const formattedDate = selectedDate.toISOString().split('T')[0];  // Format as YYYY-MM-DD
      const savedJournalData = localStorage.getItem(user.username + '_journal_' + formattedDate);

      if (savedJournalData) {
          retrieveJournalData();  // Fetch and populate journal data if it exists
          alert(`✅ Great! \nYour data entry for ${formattedDate} has been loaded successfully.`);
      } else {
          alert(`🥺 Oops! \nYou haven't logged any activity for ${formattedDate} yet. Please fill in your details to get started!`);  // Show alert if no data found
      }
  };
</script>

<main>
    {#if showActivityPopup}
        <div class="popup-overlay">
        <div class="popup">
            <h2>Welcome, {username}!</h2>
            <p>What specific skill would you like to focus on improving today?</p>
            <input
            type="text"
            bind:value={skill}
            placeholder="Enter activity (e.g., Yoga, Coding)"
            />
            <button class="submit-button" on:click={handleActivitySubmit}>Submit</button>
        </div>
        </div>
    {/if}
  

      <section id="journal-entry-form" class=" card user-info-section">
          <h2>Personalized Dashboard of {user.username}</h2>
          <UserInfo {user}  />
      </section>

      <!-- Date picker to select the date for the journal -->
      <section style="padding: 1rem; color: #1D3557;">
        <h2>Time Traveler: Explore Your Past Journey</h2>
        <div style="display: flex; flex-direction: column; gap: 1rem;">
            <label for="journal-date" style="font-size: 1rem; font-weight: bold; color: #1D3557;">
                Calendar Date:
            </label>
            <input type="date" id="journal-date" value={formatDateForInput(selectedDate)} on:change={onDateChange} 
                style="padding: 0.5rem; border: 1px solid #ddd; border-radius: 4px; font-size: 1rem;">
            
            <!-- Button with hover effect -->
            <button 
                on:click={handleJournalFetch} 
                class="my-button" 
                style="margin-top: 1rem; padding: 0.5rem; background-color: #FF6347; color: white; border: none; border-radius: 4px; cursor: pointer; font-size: 1rem;"
            >
                Fetch Previous Entry
            </button>
        </div>
    </section>

      <section class="card feelings-section">
          <h2>{user.username}'s Emotional Pulse Check</h2>
          <Feelings {feelings} />
      </section>

      <section class="card image-upload-section">
          <h2>{user.username}'s Moment Snap</h2>
          <ImageUpload bind:image />
      </section>

      <section style="padding: 1rem; color: #1D3557;">
        <h2>Mission Control: Set Your Goals</h2>
        <form style="display: flex; flex-direction: column; gap: 1rem;">
            <label for="skillPracticeGoal" style="font-size: 1rem; font-weight: bold; color: #1D3557;">
                Time Spent on {skill} (Hours) by {user.username}:
            </label>
            <input type="number" id="skillPracticeGoal" bind:value={skillPracticeGoal} min="1" 
                style="padding: 0.5rem; border: 1px solid #ddd; border-radius: 4px; font-size: 1rem;">
    
            <label for="yogaGoal" style="font-size: 1rem; font-weight: bold; color: #1D3557;">
                {user.username}'s Meditation Duration (Minutes):
            </label>
            <input type="number" id="yogaGoal" bind:value={yogaGoal} min="1" 
                style="padding: 0.5rem; border: 1px solid #ddd; border-radius: 4px; font-size: 1rem;">
    
            <label for="waterGoal" style="font-size: 1rem; font-weight: bold; color: #1D3557;">
                {user.username}'s Body Hydration Goal (Liters):
            </label>
            <input type="number" id="waterGoal" bind:value={waterGoal} step="0.1" min="0.1" 
                style="padding: 0.5rem; border: 1px solid #ddd; border-radius: 4px; font-size: 1rem;">
        </form>
    </section>

      <section class="card water-intake-section">
          <h2>{user.username}'s Hydration Hub</h2>
          <WaterIntake bind:waterIntake />
      </section>

      <section class="card reflection-section">
          <h2>Self-Reflection Zone of {user.username}</h2>
          <Reflection bind:dailyReflection />
      </section>

      <section class="card skill-practice-section">
          <h2>{skill}'s Mastery Tracker</h2>
          <SkillPractice bind:skillPractice {skill} />
      </section>

      <section class="card yoga-section">
          <h2>Relax and Recharge</h2>
          <YogaDuration bind:didYoga bind:yogaDuration />
      </section>

      <section class="card fruit-tracker-section">
          <h2>Fuel Up: Build Your Strength!</h2>
          <FruitTracker bind:fruitIntake />
      </section>

      <section class="card log-more-section">
          <h2>Expand Your Routine (Add)</h2>
          <LogMoreActivity bind:wantsToLogMore bind:newActivity />
      </section>

      <section class="card remove-activity-section">
          <h2>Streamline Your Activities (Remove)</h2>
          <RemoveActivity bind:wantsToRemove bind:activityToRemove />
      </section>

      <!-- Submit button to save journal data -->
      <button on:click={saveJournalData} class='submit'>Submit</button>

      <!-- Progress tracking for habits -->
      <section class="card progress-tracking-section">
          <h2>{user.username}'s Achievement Overview (in %)</h2>
          <Progress habitProgress={skillPracticeProgress} habitName="Average Time on {skill}" />
          <Progress habitProgress={yogaProgress} habitName="Average Stretching Duration" />
          <Progress habitProgress={waterIntakeProgress} habitName="Average Water Intake" />
      </section>

      <!-- Productivity Pie Chart -->
      <section class="card productivity-chart-section">
          <h2>{user.username}'s Performance Metrics Breakdown</h2>
          <ProductivityChart {productivityData} />
      </section>

</main>


<style>
    /* Root Variables for Colors and Fonts */
    :root {
      --primary-color: #ff6347; /* Tomato Red */
      --secondary-color: #ffc107; /* Yellow Accent */
      --background-gradient: linear-gradient(135deg, #fff5f0, #ffdddd); /* Soft Gradient */
      --text-color: #333; /* Dark Gray for Text */
      --highlight-color: #03a9f4; /* Light Blue */
      --shadow-color: rgba(0, 0, 0, 0.1);
      --font-family: 'Arial', sans-serif;
      --transition-speed: 0.3s;
    }
  
    /* Global Styles */
    body {
      margin: 0;
      font-family: var(--font-family);
      background: var(--background-gradient);
      color: var(--text-color);
    }
  
    main {
      padding: 2rem;
      max-width: 1200px;
      margin: 0 auto;
    }
  
    h2 {
      font-size: 2rem;
      color: var(--primary-color);
      font-weight: bold;
      margin-bottom: 1rem;
      text-shadow: 1px 1px 2px var(--shadow-color);
    }
  
    /* Section Layouts */
    section {
      margin-bottom: 3rem;
      padding: 1.5rem 0;
      position: relative;
      overflow: hidden;
    }
  
    section:before {
      content: '';
      position: absolute;
      top: 0;
      left: 50%;
      width: 200%;
      height: 200%;
      background: radial-gradient(circle, var(--primary-color) 0%, transparent 70%);
      transform: translateX(-50%) translateY(-80%);
      opacity: 0.05;
      pointer-events: none;
      z-index: -1;
    }
  
    section h2 {
      text-align: center;
    }
  
    /* Inputs and Buttons */
    input[type='date'],
    input[type='number'],
    textarea {
      width: 100%;
      padding: 0.8rem;
      font-size: 1rem;
      border: none;
      border-bottom: 2px solid var(--highlight-color);
      background: transparent;
      color: var(--text-color);
      transition: border-color var(--transition-speed);
      margin-top: 1rem;
    }
  
    input[type='date']:focus,
    input[type='number']:focus,
    textarea:focus {
      border-color: var(--secondary-color);
      outline: none;
    }
  
    button {
      padding: 0.8rem 2rem;
      font-size: 1rem;
      color: white;
      background: var(--primary-color);
      border: none;
      border-radius: 50px;
      cursor: pointer;
      font-weight: bold;
      transition: background-color var(--transition-speed), transform var(--transition-speed);
      box-shadow: 0 4px 10px var(--shadow-color);
    }
  
    button:hover {
      background: var(--secondary-color);
      transform: translateY(-3px);
    }
  
    /* Floating Elements */
    .floating {
      background: white;
      border-radius: 20px;
      padding: 2rem;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
      margin: 1rem auto;
      max-width: 700px;
      transition: transform var(--transition-speed), box-shadow var(--transition-speed);
    }

    html {
      scroll-behavior: smooth;
  }
  
    .floating:hover {
      transform: translateY(-5px);
      box-shadow: 0 12px 30px rgba(0, 0, 0, 0.2);
    }
  
    /* Feelings Section */
    .feelings-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
      gap: 1rem;
      justify-items: center;
      align-items: center;
    }
  
    .feeling {
      font-size: 1rem;
      color: var(--text-color);
      padding: 0.5rem 1rem;
      background: var(--secondary-color);
      border-radius: 20px;
      cursor: pointer;
      transition: background-color var(--transition-speed), color var(--transition-speed);
    }
  
    .feeling:hover {
      background: var(--primary-color);
      color: white;
    }
  
    /* Progress Bars */
    .progress {
      margin-top: 1rem;
      width: 100%;
      height: 12px;
      background: rgba(0, 0, 0, 0.1);
      border-radius: 6px;
      overflow: hidden;
      position: relative;
    }
  
    .progress-bar {
      height: 100%;
      background: var(--highlight-color);
      width: 0; /* Dynamically updated */
      transition: width var(--transition-speed);
    }
  
    /* Productivity Chart */
    .productivity-chart {
      display: flex;
      justify-content: center;
      align-items: center;
      position: relative;
      margin-top: 2rem;
      height: 300px;
      width: 300px;
      background: conic-gradient(var(--primary-color) 25%, var(--secondary-color) 25% 50%, var(--highlight-color) 50% 75%, var(--background-gradient) 75% 100%);
      border-radius: 50%;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }
  
    /* Responsive Design */
    @media (max-width: 768px) {
      h2 {
        font-size: 1.6rem;
      }
  
      button {
        font-size: 0.9rem;
      }
  
      .floating {
        padding: 1rem;
      }
    }

    .popup-overlay {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.5);
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 1000;
    }

    .popup {
        background: white;
        padding: 2rem;
        border-radius: 10px;
        width: 90%;
        max-width: 400px;
        text-align: center;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
    }

    .popup h2 {
        margin-bottom: 1rem;
        font-size: 1.5rem;
        color: #ff6347;
    }

    .popup p {
        margin-bottom: 1.5rem;
        color: #555;
    }

    .popup input {
        width: 100%;
        padding: 0.8rem;
        font-size: 1rem;
        margin-bottom: 1rem;
        border: 1px solid #ddd;
        border-radius: 5px;
        box-sizing: border-box;
    }

    .submit-button {
        padding: 0.8rem 1.5rem;
        background-color: #ff6347;
        color: white;
        border: none;
        border-radius: 5px;
        font-weight: bold;
        font-size: 1rem;
        cursor: pointer;
        transition: background-color 0.3s;
    }

    .submit-button:hover {
        background-color: #e5533f;
    }

    .my-button {
        background-color: #FF6347;
        color: white;
        transition: background-color 0.3s, color 0.3s; /* Smooth transition for hover effect */
    }

    .my-button:hover {
        background-color: #1D3557; /* Dark blue on hover */
        color: #FF6347; /* Tomato red text on hover */
    }
</style>
  



  
  