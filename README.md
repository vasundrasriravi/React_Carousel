# Ex05 Image Carousel
## Date:

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
### ImageCarousel.js
```
import React, { useState, useEffect } from 'react';
import './ImageCarousel.css';

export default function ImageCarousel({ images, autoRotate = true, rotateInterval = 3000 }) {
  const [currentIndex, setCurrentIndex] = useState(0);
  const [isHovered, setIsHovered] = useState(false);

  const nextImage = () => setCurrentIndex(prev => (prev + 1) % images.length);
  const prevImage = () => setCurrentIndex(prev => (prev - 1 + images.length) % images.length);

  useEffect(() => {
    if (!autoRotate || isHovered) return;
    const interval = setInterval(nextImage, rotateInterval);
    return () => clearInterval(interval);
  }, [autoRotate, rotateInterval, isHovered]);

  return (
    <div
      className="carousel"
      onMouseEnter={() => setIsHovered(true)}
      onMouseLeave={() => setIsHovered(false)}
    >
      <div className="image-container">
        <img src={images[currentIndex]} alt={`Slide ${currentIndex + 1}`} />
      </div>
      <div className="buttons-container">
        <button className="nav prev" onClick={prevImage} aria-label="Previous Image">Previous</button>
        <button className="nav next" onClick={nextImage} aria-label="Next Image">Next</button>
      </div>
      <div className="indicators">
        {images.map((_, index) => (
          <span
            key={index}
            className={`dot ${currentIndex === index ? 'active' : ''}`}
            onClick={() => setCurrentIndex(index)}
          />
        ))}
      </div>
    </div>
  );
}

```
### ImageCarousel.css
```
.carousel {
  max-width: 600px;
  margin: 40px auto;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.2);
  text-align: center;
  background-color: #ffffff;
  padding-bottom: 10px;
}

.image-container {
  width: 100%;
  background: #000;
}

.image-container img {
  width: 100%;
  height: auto;
  display: block;
  border-radius: 8px 8px 0 0;
  transition: opacity 0.5s ease-in-out;
}

.buttons-container {
  margin-top: 10px;
}

.nav {
  background: #007bff;
  border: none;
  color: white;
  font-size: 1rem;
  padding: 10px 20px;
  margin: 0 10px;
  cursor: pointer;
  border-radius: 5px;
  user-select: none;
  transition: background-color 0.3s ease;
}

.nav:hover {
  background: #0056b3;
}

.indicators {
  margin-top: 15px;
}

.dot {
  display: inline-block;
  width: 10px;
  height: 10px;
  margin: 0 5px;
  background-color: #ccc;
  border-radius: 50%;
  cursor: pointer;
  transition: background-color 0.3s;
}

.dot.active {
  background-color: #007bff;
}

```
### App.js
```
import React from 'react';
import ImageCarousel from './components/ImageCarousel';
import { imageUrls } from './components/images';
import './App.css';

function App() {
  return (
    <div className="app-container">
      <h1 className="heading">Animals Carousel</h1>
      <ImageCarousel images={imageUrls} autoRotate={true} rotateInterval={3000} />
      <footer className="footer">
        <p>Designed by Vasundra Sri | Reg No: 212222230168</p>
      </footer>
    </div>
  );
}

export default App;
```
### App.css
```
body, html {
  margin: 0;
  padding: 0;
  font-family: 'Segoe UI', sans-serif;
  background-color: #87e290;
}


.app-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  text-align: center;
  padding: 20px;
}


.heading {
  font-size: 2.5rem;
  font-weight: bold;
  margin-top: 20px;
  color: #333;
}


.footer {
  background-color: #064423;
  color: white;
  padding: 15px;
  width: 100%;
  text-align: center;
  font-weight: bold;
  margin-top: 40px;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
}

```
## OUTPUT


## RESULT
The program for creating Image Carousel using React is executed successfully.
