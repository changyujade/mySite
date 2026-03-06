<!--
  +page.svelte — Your HOME PAGE (the root route: /)
  
  This is what visitors see first. It should introduce YOU
  and give people a reason to explore the rest of your site.

  KEY SVELTE 5 CONCEPTS USED HERE:
  - $state()  → creates a reactive variable (updates the page when it changes)
  - {variable} → displays a variable's value in HTML (like f-strings in Python)
  - onclick    → runs a function when something is clicked

  CUSTOMIZE: Replace ALL the placeholder text with your own content!
-->
<script>
  // ============================================
  // REACTIVE STATE — $state() makes variables "live"
  // ============================================
  // When these change, the HTML updates AUTOMATICALLY.
  // No document.getElementById needed!
  // Python comparison: imagine if changing a variable
  // instantly updated every print() that used it.

  let greeting = $state("About me:");
  let showBio = $state(false);

  // A regular variable (not reactive — fine for static data)
  const name = "Jade Chang";
  const tagline = "Student · Developer · Interdisciplinary Researcher";

  // ============================================
  // FUNCTIONS — same as JavaScript, but Svelte
  // re-renders automatically when $state changes
  // ============================================
  function toggleBio() {
    // This ONE LINE updates the variable AND the page.
    // In vanilla JS you'd also need:
    //   document.getElementById('bio').style.display = ...
    //   document.getElementById('btn').textContent = ...
    // Svelte handles all of that for you.
    showBio = !showBio;
  }
</script>

<section class="hero">
  <!-- {variable} inserts the value — like Python's f"{variable}" -->
  <h1>{greeting}</h1>
  <p class="name">{name}</p>
  <p class="tagline">{tagline}</p>

  <!--
    BUTTON with onclick
    When clicked, toggleBio() runs → showBio changes →
    the {#if} block below updates automatically
  -->
</section>

<section class="hero">
  <p>Welcome to my personal website! I'm excited to share my projects and experiences with you. Here is a more detailed version of my background and interests.</p>
</section>


<section class="quick-links">
  <h2>Explore</h2>
  <div class="card-row">
    <!--
      These are simple "cards" linking to your other pages.
      Each one is just an <a> tag styled as a box.
      Add more cards as you add more pages to your site!
    -->
    <a href="/about" class="card">
      <h3>About Me</h3>
      <p>My background, interests, and goals.</p>
    </a>
  </div>
</section>

<style>
  /* ============================
     HOME PAGE STYLES
     
     All styles here are SCOPED to this page only.
     They won't affect other pages. This is a Svelte
     feature — no class name collisions!
     ============================ */

  .hero {
    text-align: center;
    padding: 3rem 0 2rem;
  }

  .hero h1 {
    font-size: 2.2rem;
    margin-bottom: 0.5rem;
  }

  .name {
    font-size: 1.4rem;
    font-weight: bold;
    margin: 0.25rem 0;
  }

  .tagline {
    color: #666;
    font-style: italic;
    margin-bottom: 1.5rem;
  }

  button {
    background-color: #8b0000;
    color: white;
    border: none;
    padding: 0.6rem 1.5rem;
    font-size: 1rem;
    border-radius: 4px;
    cursor: pointer;
    font-family: inherit;
  }

  button:hover {
    background-color: #6b0000;
  }

  /* Bio section — appears when showBio is true */
  .bio-section {
    background-color: #f5f0eb;
    padding: 1.5rem 2rem;
    border-radius: 6px;
    margin: 1.5rem 0;
    border-left: 4px solid #8b0000;
  }

  .bio-section h2 {
    margin-top: 0;
  }

  /* Card links */
  .quick-links {
    margin-top: 2.5rem;
  }

  .card-row {
    display: flex;
    gap: 1.5rem;
    flex-wrap: wrap;
  }

  .card {
    flex: 1;
    min-width: 200px;
    background: white;
    border: 1px solid #ddd;
    border-radius: 6px;
    padding: 1.5rem;
    text-decoration: none;
    color: inherit;
    transition: box-shadow 0.2s;
  }

  .card:hover {
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.12);
    text-decoration: none;
  }

  .card h3 {
    margin: 0 0 0.5rem;
    color: #8b0000;
  }

  .card p {
    margin: 0;
    color: #555;
    font-size: 0.95rem;
  }
</style>
