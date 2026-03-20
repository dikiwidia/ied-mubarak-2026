<script setup lang="ts">
import back_2 from "../assets/images/back_2.png";
import moon from "../assets/images/moon.png";
import our_picture from "../assets/images/our_picture.png";
import lamp from "../assets/images/lamp.png";
import rice_cake from "../assets/images/rice_cake.png";
import cloud from "../assets/images/cloud.png";
import drum from "../assets/images/bedug.gif";
import audio_ramadan from "../assets/audios/audio_ramadan.mp3";
import { onMounted, ref } from "vue";
import { isGlobalLoading } from "../store/loader";
import { Icon } from "@iconify/vue";

const iedFitr = ref<string>("Idul Fitri");
const audioPlayer = ref<HTMLAudioElement | null>(null);
const audioOn = ref<boolean>(false);
// const isVisible = ref<boolean>(true);
const progress = ref<number>(0);

const sendMoney = (): void => {
  const link =
    "https://link.dana.id/minta?full_url=https://qr.dana.id/v1/281012012019090581813815";
  window.open(link, "_blank");
};

const sendGreeting = (): void => {
  const phoneNumber = "6285311555456";
  const message =
    "Terima kasih, Selamat Hari Raya Idul Fitri 1447H, Mohon Maaf Lahir dan Batin 😊😊😊";
  const encodedMessage = encodeURIComponent(message);
  const link = `https://api.whatsapp.com/send?phone=${phoneNumber}&text=${encodedMessage}`;
  window.open(link, "_blank");
};

const playAudio = async () => {
  if (audioPlayer.value) {
    try {
      await audioPlayer.value.play();
      console.log("Audio playing successfully");
    } catch (err) {
      console.warn("Autoplay blocked. Waiting for user interaction.", err);

      // Fallback: Listen for the first click on the document to start audio
      const enableAudio = async () => {
        await audioPlayer.value?.play();
        document.removeEventListener("click", enableAudio);
      };
      document.addEventListener("click", enableAudio);
    }
  }
};

const stopAudio = () => {
  if (audioPlayer.value) {
    audioPlayer.value.pause();
    audioPlayer.value.currentTime = 0;
  }
};

const openGreeting = () => {
  isGlobalLoading.value = false;
  // playAudio();
};

onMounted(() => {
  const interval = setInterval(() => {
    progress.value++;
    if (progress.value === 100) {
      clearInterval(interval);
      openGreeting();
    }
  }, 50);
});
</script>

<template>
  <div class="bg-green-200 min-h-screen w-full flex justify-center p-0 xl:p-2">
    <div
      :class="`flex-col items-center justify-center ${isGlobalLoading === false ? 'hidden' : 'flex'}`"
    >
      <div
        v-if="progress < 100"
        class="flex flex-col items-center justify-center gap-5"
      >
        <div class="spinner"></div>
        <p
          class="font-medium font-google-capriola animate-pulse text-slate-800 px-12 text-center"
        >
          Memuat Kartu Ucapan ... {{ progress }}%
        </p>
      </div>
      <div v-else>
        <button
          @click="openGreeting"
          class="bg-green-500 px-4 py-2 rounded font-google-capriola text-slate-50 hover:text-white animate-zoom-pulse shadow cursor-pointer"
        >
          Buka Ucapan Hari Raya
        </button>
      </div>
    </div>
    <div
      :class="`w-full xl:w-1/4 flex-col items-center justify-center animate-gradient-bg rounded-none xl:rounded-2xl shadow-lg p-0 relative  ${isGlobalLoading === false ? 'flex' : 'hidden'}`"
    >
      <div
        class="flex flex-col items-center justify-end w-full min-h-full absolute bottom-0 z-40 text-center xl:px-16 px-10 pb-24"
      >
        <img :src="moon" alt="" class="w-30 opacity-75 pb-2" />
        <img :src="our_picture" alt="" class="w-60 py-1 animate-zoom-pulse" />
        <h3 class="font-google-capriola text-xl pt-2">Selamat Hari Raya</h3>
        <h1
          class="font-bold font-google-capriola text-4xl py-2 animate-typing w-max"
          :style="{ '--chars-step': iedFitr.length }"
        >
          {{ iedFitr }}
        </h1>
        <h3 class="font-google-capriola text-xl pb-3">1 Syawal 1447 H.</h3>
        <p class="font-medium text-sm font-google-roboto-flex text-gray-700">
          Idul Fitri adalah momen berbagi kasih dan memaafkan. Semoga kita
          selalu dalam lindungan-Nya.<br />Mohon maaf lahir dan batin.
        </p>
        <div class="border border-slate-600 w-2/3 mt-3 inset-0 shadow"></div>
        <p class="font-medium text-sm font-google-capriola py-5">
          Moch Diki Widianto & Rosi Mulyaningsih
        </p>
      </div>
      <div class="flex w-full items-end justify-end absolute bottom-0 z-0">
        <img
          :src="back_2"
          class="w-full h-full object-cover object-center opacity-5"
          alt=""
        />
      </div>
      <div
        class="absolute z-30 -top-1 right-0 w-full flex items-start justify-between"
      >
        <div class="px-5 w-1/2">
          <img :src="lamp" alt="" class="w-20 opacity-80 animate-swing" />
        </div>
        <div class="px-5 h-1/2">
          <img :src="rice_cake" alt="" class="w-20 opacity-80 animate-swing" />
        </div>
      </div>
      <div
        class="absolute z-20 -top-30 left-0 w-full flex items-center justify-center"
      >
        <div class="flex items-center justify-center w-full">
          <img
            :src="cloud"
            alt=""
            class="w-full h-full object-cover opacity-30"
          />
        </div>
      </div>
      <div
        class="lg:absolute fixed z-40 bottom-0 left-0 w-full flex items-end justify-center"
      >
        <div class="w-1/2">
          <button
            @click.prevent="sendGreeting"
            class="flex gap-1 items-center justify-start px-2 bg-lime-500 font-google-capriola text-sm py-4 w-full rounded-tl-xl xl:rounded-s-xl text-slate-50 hover:text-white"
          >
            <Icon icon="mdi:greeting-card-open" class="text-xl" />
            Kirim Pesan
          </button>
        </div>
        <div class="w-1/2">
          <button
            @click.prevent="sendMoney"
            class="flex gap-1 items-center justify-end px-2 bg-emerald-500 font-google-capriola text-sm py-4 w-full rounded-tr-xl xl:rounded-e-xl cursor-pointer text-slate-50 hover:text-white"
          >
            Bagikan THR
            <Icon icon="mdi:donate-outline" class="text-xl" />
          </button>
        </div>
      </div>
      <div
        @click="
          () => {
            audioOn = !audioOn;
            audioOn ? playAudio() : stopAudio();
          }
        "
        class="lg:absolute fixed bottom-0 center-0 rounded-full bg-gradient-to-r from-lime-500 to-emerald-500 h-26 w-26 flex flex-col items-center justify-center z-40"
      >
        <img :src="drum" alt="" :class="`w-16 ${audioOn ? '' : 'grayscale'}`" />
        <span
          class="flex items-center justify-center text-xs font-google-roboto text-white gap-0.5 font-medium"
        >
          <Icon
            :icon="`${audioOn ? 'ic:round-music-note' : 'ic:round-music-off'}`"
          ></Icon
          >Musik</span
        >
      </div>
    </div>
  </div>
  <audio ref="audioPlayer" :src="audio_ramadan" preload="auto" loop></audio>
</template>
