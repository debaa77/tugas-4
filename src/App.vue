<template>
  <div id="app">
    <div class="container">
      <!-- Counter App -->
      <div class="counter">
        <h2>Counter: {{ counter }}</h2>
        <div class="button-group">
          <button @click="incrementCounter">Increment</button>
          <button @click="decrementCounter">Decrement</button>
        </div>
      </div>

      <!-- Color Box -->
      <div class="color-box">
        <div :style="{ backgroundColor: boxColor }" class="box"></div>
        <button @click="changeColor">Change Color</button>
      </div>

      <!-- Image Slider -->
      <div class="slider">
        <button @click="prevImage" class="slider-button">Previous</button>
        <div class="slider-image-container">
          <img :src="currentImage" alt="Image Slider" class="slider-image" />
        </div>
        <button @click="nextImage" class="slider-button">Next</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      counter: 0,
      boxColor: '#ff0000',
      images: [],
      currentIndex: 0,
    };
  },
  methods: {
    incrementCounter() {
      this.counter += 1;
    },
    decrementCounter() {
      if (this.counter > 0) {
        this.counter -= 1;
      }
    },
    changeColor() {
      this.boxColor = '#' + Math.floor(Math.random() * 16777215).toString(16);
    },
    fetchImages() {
      // Generate URLs for placeholder images
      this.images = Array.from({ length: 10 }, (_, i) => `https://picsum.photos/seed/${i}/800/600`);
      if (this.images.length > 0) {
        this.currentIndex = 0; // Initialize with the first image
      }
    },
    prevImage() {
      if (this.images.length > 0) {
        this.currentIndex = (this.currentIndex - 1 + this.images.length) % this.images.length;
      }
    },
    nextImage() {
      if (this.images.length > 0) {
        this.currentIndex = (this.currentIndex + 1) % this.images.length;
      }
    },
  },
  computed: {
    currentImage() {
      return this.images[this.currentIndex];
    },
  },
  created() {
    this.fetchImages();
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  background-color: #f9f9f9;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 40px;
  width: 90%;
  max-width: 1000px;
}

.counter, .color-box, .slider {
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  padding: 20px;
  width: 100%;
  max-width: 500px;
}

.counter h2 {
  margin-bottom: 20px;
  font-size: 24px;
}

.button-group {
  display: flex;
  justify-content: space-between;
}

button {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #0056b3;
}

.color-box {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.box {
  width: 100px;
  height: 100px;
  border-radius: 8px;
  margin-bottom: 10px;
}

.slider {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

.slider-button {
  background-color: #28a745;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s;
}

.slider-button:hover {
  background-color: #218838;
}

.slider-image-container {
  flex-grow: 1;
  display: flex;
  justify-content: center;
}

.slider-image {
  max-width: 100%;
  max-height: 300px;
  border-radius: 8px;
}
</style>
