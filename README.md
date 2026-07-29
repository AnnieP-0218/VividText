<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>VividText - Dyslexia-Friendly Reading & Writing App for Students</title>
  <style>
    /* CSS RESET & DESIGN TOKENS */
    /* Custom Palette: #333333 (Dark Charcoal) & #FFDAB9 (Peach Puff) */
    :root {
      --bg-color: #faf8f5;
      --card-bg: #ffffff;
      --text-main: #333333;
      --text-muted: #555555;
      
      /* Primary Branding Colors */
      --color-dark: #333333;
      --color-peach: #FFDAB9;
      --color-peach-hover: #fcd2ab;
      --color-peach-light: #fff2e6;
      
      --border-color: #e5e5e5;
      --radius-lg: 16px;
      --radius-md: 10px;
      --font-stack: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    html {
      scroll-behavior: smooth;
    }

    body {
      background-color: var(--bg-color);
      color: var(--text-main);
      font-family: var(--font-stack);
      line-height: 1.65;
      font-size: 1.125rem; /* 18px base font size for improved legibility */
      letter-spacing: 0.01em;
      -webkit-font-smoothing: antialiased;
    }

    /* ACCESSIBILITY & LAYOUT HELPERS */
    .container {
      width: 100%;
      max-width: 960px;
      margin: 0 auto;
      padding: 0 1.25rem;
    }

    section {
      padding: 4rem 0;
      border-bottom: 1px solid rgba(0,0,0,0.05);
    }

    h1, h2, h3 {
      color: var(--text-main);
      line-height: 1.25;
      font-weight: 700;
      letter-spacing: -0.01em;
    }

    p {
      color: var(--text-muted);
      margin-top: 0.75rem;
    }

    strong {
      color: var(--text-main);
    }

    /* BUTTONS & CONTROLS */
    .btn {
      display: inline-block;
      background-color: var(--color-peach);
      color: var(--color-dark);
      font-size: 1.2rem;
      font-weight: 800;
      padding: 1.1rem 2rem;
      border-radius: var(--radius-md);
      text-decoration: none;
      text-align: center;
      transition: background-color 0.15s ease, transform 0.1s ease;
      border: 2px solid var(--color-dark);
      cursor: pointer;
      box-shadow: 0 4px 12px rgba(51, 51, 51, 0.15);
    }

    .btn:hover, .btn:focus {
      background-color: var(--color-peach-hover);
      transform: translateY(-2px);
      outline: none;
    }

    .btn-header {
      font-size: 1rem;
      padding: 0.6rem 1.2rem;
      box-shadow: none;
      min-height: 44px;
      display: inline-flex;
      align-items: center;
      justify-content: center;
    }

    .btn-large {
      width: 100%;
      max-width: 420px;
      padding: 1.25rem 2.5rem;
      font-size: 1.35rem;
      min-height: 58px; /* High-touch target size for mobile thumbs */
    }

    /* HEADER WITH TOP LEFT BRANDING & TOP RIGHT BUTTON */
    header {
      padding: 1rem 0;
      background: #ffffff;
      border-bottom: 2px solid var(--color-peach);
      position: sticky;
      top: 0;
      z-index: 100;
    }

    header .header-content {
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .logo-brand {
      display: inline-block;
      text-decoration: none;
    }

    .logo-text {
      font-size: 1.85rem;
      color: #383838;
      font-weight: 800;
      letter-spacing: -0.03em;
      line-height: 1;
    }

    /* SECTION 1: HERO */
    .hero {
      padding-top: 3rem;
      padding-bottom: 4rem;
      text-align: center;
    }

    .badge {
      display: inline-block;
      background-color: var(--color-peach);
      color: var(--color-dark);
      font-weight: 700;
      font-size: 0.95rem;
      padding: 0.4rem 1rem;
      border-radius: 50px;
      margin-bottom: 1.5rem;
      border: 1px solid var(--color-dark);
    }

    .hero h1 {
      font-size: 2.5rem;
      max-width: 800px;
      margin: 0 auto 1.25rem auto;
    }

    .hero-sub {
      font-size: 1.35rem;
      color: var(--text-main);
      font-weight: 500;
      max-width: 680px;
      margin: 0 auto 2rem auto;
    }

    /* Visual Prototype Graphic */
    .app-preview-box {
      background-color: var(--card-bg);
      border: 3px solid var(--color-dark);
      border-radius: var(--radius-lg);
      padding: 1.75rem;
      margin: 2.5rem auto 1rem auto;
      max-width: 720px;
      text-align: left;
      box-shadow: 0 10px 30px rgba(0,0,0,0.06);
    }

    .preview-header {
      display: flex;
      align-items: center;
      gap: 0.5rem;
      margin-bottom: 1.25rem;
      padding-bottom: 0.75rem;
      border-bottom: 2px solid var(--bg-color);
    }

    .dot {
      width: 12px;
      height: 12px;
      border-radius: 50%;
    }
    .dot-1 { background-color: #333333; }
    .dot-2 { background-color: #FFDAB9; }
    .dot-3 { background-color: #888888; }

    .preview-content {
      font-size: 1.2rem;
      line-height: 1.8;
      background: var(--color-peach-light);
      padding: 1.25rem;
      border-radius: var(--radius-md);
      border-left: 5px solid var(--color-dark);
    }

    .highlight-word {
      background-color: var(--color-peach);
      padding: 0.15rem 0.4rem;
      border-radius: 4px;
      font-weight: bold;
      color: var(--color-dark);
    }

    /* SECTION 2: THE PROBLEM */
    .problem-section {
      background-color: #ffffff;
    }

    .quote-card {
      background-color: var(--color-peach-light);
      border-left: 6px solid var(--color-dark);
      padding: 2rem;
      border-radius: 0 var(--radius-md) var(--radius-md) 0;
      margin-bottom: 2rem;
    }

    .quote-text {
      font-size: 1.5rem;
      font-weight: 700;
      color: var(--color-dark);
      font-style: italic;
      line-height: 1.4;
    }

    .cost-box {
      font-size: 1.25rem;
      background-color: #ffffff;
      border: 2px solid var(--color-dark);
      color: var(--color-dark);
      padding: 1.5rem;
      border-radius: var(--radius-md);
      margin-top: 1.5rem;
    }

    /* SECTION 3: HOW IT WORKS & PRICING */
    .section-title {
      font-size: 2rem;
      text-align: center;
      margin-bottom: 2.5rem;
    }

    .steps-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 1.5rem;
      margin-bottom: 4rem;
    }

    .step-card {
      background-color: var(--card-bg);
      border: 2px solid var(--color-dark);
      border-radius: var(--radius-md);
      padding: 1.75rem;
      position: relative;
    }

    .step-number {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      width: 40px;
      height: 40px;
      background-color: var(--color-dark);
      color: var(--color-peach);
      font-weight: 800;
      border-radius: 50%;
      margin-bottom: 1rem;
    }

    .step-card h3 {
      font-size: 1.25rem;
      margin-bottom: 0.5rem;
    }

    /* Pricing Table */
    .pricing-card {
      background-color: var(--card-bg);
      border: 3px solid var(--color-dark);
      border-radius: var(--radius-lg);
      padding: 2.5rem;
      max-width: 580px;
      margin: 0 auto;
      text-align: center;
      box-shadow: 0 12px 24px rgba(0,0,0,0.06);
    }

    .price-tag {
      font-size: 3.5rem;
      font-weight: 800;
      color: var(--color-dark);
      margin: 1rem 0 0.25rem 0;
    }

    .price-period {
      font-size: 1.1rem;
      color: var(--text-muted);
      margin-bottom: 1.5rem;
    }

    .features-list {
      text-align: left;
      list-style: none;
      margin: 1.5rem 0;
    }

    .features-list li {
      padding: 0.6rem 0;
      border-bottom: 1px solid var(--border-color);
      display: flex;
      align-items: center;
      gap: 0.75rem;
      font-size: 1.1rem;
    }

    .features-list li::before {
      content: "✓";
      color: var(--color-dark);
      font-weight: 900;
      font-size: 1.3rem;
    }

    .guarantee-box {
      margin-top: 1.75rem;
      padding: 1.25rem;
      background-color: var(--color-peach);
      border-radius: var(--radius-md);
      border: 2px solid var(--color-dark);
      text-align: left;
    }

    .guarantee-box strong {
      color: var(--color-dark);
      display: block;
      margin-bottom: 0.25rem;
    }

    .guarantee-box p {
      color: var(--color-dark);
      font-size: 1rem;
      margin-top: 0;
    }

    /* SECTION 5: OBJECTIONS & FAQS */
    .faq-grid {
      display: grid;
      gap: 1.5rem;
      max-width: 780px;
      margin: 0 auto;
    }

    .faq-item {
      background-color: var(--card-bg);
      border: 2px solid var(--color-dark);
      padding: 1.75rem;
      border-radius: var(--radius-md);
    }

    .faq-item h3 {
      font-size: 1.3rem;
      color: var(--color-dark);
      margin-bottom: 0.75rem;
    }

    .faq-item p {
      font-size: 1.1rem;
      color: var(--text-muted);
      margin-top: 0;
    }

    /* SECTION 6: EMBEDDED FORM SIGN-UP SECTION */
    .cta-section {
      text-align: center;
      background-color: #ffffff;
      padding: 5rem 1.25rem;
    }

    .cta-section h2 {
      font-size: 2.25rem;
      margin-bottom: 1rem;
    }

    .cta-section p {
      font-size: 1.25rem;
      margin-bottom: 2rem;
    }

    /* Form Container for Responsive Fitting */
    .form-container {
      width: 100%;
      max-width: 680px;
      margin: 2rem auto 0 auto;
      background: #ffffff;
      border: 3px solid var(--color-dark);
      border-radius: var(--radius-lg);
      padding: 0.5rem;
      box-shadow: 0 10px 25px rgba(0,0,0,0.05);
      overflow: hidden;
    }

    .form-container iframe {
      width: 100%;
      min-height: 750px;
      border: 0;
      display: block;
    }

    footer {
      text-align: center;
      padding: 2rem 0;
      background-color: var(--color-dark);
      color: var(--color-peach);
      font-size: 0.95rem;
    }

    /* RESPONSIVE MEDIA QUERIES */
    @media (max-width: 640px) {
      body {
        font-size: 1rem;
      }
      .logo-text {
        font-size: 1.4rem;
      }
      .btn-header {
        font-size: 0.85rem;
        padding: 0.45rem 0.75rem;
      }
      .hero {
        padding-top: 2rem;
      }
      .hero h1 {
        font-size: 1.85rem;
      }
      .hero-sub {
        font-size: 1.15rem;
      }
      .price-tag {
        font-size: 2.75rem;
      }
      .quote-text {
        font-size: 1.2rem;
      }
      .btn-large {
        width: 100%;
      }
      .form-container {
        padding: 0;
        border-radius: var(--radius-md);
      }
      .form-container iframe {
        min-height: 800px;
      }
    }
  </style>
</head>
<body>

  <!-- HEADER WITH "VividText" BRAND NAME ON TOP LEFT & BUTTON ON TOP RIGHT -->
  <header>
    <div class="container header-content">
      <a href="#" class="logo-brand" aria-label="VividText Homepage">
        <span class="logo-text">VividText</span>
      </a>
      <a href="#signup" class="btn btn-header">Get Started For Free</a>
    </div>
  </header>

  <main>
    <!-- SECTION 1: BIG HEADLINE & HOW IT WORKS ONE-LINER -->
    <section class="hero">
      <div class="container">
        <span class="badge">Designed Specifically for Dyslexia</span>
        <h1>VividText is an app that helps students with dyslexia actually enjoy learning.</h1>
        <p class="hero-sub">Read effortlessly and write on your own without stress or extra help.</p>

        <!-- VISUAL DEMO ILLUSTRATION -->
        <div class="app-preview-box" aria-label="App demonstration preview">
          <div class="preview-header">
            <span class="dot dot-1"></span>
            <span class="dot dot-2"></span>
            <span class="dot dot-3"></span>
            <span style="font-size: 0.85rem; color: var(--text-muted); margin-left: 0.5rem; font-weight: bold;">VividText Active Reader Demo</span>
          </div>
          <div class="preview-content">
            <p style="margin-top: 0;">
              Students read <span class="highlight-word">one clean focus line</span> at a time. Words skip visual clutter, guided by smart focus highlights.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- SECTION 2: THE PROBLEM IN CUSTOMER'S OWN WORDS -->
    <section class="problem-section">
      <div class="container">
        <h2 style="font-size: 1.75rem; margin-bottom: 1.5rem;">Why traditional reading tools fail:</h2>
        
        <div class="quote-card">
          <p class="quote-text">“I can read something I’ve written 10 times over and still miss the same problem.”</p>
        </div>

        <div class="cost-box">
          <strong>The exact moment it goes wrong:</strong>
          <p style="color: var(--text-muted); margin-top: 0.5rem;">
            It happens at 8:00 PM over homework. You know what you want to say, but letters jump around on the screen. You re-read the same paragraph five times, get exhausted, and hand in work that doesn't reflect how smart you actually are.
          </p>
        </div>
      </div>
    </section>

    <!-- SECTION 3: WHAT THEY GET & WHAT IT COSTS (STEPS + PRICING) -->
    <section>
      <div class="container">
        <h2 class="section-title">How VividText Works in 4 Steps</h2>
        
        <div class="steps-grid">
          <div class="step-card">
            <div class="step-number">1</div>
            <h3>Import Any Text</h3>
            <p>Paste your essay, book chapter, or homework sheet into VividText in one click.</p>
          </div>
          <div class="step-card">
            <div class="step-number">2</div>
            <h3>Read With Active Tools</h3>
            <p>Words are automatically formatted with custom spacing and line-highlighting to eliminate clutter.</p>
          </div>
          <div class="step-card">
            <div class="step-number">3</div>
            <h3>Type With Smart Prompts</h3>
            <p>Our smart typing engine catches repeated mistakes and suggests phonetic spelling fixes instantly.</p>
          </div>
          <div class="step-card">
            <div class="step-number">4</div>
            <h3>Finish Drafts Solo</h3>
            <p>Get step-by-step writing prompts so you can complete assignments without asking for help.</p>
          </div>
        </div>

        <!-- PRICING BOX -->
        <h2 class="section-title" style="margin-bottom: 1.5rem;">Simple, Honest Pricing</h2>
        <div class="pricing-card">
          <h3>VividText Unlimited</h3>
          <div class="price-tag">$7.99</div>
          <div class="price-period">per month • cancel anytime</div>

          <ul class="features-list">
            <li><strong>Free Tier:</strong> Basic vocabulary games & reading tools</li>
            <li><strong>Unlimited Tier:</strong> Active reading tools & visual guides</li>
            <li><strong>Smart Typing:</strong> Real-time dyslexia phonetic fixers</li>
            <li><strong>Step-by-Step Writing Support:</strong> Structured writing wizard</li>
          </ul>

          <div class="guarantee-box">
            <strong>100% Money-Back Guarantee:</strong>
            <p>Finish your first short writing draft in 3 days, or get 100% of your money back plus a free month. No questions asked.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- SECTION 4: PROOF (Omitted per instruction until real testimonials are ready) -->

    <!-- SECTION 5: REAL OBJECTIONS ANSWERED STRAIGHT -->
    <section>
      <div class="container">
        <h2 class="section-title">Frequently Asked Questions</h2>
        
        <div class="faq-grid">
          <div class="faq-item">
            <h3>1. "Will this actually work for me or my child?"</h3>
            <p>
              VividText wasn't built like standard spellcheckers. It was specifically built around how brains with dyslexia process written text—using line isolation, high visual distinction fonts, and phonetic writing prompts. Try it on your next short writing assignment for 3 days; if it doesn't immediately cut homework frustration, you pay nothing.
            </p>
          </div>

          <div class="faq-item">
            <h3>2. "Is $7.99/month worth it when there are free spellcheckers?"</h3>
            <p>
              Standard spellcheckers highlight errors *after* you get stuck. VividText actively guides your reading and writing *while* you type, preventing fatigue before it happens. Most families save hours of homework argument every single week.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- SECTION 6: EMBEDDED GOOGLE FORM SIGN-UP SECTION -->
    <section id="signup" class="cta-section">
      <div class="container">
        <h2>Ready to read and write with confidence?</h2>
        <p>Fill out the short form below to get started for free.</p>
        
        <!-- RESPONSIVE GOOGLE FORM EMBED CONTAINER -->
        <div class="form-container">
          <iframe src="https://docs.google.com/forms/d/e/1FAIpQLSfPwwAnQkdjNLcvKJACGx1KHY6ah31dl8wO-UfQqmgYnuWu9A/viewform?embedded=true" width="640" height="718" frameborder="0" marginheight="0" marginwidth="0">Loading…</iframe>
        </div>
        
        <p style="font-size: 0.95rem; margin-top: 1.5rem; color: var(--text-muted);">
          No long-term commitment. 3-day money-back guarantee.
        </p>
      </div>
    </section>
  </main>

  <footer>
    <div class="container">
      <p>&copy; VividText. Built for students with dyslexia.</p>
    </div>
  </footer>

  <script>
    console.log("VividText Landing Page loaded successfully.");
  </script>
</body>
</html>
