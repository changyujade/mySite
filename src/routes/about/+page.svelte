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

<p>目前就讀美國芝加哥大學 University of Chicago 研究所Digital Studies of Language, Culture, and History。畢業於美國Colby College，主修Computer Science+Music (資訊及音樂跨領域) 以及 French and Francophone Studies （法文與法語區研究）。大三時有機會至丹麥哥本哈根DIS Program還有瑞士日內瓦University of Geneva 進行交換，而更開拓了我的國際觀，也更奠定了我對法語的興趣。回來以後還是持續精進我的法文程度、並在2025年底得到歐語架構最高等級C2的證書。



音樂和語言一直是我成長的一部份。所以大學一開始就選擇了在資訊和音樂的跨領域主修。學習期間也是持續學習並試著將我有興趣的領域做結合。在大學的Computer Science課程裡，我學習到不只Python和Java程式語言，還深入瞭解了Classes, linked list, Binary Search Trees, Hash Trees, Heaps, Queues 等Data Structure並自行寫出像是Dijkstra’s Algorithm的演算法。其次也學習到如何用科學化、系統化的方式來管理和分析資訊 (Data Management and Statistical Data Analysis), 同時運用Python的工具例如Matplotlib來視覺化(Visualise)資訊。大學三年級時更深化了我的機器學習(Machine Learning)的技術，開發了一個運用Transfer Learning & CNN技術的神經網路 (Neural Network) 來根據聲音來辨別(Classify)中國樂器的套件。2024年暑假，受教授的邀請成為他的研究助理，協助他用機器學習的套件在音樂程式設計軟體Max上創造了一個使用使用者的手勢來訓練以及生成動機變化 (music motifs)的音樂套件。

求學過程中，我持續上大學提供的法語課，也確定其實語言才是我最大的興趣。所以積極尋找能夠在法語區交換的機會。也因為想申請交換，而法語研究也因緣際會地成為了我的第二個主修。</p>

<l> </l>
<p>
  Currently studying Digital Studies of Language, Culture, and History at the University of Chicago. 
  I graduated from Colby College with a major in Computer Science + Music and French and Francophone Studies. 
  Music and languages ​​have always been an integral part of my growth. Therefore, I chose to major in an interdisciplinary field of information and music from the beginning of my university studies. Throughout my studies, I have continuously learned and tried to combine areas of interest with my learning. In my Computer Science courses, I learned not only Python and Java programming languages, but also gained in-depth understanding of data structures such as Classes, linked lists, Binary Search Trees, Hash Trees, Heaps, and Queues, and even wrote my own algorithms similar to Dijkstra's Algorithm. Secondly, I learned how to manage and analyze information (Data Management and Statistical Data Analysis) in a scientific and systematic way, while using Python tools such as Matplotlib to visualize the information. 
  
  In my third year of college, I further deepened my machine learning skills, developing a kit that uses transfer learning and CNN technologies to classify Chinese musical instruments based on sound. In the summer of 2024, at the professor's invitation, I became his research assistant, assisting him in creating a music program on the music programming software Max that uses user gestures to train and generate music motifs. Throughout my studies, I continued to take French classes offered by the university, solidifying my interest in languages. Therefore, I actively sought opportunities to study in French-speaking regions. Because of this exchange application, French studies unexpectedly became my second major.
During this timel, I had the opportunity to participate in exchange programs at the DIS Program in Copenhagen, Denmark, and the University of Geneva, Switzerland, which broadened my international perspective and solidified my interest in French. 
  Upon returning to the US, I continued to improve my French and obtained the highest level (C2) certificate in European Language Framework by the end of 2025. 
  </p>


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

  p {
    margin: 1rem 0;
    line-height: 1.6;
    color: #555;
  }
</style>
