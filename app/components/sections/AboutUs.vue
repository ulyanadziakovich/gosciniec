<template>
  <div class="about-us-wrapper">
    <div class="about-us-content">

      <!-- Główny nagłówek -->
      <div class="hero-heading">
        <p class="subtitle">Poznajcie nas</p>
        <h1 class="main-title">Mirek i Kasia</h1>
      </div>

      <div class="grid-container">
        <!-- Sekcja tekstowa -->
        <div ref="textSection" class="text-section" :class="{ 'visible': textVisible }">
          <div class="text-card">
            <p class="paragraph">
              Nasz gościniec to miejsce stworzone z <strong>pasją i sercem</strong> przez rodzinę – Mirka i Kasię.
              Położony przy malowniczym <strong>szlaku Małego Króla</strong>, otoczony spokojnym lasem i siecią urokliwych ścieżek spacerowych,
              oferuje prawdziwy odpoczynek z dala od miejskiego zgiełku.
            </p>
            <p class="paragraph">
              To więcej niż nocleg – to <strong>dom</strong>, w którym goście stają się częścią naszej historii.
              Z miłością dbamy o każdy detal, aby Państwa pobyt był niezapomniany. Nasze domowe specjały – aromatyczne
              <strong>syropy</strong> i świeżo wyciskane <strong>soki</strong> z lokalnych owoców – to smak natury,
              który zabierzecie ze sobą w sercu.
            </p>
            <p class="paragraph">
              Zapraszamy do nas – do miejsca, gdzie <em>czas zwalnia</em>, las szumi tuż za oknem,
              a poranek wita śpiewem ptaków. Tutaj odnajdziecie spokój, ciepło i autentyczność górskiej gościnności.
            </p>

            <div class="signature">
              <p class="greeting">Serdecznie zapraszamy!</p>
              <p class="names">
                <span class="heart">Heart</span> Mirek i Kasia
              </p>
            </div>
          </div>
        </div>

        <!-- Sekcja ze zdjęciem -->
        <div ref="imageSection" class="image-section" :class="{ 'visible': imageVisible }">
          <div class="image-container">
            <img
              src="https://www.dropbox.com/scl/fi/enrk7nxf5a9z33s7587oy/MirekiKasiabialyfon.png?rlkey=9fip7cpyt2457fg07xs3nqgb1&raw=1"
              alt="Mirek i Kasia - wlasciciele Goscinca pod Malym Krollem"
              class="profile-image"
            />
            <div class="image-border"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const textVisible = ref(false)
const imageVisible = ref(false)
const textSection = ref<HTMLElement | null>(null)
const imageSection = ref<HTMLElement | null>(null)

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          if (entry.target === textSection.value) textVisible.value = true
          if (entry.target === imageSection.value) imageVisible.value = true
        }
      })
    },
    { threshold: 0.2, rootMargin: '0px 0px -10% 0px' }
  )

  if (textSection.value) observer.observe(textSection.value)
  if (imageSection.value) observer.observe(imageSection.value)
})
</script>

<style scoped>
.about-us-wrapper {
  background: #ffffff;
  min-height: 100vh;
  padding: 8rem 2rem 12rem;
  font-family: 'Poppins', system-ui, sans-serif;
}

.about-us-content {
  max-width: 1400px;
  margin: 0 auto;
  text-align: center;
}

.hero-heading {
  margin-bottom: 7rem;
}

.subtitle {
  font-size: 1.1rem;
  font-weight: 400;
  letter-spacing: 4px;
  text-transform: uppercase;
  color: #7c704c;
  margin-bottom: 1rem;
}

.main-title {
  font-family: 'Poppins', sans-serif;
  font-size: 4.8rem;
  font-weight: 600;
  color: #2c3e50;
  margin: 0;
  letter-spacing: 0.5px;
}

@media (max-width: 992px) {
  .main-title { font-size: 3.8rem; }
  .about-us-wrapper { padding: 6rem 1.5rem 10rem; }
}
@media (max-width: 640px) {
  .main-title { font-size: 2.9rem; }
  .hero-heading { margin-bottom: 5rem; }
}

.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 7rem;
  align-items: center;
}

@media (max-width: 992px) {
  .grid-container {
    grid-template-columns: 1fr;
    gap: 5rem;
  }
  .image-section { order: -1; }
}

.text-section {
  opacity: 0;
  transform: translateY(50px);
  transition: all 1.3s cubic-bezier(0.25, 0.8, 0.25, 1);
}

.text-section.visible {
  opacity: 1;
  transform: translateY(0);
}

.text-card {
  background: #fdfdfd;
  padding: 4rem;
  border-radius: 28px;
  box-shadow: 0 20px 60px rgba(0,0,0,0.09);
  border: 1px solid #f0f0f0;
  text-align: left;
}

.paragraph {
  font-size: 1.25rem;
  line-height: 1.95;
  color: #444;
  margin-bottom: 2rem;
}

.paragraph strong {
  color: #7c704c;
  font-weight: 600;
}

.paragraph em {
  color: #7c704c;
  font-style: italic;
}

.signature {
  margin-top: 4rem;
  padding-top: 2.5rem;
  border-top: 2px solid #7c704c33;
  text-align: center;
}

.greeting {
  font-size: 1.35rem;
  color: #7c704c;
  font-style: italic;
  margin-bottom: 1rem;
}

.names {
  font-family: 'Brush Script MT', 'Lucida Handwriting', cursive, Georgia, serif;
  font-size: 2.6rem;
  color: #7c704c;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
}

.heart {
  color: #e63946;
  animation: heartbeat 1.6s ease infinite;
}

@keyframes heartbeat {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.18); }
}

.image-section {
  opacity: 0;
  transform: translateY(50px);
  transition: all 1.3s cubic-bezier(0.25, 0.8, 0.25, 1) 0.15s;
}

.image-section.visible {
  opacity: 1;
  transform: translateY(0);
}

.image-container {
  position: relative;
  max-width: 580px;
  margin: 0 auto;
}

.profile-image {
  width: 100%;
  height: auto;
  border-radius: 28px;
  box-shadow: 0 25px 70px rgba(0,0,0,0.16);
  transition: transform 0.7s ease;
}

.image-container:hover .profile-image {
  transform: translateY(-8px) scale(1.02);
}

.image-border {
  position: absolute;
  inset: -24px;
  border: 3px solid #7c704c;
  border-radius: 32px;
  pointer-events: none;
  opacity: 0.3;
  z-index: -1;
}
</style>