<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'

// const fileElement = document.querySelector("#myfile");


// fileElement.addEventListener("change", (event) => {
//   console.log(event)
//   console.log(event.target.files[0].name)
// });

const fileSelected = async (e) => {
console.log(process.env.VUE_APP_APIKEY)
  if (e.target.files.length === 0) return

  let f = e.target.files[0]
  //let dotCount = f.name.match(/[.]/g).length
  //let extension = f.name.substr(f.name.lastIndexOf('\\') + 1).split('.')[dotCount]

  if (f.name.length > 2000) {
    alert('File name is too long.')
    return
  }
  // if (extension.toUpperCase() != 'PDF') {
  //   alert('Only files with a .PDF extension are allowed.')
  //   return
  // }
  
  const data = new FormData()
  data.append('file', f, f.name)

  
data.append('UPLOADCARE_PUB_KEY', 'demopublickey');
data.append('UPLOADCARE_STORE', '1');


  for (var pair of data.entries()) {
    console.log(pair[0]+ ', ' + pair[1]); 
}
// const url = 'https://ai-picture-upscaler.p.rapidapi.com/upscaler/v2/';
const url = 'https://upload.p.rapidapi.com/base/';
const options = {
	method: 'POST',
	headers: {
		'x-rapidapi-key': '3afbffbb4dmsh62c90aa1fc83dbdp1eab72jsn11ce19fa00de',
		'x-rapidapi-host': 'upload.p.rapidapi.com'
	},
	body: data
};


try {
	const response = await fetch(url, options);
	const result = await response.text();
	console.log(result);
} catch (error) {
	console.error(error);
}

}

</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <label for="myfile">Select a file:</label>
<input type="file" id="myfile" name="myfile" @change="fileSelected">

  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
