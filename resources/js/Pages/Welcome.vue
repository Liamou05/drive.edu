<script setup>
import { Head, Link } from '@inertiajs/vue3';

defineProps({
    canLogin: {
        type: Boolean,
    },
    canRegister: {
        type: Boolean,
    },
    laravelVersion: {
        type: String,
        required: true,
    },
    phpVersion: {
        type: String,
        required: true,
    },
});
</script>

<template>
    <Head title="Drive.edu - Your Journey, Your Pace, Your Success" />

    <div class="page-wrapper">
        <!-- Navigation -->
        <nav>
            <Link href="/" class="logo">
                Drive<span class="logo-dot">.</span>edu
            </Link>
            <div v-if="canLogin" class="nav-links">
                <Link 
                    v-if="$page.props.auth.user"
                    :href="route('dashboard')"
                    class="register-btn"
                >
                    Dashboard
                </Link>
                <template v-else>
                    <Link :href="route('login')" class="login-btn">Log in</Link>
                    <Link v-if="canRegister" :href="route('register')" class="register-btn">Register</Link>
                </template>
            </div>
        </nav>

        <!-- Main Content -->
        <div class="container">
            <div class="content">
                <h1 class="hero-title">Store, Share, and Manage Your Files with Ease</h1>
                <p class="tagline">
                    Secure cloud storage designed for everyone. Upload, organize, and access your files from anywhere with Drive.edu – your trusted file management solution.
                </p>
                <Link 
                    :href="canRegister ? route('register') : route('login')" 
                    class="cta-button"
                >
                    Get Started for Free
                </Link>
            </div>

            <div class="visual-section">
                <div class="shape shape-1"></div>
                <div class="shape shape-2"></div>
                <div class="shape shape-3"></div>
                
                <div class="floating-card card-1">
                    <div class="card-row">
                        <span class="card-label">Storage Used</span>
                        <span class="card-value">12.4 GB / 50 GB</span>
                        <div class="status-badge"></div>
                    </div>
                    <div class="card-row">
                        <span class="card-label">Total Files</span>
                        <span class="card-value">1,247 Files</span>
                        <div class="status-badge"></div>
                    </div>
                    <div class="card-row">
                        <span class="card-label">Shared</span>
                        <span class="card-value">23 Items</span>
                        <div class="status-badge"></div>
                    </div>
                </div>

                <div class="floating-card card-2">
                    <div class="card-row">
                        <span class="card-label">Recent Upload</span>
                        <span class="card-value">Project_Final.pdf</span>
                        <div class="status-badge"></div>
                    </div>
                    <div class="card-row">
                        <span class="card-label">Uploaded</span>
                        <span class="card-value">2 minutes ago</span>
                        <div class="status-badge"></div>
                    </div>
                </div>
                
                <div class="floating-card card-3">
                    <div class="card-row">
                        <span class="card-label">Available Space</span>
                        <span class="card-value">37.6 GB</span>
                        <div class="status-badge"></div>
                    </div>
                    <div class="card-row">
                        <span class="card-label">Last Backup</span>
                        <span class="card-value">Today, 10:30 AM</span>
                        <div class="status-badge"></div>
                    </div>
                </div>
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

.page-wrapper {
    font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    background: #ffffff;
    min-height: 100vh;
    overflow-x: hidden;
    color: #1a1a1a;
}

nav {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    padding: 2rem 3rem;
    z-index: 100;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #ffffff;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
}

.logo {
    font-size: 1.5rem;
    font-weight: 700;
    color: #1a1a1a;
    text-decoration: none;
    letter-spacing: -0.02em;
}

.logo-dot {
    color: #3b82f6;
}

.nav-links {
    display: flex;
    gap: 1rem;
}

.nav-links a {
    text-decoration: none;
    font-size: 0.95rem;
    font-weight: 500;
    transition: all 0.3s ease;
    padding: 0.7rem 1.8rem;
    border-radius: 8px;
}

.login-btn {
    color: #1a1a1a;
    border: 1px solid #e5e7eb;
}

.login-btn:hover {
    background: #f9fafb;
    border-color: #d1d5db;
}

.register-btn {
    color: #ffffff;
    background: #1a1a1a;
}

.register-btn:hover {
    background: #374151;
    transform: translateY(-2px);
}

.container {
    display: grid;
    grid-template-columns: 1fr 1.3fr;
    align-items: center;
    width: 100%;
    max-width: 1600px;
    margin: 0 auto;
    height: 100vh;
    padding: 0 5rem;
    gap: 4rem;
}

.content {
    max-width: 700px;
    padding-right: 2rem;
}

.hero-title {
    font-size: 4.5rem;
    font-weight: 800;
    color: #1a1a1a;
    margin-bottom: 2.5rem;
    letter-spacing: -0.03em;
    line-height: 1.1;
    animation: fadeInUp 0.8s ease;
}

.tagline {
    font-size: 1.25rem;
    color: #6b7280;
    font-weight: 400;
    animation: fadeInUp 0.8s ease 0.2s backwards;
    line-height: 1.7;
    margin-bottom: 3.5rem;
}

.cta-button {
    display: inline-block;
    padding: 1rem 2.5rem;
    background: #1a1a1a;
    color: #ffffff;
    text-decoration: none;
    border-radius: 8px;
    font-weight: 600;
    font-size: 1rem;
    transition: all 0.3s ease;
    animation: fadeInUp 0.8s ease 0.4s backwards;
}

.cta-button:hover {
    background: #374151;
    transform: translateY(-3px);
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
}

.visual-section {
    position: relative;
    height: 600px;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    padding-left: 2rem;
}

.floating-card {
    background: #ffffff;
    border-radius: 16px;
    padding: 2rem;
    box-shadow: 0 20px 50px rgba(0, 0, 0, 0.08);
    position: absolute;
    animation: floatCard 6s infinite ease-in-out;
    border: 1px solid rgba(0, 0, 0, 0.03);
}

.card-1 {
    width: 400px;
    top: 50px;
    right: 20px;
    animation-delay: 0s;
}

.card-2 {
    width: 350px;
    bottom: 100px;
    left: 40px;
    animation-delay: 2s;
}

.card-3 {
    width: 320px;
    top: 200px;
    left: 100px;
    animation-delay: 4s;
}

.card-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 0;
    border-bottom: 1px solid #f3f4f6;
}

.card-row:last-child {
    border-bottom: none;
}

.card-label {
    font-size: 0.9rem;
    color: #6b7280;
    font-weight: 500;
}

.card-value {
    font-size: 0.9rem;
    color: #1a1a1a;
    font-weight: 600;
}

.status-badge {
    width: 24px;
    height: 24px;
    background: #10b981;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
}

.status-badge::after {
    content: '✓';
    color: white;
    font-size: 12px;
    font-weight: bold;
}

.shape {
    position: absolute;
    opacity: 0.6;
    animation: rotate 20s linear infinite;
}

.shape-1 {
    width: 100px;
    height: 100px;
    background: linear-gradient(135deg, #60a5fa 0%, #3b82f6 100%);
    border-radius: 30% 70% 70% 30% / 30% 30% 70% 70%;
    top: 100px;
    left: 100px;
    animation-delay: 0s;
}

.shape-2 {
    width: 80px;
    height: 80px;
    background: linear-gradient(135deg, #34d399 0%, #10b981 100%);
    border-radius: 70% 30% 30% 70% / 70% 70% 30% 30%;
    bottom: 150px;
    right: 100px;
    animation-delay: 5s;
}

.shape-3 {
    width: 60px;
    height: 60px;
    background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
    border-radius: 50% 50% 20% 80% / 25% 80% 20% 75%;
    top: 300px;
    right: 200px;
    animation-delay: 10s;
}

@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(40px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

@keyframes floatCard {
    0%, 100% {
        transform: translateY(0) rotate(0deg);
    }
    50% {
        transform: translateY(-20px) rotate(2deg);
    }
}

@keyframes rotate {
    0% {
        transform: rotate(0deg);
        border-radius: 30% 70% 70% 30% / 30% 30% 70% 70%;
    }
    50% {
        transform: rotate(180deg);
        border-radius: 70% 30% 30% 70% / 70% 70% 30% 30%;
    }
    100% {
        transform: rotate(360deg);
        border-radius: 30% 70% 70% 30% / 30% 30% 70% 70%;
    }
}

/* Ultra-wide screens (2560px+) */
@media (min-width: 2560px) {
    .container {
        max-width: 2200px;
        padding: 0 12rem;
        gap: 12rem;
    }
    
    .content {
        max-width: 900px;
    }
    
    .hero-title {
        font-size: 6rem;
    }
    
    .tagline {
        font-size: 1.5rem;
    }
    
    .visual-section {
        height: 800px;
    }
    
    .card-1 {
        width: 500px;
        right: 100px;
    }
    
    .card-2 {
        width: 450px;
        left: 100px;
    }
    
    .card-3 {
        width: 400px;
        left: 200px;
    }
    
    .shape-1 {
        width: 120px;
        height: 120px;
    }
    
    .shape-2 {
        width: 100px;
        height: 100px;
    }
    
    .shape-3 {
        width: 80px;
        height: 80px;
    }
}

/* Large Desktop (1920px - 2559px) */
@media (min-width: 1920px) and (max-width: 2559px) {
    .container {
        max-width: 1800px;
        padding: 0 8rem;
        gap: 10rem;
    }
    
    .content {
        max-width: 750px;
    }
    
    .hero-title {
        font-size: 5rem;
    }
    
    .visual-section {
        height: 700px;
    }
    
    .card-1 {
        width: 450px;
    }
    
    .card-2 {
        width: 400px;
    }
    
    .card-3 {
        width: 380px;
    }
}

/* Standard Desktop (1440px - 1919px) */
@media (min-width: 1440px) and (max-width: 1919px) {
    .container {
        padding: 0 5rem;
        gap: 8rem;
    }
    
    .hero-title {
        font-size: 4.5rem;
    }
}

/* Medium Desktop/Laptop (1280px - 1439px) */
@media (min-width: 1280px) and (max-width: 1439px) {
    .container {
        padding: 0 4rem;
        gap: 6rem;
    }
    
    .content {
        max-width: 650px;
    }
    
    .hero-title {
        font-size: 4rem;
    }
    
    .tagline {
        font-size: 1.2rem;
    }
    
    .visual-section {
        height: 550px;
    }
    
    .card-1 {
        width: 380px;
        right: 20px;
    }
    
    .card-2 {
        width: 330px;
    }
    
    .card-3 {
        width: 300px;
        left: 50px;
    }
}

/* Small Laptop (1024px - 1279px) */
@media (min-width: 1024px) and (max-width: 1279px) {
    nav {
        padding: 1.5rem 2.5rem;
    }
    
    .container {
        padding: 0 3rem;
        gap: 3rem;
    }
    
    .content {
        max-width: 500px;
        padding-right: 1rem;
    }
    
    .hero-title {
        font-size: 3.5rem;
        margin-bottom: 2rem;
    }
    
    .tagline {
        font-size: 1.1rem;
        margin-bottom: 2.5rem;
    }
    
    .visual-section {
        height: 500px;
        padding-left: 1rem;
    }
    
    .card-1 {
        width: 340px;
        right: 10px;
        top: 30px;
    }
    
    .card-2 {
        width: 300px;
        bottom: 80px;
        left: -20px;
    }
    
    .card-3 {
        display: none;
    }
    
    .shape-1 {
        width: 80px;
        height: 80px;
        left: 50px;
    }
    
    .shape-2 {
        width: 60px;
        height: 60px;
        right: 50px;
    }
    
    .shape-3 {
        display: none;
    }
}

/* Tablet Landscape (900px - 1023px) */
@media (min-width: 900px) and (max-width: 1023px) {
    nav {
        padding: 1.5rem 2rem;
    }
    
    .container {
        grid-template-columns: 1fr;
        padding: 0 2.5rem;
        gap: 4rem;
    }
    
    .content {
        text-align: center;
        max-width: 100%;
        padding-right: 0;
    }
    
    .hero-title {
        font-size: 3.5rem;
    }
    
    .tagline {
        font-size: 1.15rem;
        max-width: 600px;
        margin-left: auto;
        margin-right: auto;
    }
    
    .cta-button {
        margin-top: 1rem;
    }
    
    .visual-section {
        height: 450px;
        margin-top: 2rem;
        padding-left: 0;
    }
    
    .card-1 {
        width: 350px;
        right: 80px;
        top: 20px;
    }
    
    .card-2 {
        width: 320px;
        bottom: 50px;
        left: 80px;
    }
    
    .card-3 {
        display: none;
    }
    
    .shape-3 {
        display: none;
    }
}

/* Tablet Portrait (768px - 899px) */
@media (min-width: 768px) and (max-width: 899px) {
    nav {
        padding: 1.5rem 2rem;
    }
    
    .logo {
        font-size: 1.3rem;
    }
    
    .container {
        grid-template-columns: 1fr;
        padding: 0 2rem;
        gap: 3rem;
    }
    
    .content {
        text-align: center;
        padding-right: 0;
    }
    
    .hero-title {
        font-size: 3rem;
    }
    
    .tagline {
        font-size: 1.1rem;
    }
    
    .visual-section {
        height: 400px;
        padding-left: 0;
    }
    
    .card-1 {
        width: 300px;
        right: 50px;
    }
    
    .card-2 {
        width: 280px;
        left: 50px;
        bottom: 60px;
    }
    
    .card-3 {
        display: none;
    }
    
    .shape-1, .shape-2 {
        width: 60px;
        height: 60px;
    }
    
    .shape-3 {
        display: none;
    }
}

/* Mobile Large (640px - 767px) */
@media (min-width: 640px) and (max-width: 767px) {
    nav {
        padding: 1.2rem 1.5rem;
    }
    
    .logo {
        font-size: 1.2rem;
    }
    
    .nav-links a {
        font-size: 0.85rem;
        padding: 0.6rem 1.2rem;
    }
    
    .container {
        grid-template-columns: 1fr;
        padding: 0 1.5rem;
        padding-top: 5rem;
        gap: 2rem;
    }
    
    .content {
        text-align: center;
        padding-right: 0;
    }
    
    .hero-title {
        font-size: 2.5rem;
    }
    
    .tagline {
        font-size: 1rem;
    }
    
    .visual-section {
        height: 350px;
        margin-top: 1rem;
        padding-left: 0;
    }
    
    .card-1, .card-2 {
        width: 260px;
        padding: 1.5rem;
    }
    
    .card-1 {
        top: 10px;
        right: 20px;
    }
    
    .card-2 {
        bottom: 30px;
        left: 20px;
    }
    
    .card-3 {
        display: none;
    }
    
    .card-label, .card-value {
        font-size: 0.85rem;
    }
    
    .shape-1, .shape-2, .shape-3 {
        display: none;
    }
}

/* Mobile Medium (480px - 639px) */
@media (min-width: 480px) and (max-width: 639px) {
    nav {
        padding: 1rem 1.2rem;
        flex-wrap: wrap;
        gap: 1rem;
    }
    
    .logo {
        font-size: 1.1rem;
    }
    
    .nav-links {
        gap: 0.5rem;
    }
    
    .nav-links a {
        font-size: 0.8rem;
        padding: 0.5rem 1rem;
    }
    
    .container {
        padding: 0 1.5rem;
        padding-top: 6rem;
        gap: 2rem;
    }
    
    .content {
        padding-right: 0;
    }
    
    .hero-title {
        font-size: 2.2rem;
    }
    
    .tagline {
        font-size: 0.95rem;
        margin-bottom: 2rem;
    }
    
    .cta-button {
        padding: 0.9rem 2rem;
        font-size: 0.95rem;
    }
    
    .visual-section {
        height: 300px;
        padding-left: 0;
    }
    
    .card-1 {
        width: 240px;
        top: 0;
        right: 10px;
    }
    
    .card-2 {
        width: 220px;
        bottom: 0;
        left: 10px;
    }
    
    .card-3 {
        display: none;
    }
    
    .card-row {
        padding: 0.8rem 0;
    }
    
    .shape-1, .shape-2, .shape-3 {
        display: none;
    }
}

/* Mobile Small (below 480px) */
@media (max-width: 479px) {
    nav {
        padding: 1rem;
        flex-direction: column;
        gap: 1rem;
        align-items: stretch;
    }
    
    .logo {
        font-size: 1.1rem;
        text-align: center;
    }
    
    .nav-links {
        justify-content: center;
        gap: 0.5rem;
    }
    
    .nav-links a {
        font-size: 0.75rem;
        padding: 0.5rem 1rem;
        flex: 1;
        text-align: center;
    }
    
    .container {
        padding: 0 1rem;
        padding-top: 7rem;
        gap: 2rem;
    }
    
    .content {
        padding-right: 0;
    }
    
    .hero-title {
        font-size: 1.8rem;
        margin-bottom: 1rem;
    }
    
    .tagline {
        font-size: 0.9rem;
        margin-bottom: 1.5rem;
    }
    
    .cta-button {
        padding: 0.8rem 1.5rem;
        font-size: 0.9rem;
        width: 100%;
        text-align: center;
    }
    
    .visual-section {
        height: 280px;
        margin-top: 1.5rem;
        padding-left: 0;
    }
    
    .floating-card {
        padding: 1.2rem;
    }
    
    .card-1 {
        width: 200px;
        top: -10px;
        right: -5px;
    }
    
    .card-2 {
        width: 190px;
        bottom: -10px;
        left: -5px;
    }
    
    .card-3 {
        display: none;
    }
    
    .card-row {
        padding: 0.6rem 0;
        flex-direction: column;
        align-items: flex-start;
        gap: 0.3rem;
    }
    
    .status-badge {
        width: 20px;
        height: 20px;
        position: absolute;
        right: 0;
        top: 50%;
        transform: translateY(-50%);
    }
    
    .card-label, .card-value {
        font-size: 0.75rem;
    }
    
    .shape-1, .shape-2, .shape-3 {
        display: none;
    }
}
</style>