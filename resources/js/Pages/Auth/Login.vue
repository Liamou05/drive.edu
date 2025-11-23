<script setup>
import { ref } from 'vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

defineProps({
    canResetPassword: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});

const showPassword = ref(false);

const form = useForm({
    email: '',
    password: '',
    remember: false,
});

const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
</script>

<template>
    <Head title="Log in - Drive.edu" />
    
    <div class="login-page">
        <!-- Navigation -->
        <nav class="nav">
            <!-- <Link href="/" class="logo">
                Drive<span class="logo-dot">.</span>edu
            </Link> -->
        </nav>

        <!-- Login Container -->
        <div class="login-container">
            <div class="login-box">
                <!-- Header -->
                <div class="header">
                    <h1 class="title">Welcome back</h1>
                    <p class="subtitle">Sign in to continue your driving journey</p>
                </div>

                <!-- Status Message -->
                <div v-if="status" class="status-message">
                    {{ status }}
                </div>

                <!-- Login Form -->
                <form @submit.prevent="submit" class="form">
                    <!-- Email Input -->
                    <div class="input-group">
                        <label for="email" class="label">Email</label>
                        <input
                            id="email"
                            type="email"
                            v-model="form.email"
                            required
                            autofocus
                            autocomplete="username"
                            class="input"
                            :class="{ 'input-error': form.errors.email }"
                            placeholder="you@example.com"
                        />
                        <p v-if="form.errors.email" class="error-message">
                            {{ form.errors.email }}
                        </p>
                    </div>

                    <!-- Password Input -->
                    <div class="input-group">
                        <label for="password" class="label">Password</label>
                        <div class="password-wrapper">
                            <input
                                id="password"
                                :type="showPassword ? 'text' : 'password'"
                                v-model="form.password"
                                required
                                autocomplete="current-password"
                                class="input"
                                :class="{ 'input-error': form.errors.password }"
                                placeholder="Enter your password"
                            />
                            <button
                                type="button"
                                @click="showPassword = !showPassword"
                                class="toggle-password"
                                tabindex="-1"
                            >
                                <svg v-if="!showPassword" class="eye-icon" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                                </svg>
                                <svg v-else class="eye-icon" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.88 9.88l-3.29-3.29m7.532 7.532l3.29 3.29M3 3l3.59 3.59m0 0A9.953 9.953 0 0112 5c4.478 0 8.268 2.943 9.543 7a10.025 10.025 0 01-4.132 5.411m0 0L21 21" />
                                </svg>
                            </button>
                        </div>
                        <p v-if="form.errors.password" class="error-message">
                            {{ form.errors.password }}
                        </p>
                    </div>

                    <!-- Remember Me & Forgot Password -->
                    <div class="form-options">
                        <label class="checkbox-label">
                            <input
                                type="checkbox"
                                v-model="form.remember"
                                class="checkbox"
                            />
                            <span>Remember me</span>
                        </label>

                        <Link
                            v-if="canResetPassword"
                            :href="route('password.request')"
                            class="forgot-link"
                        >
                            Forgot password?
                        </Link>
                    </div>

                    <!-- Submit Button -->
                    <button
                        type="submit"
                        class="submit-btn"
                        :class="{ 'submit-btn-loading': form.processing }"
                        :disabled="form.processing"
                    >
                        <span v-if="form.processing" class="loader"></span>
                        <span v-else>Sign in</span>
                    </button>

                    <!-- Register Link -->
                    <div class="register-section">
                        <p class="register-text">
                            Don't have an account?
                            <Link :href="route('register')" class="register-link">
                                Sign up
                            </Link>
                        </p>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.login-page {
    font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    background: #fafafa;
    min-height: 100vh;
    color: #1a1a1a;
}

.nav {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    padding: 1.5rem 3rem;
    z-index: 100;
    background: rgba(255, 255, 255, 0.8);
    backdrop-filter: blur(10px);
    border-bottom: 1px solid #e5e7eb;
}

.logo {
    font-size: 1.25rem;
    font-weight: 700;
    color: #1a1a1a;
    text-decoration: none;
    letter-spacing: -0.02em;
    transition: opacity 0.3s ease;
}

.logo:hover {
    opacity: 0.7;
}

.logo-dot {
    color: #10b981;
}

.login-container {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    padding: 2rem 1rem;
}

.login-box {
    width: 100%;
    max-width: 420px;
    background: #ffffff;
    padding: 3rem 2.5rem;
    border-radius: 16px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.02), 0 10px 30px rgba(0, 0, 0, 0.04);
    animation: fadeInUp 0.5s ease;
}

.header {
    margin-bottom: 2rem;
}

.title {
    font-size: 1.875rem;
    font-weight: 700;
    color: #1a1a1a;
    margin-bottom: 0.5rem;
    letter-spacing: -0.02em;
}

.subtitle {
    font-size: 0.9375rem;
    color: #6b7280;
    font-weight: 400;
}

.status-message {
    background: #d1fae5;
    border-left: 4px solid #10b981;
    color: #065f46;
    padding: 0.875rem 1rem;
    border-radius: 6px;
    font-size: 0.875rem;
    margin-bottom: 1.5rem;
}

.form {
    display: flex;
    flex-direction: column;
    gap: 1.25rem;
}

.input-group {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.label {
    font-size: 0.875rem;
    font-weight: 600;
    color: #1a1a1a;
}

.input {
    width: 100%;
    padding: 0.75rem 1rem;
    border: 1.5px solid #e5e7eb;
    border-radius: 10px;
    font-size: 0.9375rem;
    color: #1a1a1a;
    transition: all 0.2s ease;
    background: #fafafa;
}

.input::placeholder {
    color: #9ca3af;
}

.input:focus {
    outline: none;
    border-color: #1a1a1a;
    background: #ffffff;
    box-shadow: 0 0 0 4px rgba(26, 26, 26, 0.05);
}

.input-error {
    border-color: #ef4444;
    background: #fef2f2;
}

.input-error:focus {
    border-color: #ef4444;
    box-shadow: 0 0 0 4px rgba(239, 68, 68, 0.1);
}

.error-message {
    font-size: 0.8125rem;
    color: #ef4444;
    font-weight: 500;
}

.password-wrapper {
    position: relative;
}

.toggle-password {
    position: absolute;
    right: 0.875rem;
    top: 50%;
    transform: translateY(-50%);
    background: none;
    border: none;
    cursor: pointer;
    padding: 0.25rem;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #9ca3af;
    transition: color 0.2s ease;
    border-radius: 4px;
}

.toggle-password:hover {
    color: #6b7280;
}

.toggle-password:focus {
    outline: 2px solid #1a1a1a;
    outline-offset: 2px;
}

.eye-icon {
    width: 20px;
    height: 20px;
}

.form-options {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-top: 0.25rem;
}

.checkbox-label {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    cursor: pointer;
    font-size: 0.875rem;
    color: #374151;
    font-weight: 500;
}

.checkbox {
    width: 17px;
    height: 17px;
    border-radius: 5px;
    border: 1.5px solid #d1d5db;
    cursor: pointer;
    accent-color: #1a1a1a;
}

.forgot-link {
    font-size: 0.875rem;
    color: #1a1a1a;
    text-decoration: none;
    font-weight: 600;
    transition: all 0.2s ease;
    border-bottom: 1px solid transparent;
}

.forgot-link:hover {
    color: #10b981;
    border-bottom-color: #10b981;
}

.submit-btn {
    width: 100%;
    padding: 0.875rem 1rem;
    background: #1a1a1a;
    color: #ffffff;
    border: none;
    border-radius: 10px;
    font-size: 0.9375rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s ease;
    margin-top: 0.75rem;
}

.submit-btn:hover:not(:disabled) {
    background: #000000;
    transform: translateY(-1px);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.submit-btn:active:not(:disabled) {
    transform: translateY(0);
}

.submit-btn:disabled {
    opacity: 0.6;
    cursor: not-allowed;
}

.submit-btn-loading {
    display: flex;
    align-items: center;
    justify-content: center;
}

.loader {
    width: 18px;
    height: 18px;
    border: 2.5px solid rgba(255, 255, 255, 0.3);
    border-top-color: #ffffff;
    border-radius: 50%;
    animation: spin 0.7s linear infinite;
}

.register-section {
    text-align: center;
    margin-top: 0.5rem;
}

.register-text {
    font-size: 0.875rem;
    color: #6b7280;
}

.register-link {
    color: #1a1a1a;
    text-decoration: none;
    font-weight: 700;
    transition: all 0.2s ease;
    border-bottom: 1.5px solid transparent;
}

.register-link:hover {
    color: #10b981;
    border-bottom-color: #10b981;
}

@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(20px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

@keyframes spin {
    to {
        transform: rotate(360deg);
    }
}

/* Tablet */
@media (max-width: 768px) {
    .nav {
        padding: 1.25rem 2rem;
    }
    
    .logo {
        font-size: 1.15rem;
    }
    
    .login-box {
        padding: 2.5rem 2rem;
    }
    
    .title {
        font-size: 1.625rem;
    }
}

/* Mobile */
@media (max-width: 480px) {
    .nav {
        padding: 1rem 1.25rem;
    }
    
    .logo {
        font-size: 1.1rem;
    }
    
    .login-box {
        padding: 2rem 1.5rem;
        border-radius: 12px;
    }
    
    .title {
        font-size: 1.5rem;
    }
    
    .subtitle {
        font-size: 0.875rem;
    }
    
    .form-options {
        flex-direction: column;
        align-items: flex-start;
        gap: 0.875rem;
    }
}
</style>