<template>
  <div>
    <Header />
    <main>
      <article dir="rtl" class="relative grid items-center justify-center">
        <ClientOnly>
          <div
            id="song-page"
            class="relative w-screen h-full flex flex-col justify-center items-center mt-14"
          >
            <div
              id="bg"
              class="fixed w-screen h-screen ml-auto mr-auto inset-0"
            >
         
              <img
                id="art"
                :src="songs.image"
                class="opacity-20 relative w-screen h-screen inset-0 mix-blend-multiply"
              />
            </div>

            <!-- audio player -->

            <div
              id="player"
              class="player w-full flex flex-col items-center relative mb-8 mt-6"
            >
              <label id="labelHe" class="text-2xl font-bold mb-1" for="audio"
              >{{ songs.title }}
            </label>

              <label id="labelEn" dir="ltr" class="text-sm font-normal mb-3" for="audio"
                >{{ songs.titleEn }}
              </label>
              <audio controls :src="songs.audio"></audio>
            </div>
          <ContentRenderer
            class="blog-link text-white relative ml-auto mr-auto grid items-center"
            :value="songs"
          >
            <template #empty>
              <p>No content found.</p>
            </template>
          </ContentRenderer>
           </div>
        </ClientOnly>
      </article>
    </main>
  </div>
</template>

<script setup>
const slug = useRoute().params.slug.toString().replace(/,/g, "/");
const { data: songs } = await useAsyncData(slug, () => {
  return queryContent(slug).findOne();
});
useHead({
  title: `${songs.value.title}`,
});
</script>

<style>
#bg {
  z-index: 0;
  background: linear-gradient(
    118.74deg,
    rgba(255, 255, 255, 0.95) -9.92%,
    rgba(1, 55, 183, 0.95) 24.49%,
    rgba(0, 0, 0, 0.95) 54.61%,
    rgba(255, 0, 0, 0.95) 116.82%
  );
  background-position: center;
  background-repeat: no-repeat;
  z-index: 0;
}
#lyrics {
  font-family: 'Times New Roman', Times, serif;
  background: rgba(0, 25, 100, 0.5);
  -webkit-backdrop-filter: blur(3px);
  backdrop-filter: blur(2px);
  width: 97vw;
  box-shadow: -4px, -4px, 4px white;
  margin-top: -20px;
  padding: 10px;
  font-size: 17.5px;
}

@media (min-width: 600px) {
  #lyrics {
    font-size: 21px;
    line-height: 2rem;
    width: 80vw;
    padding:1rem 2rem;
  }
}
@media (min-width: 1000px) {
  #lyrics {
    width: 60vw;
    padding: 2rem 4rem;
  }
}
nuxt-link {
  text-decoration: none;
}
</style>
