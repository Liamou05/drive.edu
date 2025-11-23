<script setup>
import { Head, Link, useForm } from '@inertiajs/vue3';

defineProps({
    status: {
        type: String,
    },
});

const form = useForm({
    email: '',
});

const submit = () => {
    form.post(route('password.email'));
};
</script>

<template>
    <Head title="Forgot Password - Drive.edu" />
    
    <div class="forgot-page">
        <!-- Forgot Container -->
        <div class="forgot-container">
            <div class="forgot-box">
                <!-- Header -->
                <div class="header">
                    <h1 class="title">Forgot your password?</h1>
                    <p class="subtitle">
                        No problem. Just let us know your email address and we will email you a password reset link that will allow you to choose a new one.
                    </p>
                </div>

                <!-- Success Message -->
                <div v-if="status" class="success-message">
                    <svg class="check-icon" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                    </svg>
                    <p>{{ status }}</p>
                </div>

                <!-- Form -->
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

                    <!-- Submit Button -->
                    <button
                        type="submit"
                        class="submit-btn"
                        :class="{ 'submit-btn-loading': form.processing }"
                        :disabled="form.processing"
                    >
                        <span v-if="form.processing" class="loader"></span>
                        <span v-else>Email Password Reset Link</span>
                    </button>

                    <!-- Back to Login Link -->
                    <div class="login-section">
                        <Link :href="route('login')" class="login-link">
                            ← Back to sign in
                        </Link>
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

.forgot-page {
    font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    background: #fafafa;
    min-height: 100vh;
    color: #1a1a1a;
}

.forgot-container {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    padding: 2rem 1rem;
}

.forgot-box {
    width: 100%;
    max-width: 440px;
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
    margin-bottom: 0.75rem;
    letter-spacing: -0.02em;
}

.subtitle {
    font-size: 0.9375rem;
    color: #6b7280;
    font-weight: 400;
    line-height: 1.6;
}

.success-message {
    display: flex;
    align-items: flex-start;
    gap: 0.75rem;
    background: #d1fae5;
    border-left: 4px solid #10b981;
    color: #065f46;
    padding: 1rem 1.25rem;
    border-radius: 8px;
    font-size: 0.875rem;
    margin-bottom: 1.5rem;
    line-height: 1.5;
}

.check-icon {
    width: 20px;
    height: 20px;
    color: #10b981;
    flex-shrink: 0;
    margin-top: 2px;
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

.login-link {
    color: #6b7280;
    text-decoration: none;
    font-size: 0.875rem;
    font-weight: 600;
    transition: all 0.2s ease;
    border-bottom: 1.5px solid transparent;
    display: inline-block;
}

.login-link:hover {
    color: #1a1a1a;
    border-bottom-color: #1a1a1a;
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
    .forgot-box {
        padding: 2.5rem 2rem;
    }
    
    .title {
        font-size: 1.625rem;
    }
}

/* Mobile */
@media (max-width: 480px) {
    .forgot-box {
        padding: 2rem 1.5rem;
        border-radius: 12px;
    }
    
    .title {
        font-size: 1.5rem;
    }
    
    .subtitle {
        font-size: 0.875rem;
    }
    
    .success-message {
        font-size: 0.8125rem;
    }
}
</style>