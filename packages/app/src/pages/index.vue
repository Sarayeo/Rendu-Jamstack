<script lang="ts" setup>
const {find} = useStrapi()
const {data: suspects,pending,error} =useAsyncData('suspects',() => find('suspects',{
  populate:'*',
}))
onMounted(() => 
console.log({
  suspects,pending,error
}))
</script>
<template>

  <header>
    <div>
      <img src="../assets/css/images/cinamorol.png" alt=" intro image" style="width: 80%;height: auto;">
    </div>
    <div id="background" class="flex flex-col ml-[-8]">
      <div id="gallery" v-if="suspects">
      <figure class="pic1" v-for="suspect in suspects.data" :key="suspect.id">
        <NuxtImg
        :src="suspect.idpicture.url" alt="" aria-hidden="true"
        class="h-[500px] object-contain object-center w-full bg-white"
      />
        <figcaption>{{ suspect.name}}</figcaption>
      </figure>
    </div>
      <div>
        <p class="color-white mt-6">
          Step into the enchanting Sanrio Village, where the adorable character Cinnamoroll has met a mysterious end. As the investigator, explore vibrant locations, gather clues, and interview Sanrio characters to unveil the truth. Solve the puzzle, expose the culprit, and bring justice to this charming village. The fate of Sanrio Village is in your hands.
        </p>
      </div>
    </div>
  </header>
  <div class="">
    <div class="flex flex-col items-center color-white ">
      <h1 class="text-4xl font-bold"> Take a look at the suspects and the victim and their stories </h1>

      <ul id="filters">
	        <li><button class="active" data-filter="all">all</button></li>
	        <li><button data-filter="rojo">friends</button></li>
	        <li><button data-filter="verde">accountences</button></li>
	        <li><button data-filter="azul">unknown</button></li>
      </ul>

      <div v-if="suspects">
        <ul class="color-white">
          <li v-for="suspect in suspects.data" :key="suspect.id">
            {{ suspect.name}}
          </li>
        </ul>
      </div>
      <div class="container" v-if="suspects">
	        <div class="box box-2" v-for="suspect in suspects.data" :key="suspect.id" data-text="no name"> <NuxtImg
        :src="suspect.image[0].url" alt="" aria-hidden="true"
        class="h-[500px] object-contain object-center w-full bg-white"
      />
        </div>
      </div>
    </div>
  </div>
</template>
