<script>
  import { images } from "./imageData";
  import Slide from "./components/Slideshow.svelte";
  import { each } from "svelte/internal";
  import Caption from "./components/Caption.svelte";
  import Thumbnail from "./components/Thumbnail.svelte";

  let imageShowIndex = 0;
  $: console.log(imageShowIndex);

  const prevSlide = () => {
    if (imageShowIndex === 0) {
      imageShowIndex = images.length - 1;
    } else {
      imageShowIndex -= 1;
    }
  };
  const nextSlide = () => {
    if (imageShowIndex === images.length - 1) {
      imageShowIndex = 0;
    } else {
      imageShowIndex += 1;
    }
  };
const goToSlide = (idNumber) => imageShowIndex = idNumber;

</script>

<div class="container-fluid">
  {#each images as { id, name, imgurl, attribution }}
    <Slide
      image={imgurl}
      altTag={name}
      attr={attribution}
      slideNo={id + 1}
      totalSlides={images.length}
      imageShowing={id === imageShowIndex}
    />
  {/each}
</div>

<Caption
  caption={images[imageShowIndex].name}
  on:prevClic={prevSlide}
  on:nextClic={nextSlide}
/>
<div class="thumbnails-row">
{#each images as {id, imgurl, name} }
  <Thumbnail thumbImg={imgurl} altTag={name} on:click={() => goToSlide(id)}/>
{/each}
</div>


<style>
    .container-fluid {
    position: relative;
  }
    /* main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	} */
</style>
