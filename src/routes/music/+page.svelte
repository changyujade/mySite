<!-- <script>
  const profileUrl = "https://soundcloud.com/user-929081810?utm_source=clipboard&utm_medium=text&utm_campaign=social_sharing";
  const embedUrl = `https://w.soundcloud.com/player/?url=${encodeURIComponent(profileUrl)}&color=%23ff5500&auto_play=false&hide_related=true&show_comments=false&show_user=true&show_reposts=false&visual=true`; -->

<script>
  import { onMount } from "svelte";

  const profileUrl = "https://soundcloud.com/user-929081810?utm_source=clipboard&utm_medium=text&utm_campaign=social_sharing";
  const embedUrl = `https://w.soundcloud.com/player/?url=${encodeURIComponent(profileUrl)}&visual=true`;

  let playerEl;

  onMount(() => {
    const setup = () => {
      const widget = window.SC?.Widget?.(playerEl);
      if (!widget) return;

      widget.bind(window.SC.Widget.Events.READY, () => {
        console.log("SoundCloud widget ready");
      });

      // Example controls:
      // widget.play();
      // widget.pause();
      // widget.getCurrentSound((sound) => console.log(sound));
    };

    if (window.SC?.Widget) return setup();

    const script = document.createElement("script");
    script.src = "https://w.soundcloud.com/player/api.js";
    script.onload = setup;
    document.body.appendChild(script);
  });
</script>

<iframe
  bind:this={playerEl}
  width="100%"
  height="300"
  allow="autoplay"
  src={embedUrl}
  title="SoundCloud player"
></iframe>


<!-- // <iframe -->
<!-- //   width="100%"
//   height="300"
//   scrolling="no"
//   frameborder="no"
//   allow="autoplay"
//   src={embedUrl}
//   title="SoundCloud profile"
// ></iframe> -->
