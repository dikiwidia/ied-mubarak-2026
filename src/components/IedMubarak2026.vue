<script setup lang="ts">
import back_2 from "../assets/images/back_2.png";
import moon from "../assets/images/moon.png";
import our_picture from "../assets/images/our_picture.png";
import lamp from "../assets/images/lamp.png";
import rice_cake from "../assets/images/rice_cake.png";
import cloud from "../assets/images/cloud.png";
import drum from "../assets/images/bedug.gif";
import { ref } from "vue";

const iedFitr = ref<string>("Idul Fitri");

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
</script>

<template>
  <div class="bg-green-200 min-h-screen w-full flex justify-center p-0 xl:p-2">
    <div
      class="w-full xl:w-1/4 flex flex-col items-center justify-center animate-gradient-bg rounded-none xl:rounded-2xl shadow-lg p-0 relative"
    >
      <div
        class="flex flex-col items-center w-full absolute bottom-0 z-30 text-center xl:px-16 px-10 pb-24"
      >
        <img :src="moon" alt="" class="w-30 opacity-75" />
        <img :src="our_picture" alt="" class="w-60 py-3 animate-zoom-pulse" />
        <h3 class="font-google-capriola text-xl pt-5">Selamat Hari Raya</h3>
        <h1
          class="font-bold font-google-capriola text-4xl py-2 animate-typing w-max"
          :style="{ '--chars-step': iedFitr.length }"
        >
          {{ iedFitr }}
        </h1>
        <h3 class="font-google-capriola text-xl pb-5">1 Syawal 1447 H.</h3>
        <p class="font-medium text-sm font-google-roboto-flex text-gray-700">
          Ramadhan telah berlalu, Tiada kesucian tanpa permohonan maaf, tiada
          kedamaian tanpa ketulusan. Selamat Hari Raya Idul Fitri. Mohon maaf
          lahir dan batin.
        </p>
        <div class="border border-slate-400 w-2/3 mt-4 inset-0 shadow"></div>
        <p class="font-medium text-sm font-google-capriola py-4">
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
        class="absolute z-20 -top-1 right-0 w-full flex items-start justify-between"
      >
        <div class="px-5 w-1/2">
          <img :src="lamp" alt="" class="w-20 opacity-80 animate-swing" />
        </div>
        <div class="px-5 h-1/2">
          <img :src="rice_cake" alt="" class="w-20 opacity-80 animate-swing" />
        </div>
      </div>
      <div
        class="absolute z-10 -top-30 left-0 w-full flex items-center justify-center"
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
        class="absolute z-40 bottom-0 left-0 w-full flex items-end justify-center"
      >
        <div class="w-1/2">
          <button
            @click.prevent="sendGreeting"
            class="flex items-center justify-start px-4 bg-blue-400 font-google-capriola py-4 w-full rounded-tl-2xl xl:rounded-s-2xl text-slate-50 hover:text-white"
          >
            Kirim Ucapan
          </button>
        </div>
        <div class="w-1/2">
          <button
            @click.prevent="sendMoney"
            class="flex items-center justify-end px-4 bg-green-400 font-google-capriola py-4 w-full rounded-tr-2xl xl:rounded-e-2xl cursor-pointer text-slate-50 hover:text-white"
          >
            Bagi THR
          </button>
        </div>
      </div>
      <div
        class="absolute bottom-0 center-0 rounded-full bg-gradient-to-r from-blue-400 to-green-400 h-24 w-24 flex items-center justify-center z-40"
      >
        <img :src="drum" alt="" class="w-20" />
      </div>
    </div>
  </div>
</template>
