<script setup>
import { ref } from 'vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

const showPassword = ref(false);
const showPasswordConfirmation = ref(false);

const form = useForm({
    name: '',
    email: '',
    password: '',
    password_confirmation: '',
});

const submit = () => {
    form.post(route('register'), {
        onFinish: () => form.reset('password', 'password_confirmation'),
    });
};
</script>

<template>
    <Head title="Register - Drive.edu" />
    
    <div class="register-page">
        <!-- Login Container -->
        <div class="register-container">
            <div class="register-box">
                <!-- Header -->
                <div class="header">
                    <h1 class="title">Create your account</h1>
                    <p class="subtitle">Start your driving journey with Drive.edu</p>
                </div>

                <!-- Register Form -->
                <form @submit.prevent="submit" class="form">
                    <!-- Name Input -->
                    <div class="input-group">
                        <label for="name" class="label">Name</label>
                        <input
                            id="name"
                            type="text"
                            v-model="form.name"
                            required
                            autofocus
                            autocomplete="name"
                            class="input"
                            :class="{ 'input-error': form.errors.name }"
                            placeholder="Enter your full name"
                        />
                        <p v-if="form.errors.name" class="error-message">
                            {{ form.errors.name }}
                        </p>
                    </div>

                    <!-- Email Input -->
                    <div class="input-group">
                        <label for="email" class="label">Email</label>
                        <input
                            id="email"
                            type="email"
                            v-model="form.email"
                            required
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
                                autocomplete="new-password"
                                class="input"
                                :class="{ 'input-error': form.errors.password }"
                                placeholder="Create a password"
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

                    <!-- Confirm Password Input -->
                    <div class="input-group">
                        <label for="password_confirmation" class="label">Confirm Password</label>
                        <div class="password-wrapper">
                            <input
                                id="password_confirmation"
                                :type="showPasswordConfirmation ? 'text' : 'password'"
                                v-model="form.password_confirmation"
                                required
                                autocomplete="new-password"
                                class="input"
                                :class="{ 'input-error': form.errors.password_confirmation }"
                                placeholder="Confirm your password"
                            />
                            <button
                                type="button"
                                @click="showPasswordConfirmation = !showPasswordConfirmation"
                                class="toggle-password"
                                tabindex="-1"
                            >
                                <svg v-if="!showPasswordConfirmation" class="eye-icon" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                                </svg>
                                <svg v-else class="eye-icon" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.88 9.88l-3.29-3.29m7.532 7.532l3.29 3.29M3 3l3.59 3.59m0 0A9.953 9.953 0 0112 5c4.478 0 8.268 2.943 9.543 7a10.025 10.025 0 01-4.132 5.411m0 0L21 21" />
                                </svg>
                            </button>
                        </div>
                        <p v-if="form.errors.password_confirmation" class="error-message">
                            {{ form.errors.password_confirmation }}
                        </p>
                    </div>

                    <!-- Submit Button -->
                    <button
                        type="submit"
                        class="submit-btn"
                        :class="{ 'submit-btn-loading': form.processing }"
                        :disabled="form.processing"
                    >
                        <span v-if="form.processing" class="loader"></span>
                        <span v-else>Create account</span>
                    </button>

                    <!-- Login Link -->
                    <div class="login-section">
                        <p class="login-text">
                            Already have an account?
                            <Link :href="route('login')" class="login-link">
                                Sign in
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

.register-page {
    font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    background: #fafafa;
    min-height: 100vh;
    color: #1a1a1a;
}

.register-container {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    padding: 2rem 1rem;
}

.register-box {
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

.login-section {
    text-align: center;
    margin-top: 0.5rem;
}

.login-text {
    font-size: 0.875rem;
    color: #6b7280;
}

.login-link {
    color: #1a1a1a;
    text-decoration: none;
    font-weight: 700;
    transition: all 0.2s ease;
    border-bottom: 1.5px solid transparent;
}

.login-link:hover {
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
    .register-box {
        padding: 2.5rem 2rem;
    }
    
    .title {
        font-size: 1.625rem;
    }
}

/* Mobile */
@media (max-width: 480px) {
    .register-box {
        padding: 2rem 1.5rem;
        border-radius: 12px;
    }
    
    .title {
        font-size: 1.5rem;
    }
    
    .subtitle {
        font-size: 0.875rem;
    }
}
</style>