<template>
  <Section id="what-ive-done">
    <Abstract3 />

    <Heading>Other samples of my work</Heading>
    <p>
      I have mainly worked on internal tools, but I do have a few public views of some of my work linked inside the bubbles. This site was made with vue. 
    </p>

    <div ref="container" class="bubble-container">
      <div
        v-for="(bubble, index) in bubbles"
        :key="index"
        class="bubble"
        :style="bubbleStyle(bubble)"
        @mouseenter="hoverBubble(index)"
        @mouseleave="leaveBubble(index)"
        @click="goToLink(bubble.link)"
      >
        {{ bubble.text }}
      </div>
    </div>

    <p>
      I do have some old coding exercises available to view on both my
      <a href="https://github.com/HollyMaguire" target="_blank">Github</a>
      and
      <a href="https://codepen.io/hollyMaguire" target="_blank">CodePen</a>
    </p>
  </Section>
</template>

<script setup>
import { ref, onMounted } from "vue";

const container = ref(null);

const bubbles = ref([
  { text: "International Data", link: "https://www.eia.gov/international/data/world" },
  { text: "Today in Energy", link: "https://www.eia.gov/todayinenergy/" },
  { text: "FedMall", link: "https://www.fedmall.mil/index.html" },
  { text: "Short Term Energy Outlook", link: "https://www.eia.gov/outlooks/steo/" },
  { text: "Open Data", link: "https://www.eia.gov/opendata/" },
]);

let containerWidth = 0;
let containerHeight = 0;

const initBubbles = () => {
  containerWidth = container.value.clientWidth;
  containerHeight = container.value.clientHeight;

  bubbles.value.forEach((bubble) => {
    bubble.size = 110 + Math.random() * 60;
    bubble.x = Math.random() * (containerWidth - bubble.size);
    bubble.y = Math.random() * (containerHeight - bubble.size);
    bubble.vx = (Math.random() - 0.5) * 0.6;
    bubble.vy = (Math.random() - 0.5) * 0.6;
    bubble.scale = 1;
    bubble.opacity = 0.9;
  });
};

const hoverBubble = (i) => (bubbles.value[i].scale = 1.15);
const leaveBubble = (i) => (bubbles.value[i].scale = 1);

const goToLink = (link) => window.open(link, "_blank");

const handleCollisions = () => {
  for (let i = 0; i < bubbles.value.length; i++) {
    for (let j = i + 1; j < bubbles.value.length; j++) {
      const a = bubbles.value[i];
      const b = bubbles.value[j];

      const dx = b.x - a.x;
      const dy = b.y - a.y;
      const dist = Math.sqrt(dx * dx + dy * dy);
      const minDist = (a.size + b.size) / 2;

      if (dist < minDist) {
        const angle = Math.atan2(dy, dx);
        const overlap = minDist - dist;
        const pushX = Math.cos(angle) * overlap * 0.5;
        const pushY = Math.sin(angle) * overlap * 0.5;

        a.x -= pushX;
        a.y -= pushY;
        b.x += pushX;
        b.y += pushY;

        [a.vx, b.vx] = [b.vx, a.vx];
        [a.vy, b.vy] = [b.vy, a.vy];
      }
    }
  }
};

const animate = () => {
  bubbles.value.forEach((bubble) => {
    bubble.x += bubble.vx;
    bubble.y += bubble.vy;

    bubble.x = Math.max(0, Math.min(bubble.x, containerWidth - bubble.size));
    bubble.y = Math.max(0, Math.min(bubble.y, containerHeight - bubble.size));

    if (bubble.x <= 0 || bubble.x >= containerWidth - bubble.size) bubble.vx *= -1;
    if (bubble.y <= 0 || bubble.y >= containerHeight - bubble.size) bubble.vy *= -1;
  });

  handleCollisions();
  requestAnimationFrame(animate);
};

onMounted(() => {
  initBubbles();
  animate();
});

const bubbleStyle = (bubble) => ({
  width: `${bubble.size}px`,
  height: `${bubble.size}px`,
  top: `${bubble.y}px`,
  left: `${bubble.x}px`,
  position: "absolute",
  borderRadius: "50%",
  display: "flex",
  alignItems: "center",
  justifyContent: "center",
  textAlign: "center",
  cursor: "pointer",
  transform: `scale(${bubble.scale})`,
  transition: "transform 0.25s ease",
  color: "#00BFFF",
  fontWeight: "bold",
  fontSize: "14px",
  opacity: bubble.opacity,

  textShadow: `
    -1px -1px 0 #000,
     1px -1px 0 #000,
    -1px  1px 0 #000,
     1px  1px 0 #000,
     0px  0px 3px #000
  `,

  background: `
    radial-gradient(circle at 25% 25%, rgba(255,255,255,0.9), rgba(135,206,250,0.3) 50%, rgba(70,130,180,0.6)),
    conic-gradient(
      rgba(255,0,0,0.05),
      rgba(0,255,255,0.05),
      rgba(255,0,255,0.05),
      rgba(255,0,0,0.05)
    )
  `,
  boxShadow: "0 6px 30px rgba(0,0,0,0.25), inset 0 0 30px rgba(255,255,255,0.6)"
});
</script>

<style scoped>
#what-ive-done {
  min-height: 100vh;
  overflow: hidden;
}

.bubble-container {
  position: relative;
  width: 100%;
  height: 70vh;
  overflow: hidden;
}

p {
  text-align: center;
  margin-top: 2rem;
}
</style>
