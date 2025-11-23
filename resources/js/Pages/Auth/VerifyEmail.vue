<script setup>
import { computed } from 'vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

const props = defineProps({
    status: {
        type: String,
    },
});

const form = useForm({});

const submit = () => {
    form.post(route('verification.send'));
};

const verificationLinkSent = computed(() => props.status === 'verification-link-sent');
</script>

<template>
    <Head title="Email Verification - Drive.edu" />
    
    <div class="verify-page">
        <!-- Verification Container -->
        <div class="verify-container">
            <div class="verify-box">
                <!-- Icon -->
                <div class="icon-wrapper">
                    <svg class="icon" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                    </svg>
                </div>

                <!-- Header -->
                <div class="header">
                    <h1 class="title">Verify your email</h1>
                    <p class="subtitle">
                        Thanks for signing up! Before getting started, could you verify your email address by clicking on the link we just emailed to you? If you didn't receive the email, we will gladly send you another.
                    </p>
                </div>

                <!-- Success Message -->
                <div v-if="verificationLinkSent" class="success-message">
                    <svg class="check-icon" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                    </svg>
                    <p>A new verification link has been sent to the email address you provided during registration.</p>
                </div>

                <!-- Form -->
                <form @submit.prevent="submit" class="form">
                    <button
                        type="submit"
                        class="submit-btn"
                        :class="{ 'submit-btn-loading': form.processing }"
                        :disabled="form.processing"
                    >
                        <span v-if="form.processing" class="loader"></span>
                        <span v-else>Resend Verification Email</span>
                    </button>

                    <div class="logout-section">
                        <Link
                            :href="route('logout')"
                            method="post"
                            as="button"
                            class="logout-link"
                        >
                            Log out
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

.verify-page {
    font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    background: #fafafa;
    min-height: 100vh;
    color: #1a1a1a;
}

.verify-container {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    padding: 2rem 1rem;
}

.verify-box {
    width: 100%;
    max-width: 480px;
    background: #ffffff;
    padding: 3rem 2.5rem;
    border-radius: 16px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.02), 0 10px 30px rgba(0, 0, 0, 0.04);
    animation: fadeInUp 0.5s ease;
    text-align: center;
}

.icon-wrapper {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 80px;
    height: 80px;
    background: #f0fdf4;
    border-radius: 50%;
    margin-bottom: 1.5rem;
}

.icon {
    width: 40px;
    height: 40px;
    color: #10b981;
}

.header {
    margin-bottom: 2rem;
}

.title {
    font-size: 1.875rem;
    font-weight: 700;
    color: #1a1a1a;
    margin-bottom: 1rem;
    letter-spacing: -0.02em;
}

.subtitle {
    font-size: 0.9375rem;
    color: #6b7280;
    font-weight: 400;
    line-height: 1.6;
    text-align: center;
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
    text-align: left;
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
    gap: 1rem;
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

.btn-icon {
    width: 18px;
    height: 18px;
}

.loader {
    width: 18px;
    height: 18px;
    border: 2.5px solid rgba(255, 255, 255, 0.3);
    border-top-color: #ffffff;
    border-radius: 50%;
    animation: spin 0.7s linear infinite;
}

.logout-section {
    text-align: center;
    padding-top: 0.5rem;
}

.logout-link {
    color: #6b7280;
    text-decoration: none;
    font-size: 0.875rem;
    font-weight: 600;
    transition: all 0.2s ease;
    border-bottom: 1.5px solid transparent;
    background: none;
    border: none;
    cursor: pointer;
    padding: 0;
}

.logout-link:hover {
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
    .verify-box {
        padding: 2.5rem 2rem;
    }
    
    .title {
        font-size: 1.625rem;
    }
    
    .icon-wrapper {
        width: 70px;
        height: 70px;
    }
    
    .icon {
        width: 36px;
        height: 36px;
    }
}

/* Mobile */
@media (max-width: 480px) {
    .verify-box {
        padding: 2rem 1.5rem;
        border-radius: 12px;
    }
    
    .icon-wrapper {
        width: 64px;
        height: 64px;
    }
    
    .icon {
        width: 32px;
        height: 32px;
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