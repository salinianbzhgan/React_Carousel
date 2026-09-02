# Ex05 Image Carousel


## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM
App.jsx
~~~
import React, { useEffect, useState } from "react";
import "./App.css";

function App() {
  const images = [
    "https://picsum.photos/id/1015/800/450",
    "https://picsum.photos/id/1016/800/450",
    "https://picsum.photos/id/1018/800/450",
    "https://picsum.photos/id/1020/800/450",
  ];

  const [currentIndex, setCurrentIndex] = useState(0);

  // Next image
  const nextImage = () => {
    setCurrentIndex((currentIndex + 1) % images.length);
  };

  // Previous image
  const previousImage = () => {
    setCurrentIndex(
      (currentIndex - 1 + images.length) % images.length
    );
  };

  // Automatic rotation
  useEffect(() => {
    const interval = setInterval(() => {
      setCurrentIndex((currentIndex) => (currentIndex + 1) % images.length);
    }, 3000);

    return () => clearInterval(interval);
  }, [images.length]);

  return (
    <div className="app">
      <h1>Image Carousel</h1>

      <div className="carousel">
        <img
          src={images[currentIndex]}
          alt={`Slide ${currentIndex + 1}`}
        />

        <button className="prev" onClick={previousImage}>
          ❮
        </button>

        <button className="next" onClick={nextImage}>
          ❯
        </button>
      </div>

      <div className="dots">
        {images.map((_, index) => (
          <span
            key={index}
            className={index === currentIndex ? "dot active" : "dot"}
            onClick={() => setCurrentIndex(index)}
          ></span>
        ))}
      </div>

      <p>
        Image {currentIndex + 1} of {images.length}
      </p>
    </div>
  );
}

export default App;
~~~
App.css
~~~
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, sans-serif;
  background: #f2f2f2;
}

.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 20px;
}

h1 {
  font-size: 32px;
}

.carousel {
  position: relative;
  width: 800px;
  max-width: 90%;
  overflow: hidden;
  border-radius: 12px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.2);
}

.carousel img {
  width: 100%;
  height: 450px;
  display: block;
  object-fit: cover;
}

button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  border: none;
  background: rgba(0, 0, 0, 0.5);
  color: white;
  font-size: 30px;
  padding: 10px 16px;
  cursor: pointer;
  border-radius: 6px;
}

button:hover {
  background: rgba(0, 0, 0, 0.8);
}

.prev {
  left: 15px;
}

.next {
  right: 15px;
}

.dots {
  display: flex;
  gap: 8px;
}

.dot {
  width: 12px;
  height: 12px;
  background: #bbb;
  border-radius: 50%;
  cursor: pointer;
}

.dot.active {
  background: #333;
}

p {
  font-size: 16px;
}
~~~

## OUTPUT
<img width="1142" height="862" alt="image" src="https://github.com/user-attachments/assets/5e4f202c-7195-4e51-9fa2-a674feb9de9c" />

<img width="1142" height="865" alt="image" src="https://github.com/user-attachments/assets/9e09fd1e-b424-4def-ac0a-32228884fb64" />


## RESULT
The program for creating Image Carousel using React is executed successfully.
