# Ex05 Image Carousel
## Date: 19-05-2025

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

App.js
```
import React, { useState } from 'react';
import './App.css';

const images = [
  'Screenshot 2025-05-19 131751.png',
  'Screenshot 2025-05-19 132048.png',
  'Screenshot 2025-05-19 132251.png',
  'Screenshot 2025-05-19 132331.png',
];

function App() {
  const [current, setCurrent] = useState(0);

  const prevSlide = () => {
    setCurrent((prev) => (prev === 0 ? images.length - 1 : prev - 1));
  };

  const nextSlide = () => {
    setCurrent((prev) => (prev === images.length - 1 ? 0 : prev + 1));
  };

  return (
    <div className="app">
      <h2> Car Carousel </h2>

      <div className="carousel">
        {images.map((img, index) => {
          let className = 'slide';
          if (index === current) {
            className += ' active';
          } else if (index === (current + 1) % images.length) {
            className += ' next';
          } else if (index === (current - 1 + images.length) % images.length) {
            className += ' prev';
          }
          return <img key={index} src={img} alt="" className={className} />;
        })}

        <button className="nav left" onClick={prevSlide}>❮</button>
        <button className="nav right" onClick={nextSlide}>❯</button>
      </div>

      <footer>
        <p>© {new Date().getFullYear()} Swetha A(212223220114) All rights reserved.</p>
      </footer>
    </div>
  );
}

export default App;

```
App.css
```

.app {
  background: linear-gradient(to bottom, #736e6e 0%, #2f2f2f 50%);
  color: rgb(10, 37, 37);
  min-height: 100vh;
  text-align: center;
  padding-top: 40px;
}

.carousel {
  position: relative;
  width: 800px;
  height: 400px;
  margin: 40px auto;
  perspective: 1000px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.slide {
  position: absolute;
  width: 60%;
  height: 100%;
  opacity: 0;
  transition: transform 0.5s, opacity 0.5s;
  transform: scale(0.7);
  z-index: 1;
  border-radius: 10px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.5);
}

.slide.active {
  opacity: 1;
  transform: scale(1);
  z-index: 3;
}

.slide.prev {
  opacity: 0.5;
  transform: translateX(-80%) scale(0.8) rotateY(25deg);
  z-index: 2;
}

.slide.next {
  opacity: 0.5;
  transform: translateX(80%) scale(0.8) rotateY(-25deg);
  z-index: 2;
}


.nav {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-size: 2rem;
  background: rgba(142, 127, 127, 0.2);
  border: none;
  color: white;
  padding: 10px;
  cursor: pointer;
  z-index: 4;
  border-radius: 50%;
}

.nav.left {
  left: -50px;
}

.nav.right {
  right: -50px;
}

.nav:hover {
  background: rgba(255,255,255,0.4);
}


footer {
  background-color: #1e1e1e;
  color: #ddd;
  padding: 20px 0;
  font-size: 0.9rem;
}

.footer-links {
  margin-top: 10px;
  display: flex;
  justify-content: center;
  gap: 20px;
}

.footer-links a {
  color: #aaa;
  text-decoration: none;
  transition: color 0.3s;
}

.footer-links a:hover {
  color: #fff;
}

```


## OUTPUT

![image](https://github.com/user-attachments/assets/d08d80d3-0c16-4780-974a-461ef74a3bff)

![image](https://github.com/user-attachments/assets/93c3d68b-552c-405f-bde9-e572e67f47bf)

![image](https://github.com/user-attachments/assets/4285fbfa-cce9-471c-ad74-87df84631d81)


## RESULT
The program for creating Image Carousel using React is executed successfully.
