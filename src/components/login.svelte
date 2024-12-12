<script>
    import { createEventDispatcher } from 'svelte';

    let username = '';
    let password = '';
    let isLogin = true;
    const dispatch = createEventDispatcher();

    let isBreathingIn = true; // Track inhale/exhale state
    let isDarkMode = false; // Track dark mode state

    // Handle login
    const handleLogin = () => {
        const storedUser = JSON.parse(localStorage.getItem(username));
        if (storedUser && storedUser.password === password) {
            alert(`🎉 Welcome back, ${username}!`);
            localStorage.setItem('username', username); // Save username to localStorage
            dispatch('login', { username }); // Dispatch login event
            resetFields();
        } else {
            alert('❌ Invalid credentials! Please try again or create an account.');
        }
    };

    // Handle sign-up
    const handleSignUp = () => {
        const storedUser = JSON.parse(localStorage.getItem(username));
        if (storedUser) {
            alert('😄 User already exists. Please log in.');
        } else {
            const newUser = { username, password };
            localStorage.setItem(username, JSON.stringify(newUser));
            alert('✅ Account created successfully! Please log in.');
            isLogin = true;
        }
        resetFields();
    };

    // Submit handler
    const handleSubmit = () => {
        if (isLogin) {
            handleLogin();
        } else {
            handleSignUp();
        }
    };

    // Toggle between login and sign-up
    const toggleMode = () => {
        isLogin = !isLogin;
        resetFields();
    };

    // Reset input fields
    const resetFields = () => {
        username = '';
        password = '';
    };

    // Breathing animation cycle
    const cycleBreathing = () => {
        setInterval(() => {
            isBreathingIn = !isBreathingIn;
        }, 5000); // Switch every 5 seconds
    };

    // Toggle dark mode for the login container
    const toggleDarkMode = () => {
        isDarkMode = !isDarkMode;
        document.documentElement.style.setProperty(
            '--circle-color-light',
            isDarkMode ? 'rgba(0, 0, 0, 0.4)' : 'rgba(255, 255, 255, 0.2)'
        );
    };

    cycleBreathing(); // Start breathing cycle
</script>


<style>
    :root {
        --circle-color-light: rgba(255, 255, 255, 0.2); /* Light mode color */
        --circle-color-dark: rgba(0, 0, 0, 0.4); /* Dark mode color */
    }

    .login-container {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100vh;
        background: linear-gradient(135deg, #ff6347, #ffe4b5);
        font-family: 'Arial', sans-serif;
        color: #333;
        padding: 1rem;
    }

    .header {
        font-size: 2.5rem;
        color: #fff;
        margin-bottom: 1rem;
        text-align: center;
        font-weight: bold;
        text-transform: uppercase;
        text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.2);
    }

    .breathing-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 200px;
        height: 200px;
        border-radius: 50%;
        background: var(--circle-color-light); /* Use CSS variable for color */
        box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
        margin-bottom: 2rem;
        transition: transform 5s ease-in-out, background 0.3s ease;
    }

    .breathing-text {
        color: #fff;
        font-size: 1.5rem;
        font-weight: bold;
        text-align: center;
    }

    .login-box {
        background: #fff;
        border-radius: 16px;
        padding: 2rem;
        width: 100%;
        max-width: 400px;
        text-align: center;
        box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        box-sizing: border-box;
    }

    input {
        margin: 1rem 0;
        padding: 1rem;
        width: calc(100% - 2rem);
        border-radius: 8px;
        border: 1px solid #ddd;
        font-size: 1rem;
        transition: all 0.3s ease;
        box-sizing: border-box;
    }

    input:focus {
        outline: none;
        border-color: #ff6347;
        box-shadow: 0 0 8px rgba(255, 99, 71, 0.3);
    }

    .button {
        margin-top: 1.5rem;
        padding: 0.8rem;
        border: none;
        border-radius: 8px;
        background: linear-gradient(135deg, #ff6347, #ffa07a);
        color: #fff;
        font-size: 1.2rem;
        font-weight: bold;
        cursor: pointer;
        width: 100%;
        transition: background 0.3s ease, transform 0.2s ease;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }

    .button:hover {
        background: linear-gradient(135deg, #ffa07a, #ff6347);
        transform: translateY(-2px);
    }

    .button:active {
        transform: translateY(0);
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
    }

    .toggle-button {
        margin-top: 1rem;
        background: transparent;
        color: #ff6347;
        border: none;
        font-size: 1rem;
        cursor: pointer;
        transition: color 0.3s ease;
    }

    .toggle-button:hover {
        color: #e5533f;
    }

    @media (max-width: 600px) {
        .header {
            font-size: 2rem;
        }

        .login-box {
            padding: 1.5rem;
        }

        .breathing-text {
            font-size: 1.2rem;
        }
    }
</style>


<div class="login-container">
    <div class="header">MindVault</div>

    <!-- Breathing Exercise -->
    <div
        class="breathing-container"
        style="transform: scale({isBreathingIn ? 1.2 : 0.8})"
    >
        <div class="breathing-text">{isBreathingIn ? 'Inhale...' : 'Exhale...'}</div>
    </div>

    <div class="login-box">
        <h2>{isLogin ? 'Welcome Back!' : 'Join MindVault'}</h2>
        <input type="text" bind:value={username} placeholder="Enter Your Name" />
        <input type="password" bind:value={password} placeholder="Enter Your Password" />
        <button class="button" on:click={handleSubmit}>
            {isLogin ? 'Log In' : 'Sign Up'}
        </button>
        <button class="toggle-button" on:click={toggleMode}>
            {isLogin ? "Don't have an account? Sign Up" : 'Already a member? Log In'}
        </button>
    </div>
</div>