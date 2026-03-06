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

  let projects = $state("My Projects:");
  let showBio = $state(false);
  const spotifyProfileUrl = "https://open.spotify.com/user/YOUR_SPOTIFY_USER_ID";

  
  const profileUrl = "https://soundcloud.com/user-929081810?utm_source=clipboard&utm_medium=text&utm_campaign=social_sharing";
  const embedUrl = `https://w.soundcloud.com/player/?url=${encodeURIComponent(profileUrl)}&visual=true`;

  // A regular variable (not reactive — fine for static data)


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
  <h1>{projects}</h1>

  <!--
    BUTTON with onclick
    When clicked, toggleBio() runs → showBio changes →
    the {#if} block below updates automatically
  -->
</section>





<section class="quick-links">
  <h2>Explore</h2>
  <div class="card-row">
    <!--
      These are simple "cards" linking to your other pages.
      Each one is just an <a> tag styled as a box.
      Add more cards as you add more pages to your site!
    -->
    <a href="/about" class="card card-social">
      <h3>Project on social media analysis</h3>
      <p>Currently in progress. Analysing misogyny in social media content, in particular the platform "threads"</p>
    </a>

  
    <div class="card">
      <h3>My SoundCloud Track</h3>
      <p>These are the original music that I've made in the past. Listen to it on SoundCloud!</p>
      <iframe
        width="100%"
        height="300"
        allow="autoplay"
        src={embedUrl}
        title="SoundCloud player"
      ></iframe>
    </div>

    <a href="https://github.com/changyujade/jazz-analyzer" class="card card-jazz">
      <h3>jazz-analyzer</h3>
      <p>This is my project on jazz analysis. For my senior-year capstone project, I built a jazz analyzer website. The goal of this project was to help beginners learn jazz theory. I parsed chord data from plain text files into Python and normalized songs in different keys into Roman numeral notation (I–VII), allowing the program to analyze chord functions automatically. This made it possible to identify different chord patterns. When users move their cursor over a detected chord progression, they can learn about the function of each chord in the song and receive suggestions for appropriate scales to play over the progression. I invited music majors and professors to test the program and used their feedback to improve both the system and its usability. This project demonstrates my ability to use technology to address the needs and challenges faced by beginners in jazz music. Click to goto the github repository </p>
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
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem;
  }

  .card {
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
    color: #f8a484;
  }

  .card p {
    margin: 0;
    color: #555;
    font-size: 0.95rem;
  }

  @media (min-width: 900px) {
    .card-social {
      grid-column: 1;
      grid-row: 1;
    }

    .card-spotify {
      grid-column: 1;
      grid-row: 2;
    }

    .card-jazz {
      grid-column: 2;
      grid-row: 1 / span 2;
    }
  }
</style>

