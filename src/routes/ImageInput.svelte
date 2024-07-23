<script>
  import { onMount } from 'svelte';

  let imageSrc = '';

  onMount(() => {
    // Load the image from localStorage if it exists
    const storedImage = localStorage.getItem('latestImage');
    if (storedImage) {
      imageSrc = storedImage;
    }
  });

  function handleImageChange(event) {
    const file = event.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = () => {
        // Save the image to localStorage
        localStorage.setItem('latestImage', reader.result);
        imageSrc = reader.result;
      };
      reader.readAsDataURL(file);
    }
  }

  function removeImage() {
    // Remove the image from localStorage
    localStorage.removeItem('latestImage');
    imageSrc = '';
  }
</script>

<style>
  .image-container {
    margin-top: 10px;
    text-align: center;
  }

  img {
    max-width: 100%;
    height: auto;
  }

  .remove-button {
    margin-top: 10px;
    background-color: var(--color-theme-1);
    border: none;
    padding: 10px 20px;
    color: white;
    cursor: pointer;
  }
</style>

<div>
  <input type="file" accept="image/*" capture="environment" on:change={handleImageChange} />
  {#if imageSrc}
    <div class="image-container">
      <img src={imageSrc} alt="Uploaded image" />
      <button class="remove-button" on:click={removeImage}>Remove Image</button>
    </div>
  {/if}
</div>
