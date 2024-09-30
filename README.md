# People Carousel App

This is a **People Carousel** app built using React. It allows users to browse through a list of people, view random profiles, and navigate forward or backward through the list.

## Features

- **View People**: Displays a person's name, job title, image, and description.
- **Navigation**: Browse to the next or previous person using navigation buttons.
- **Random Person**: Select a random person from the list using the "Surprise Me" button.
- **Circular Navigation**: If you reach the end or the beginning of the list, navigation wraps around.

## Installation

### Prerequisites

Before you start, ensure you have the following installed:

- **Node.js**: [Download Node.js](https://nodejs.org/)
- **npm** (Node Package Manager)

### Installation Steps

1. **Clone the repository:**

   ```bash
   git clone <repository_url>
   cd people-carousel-app
   ```

2. **Install the dependencies:**

   Run the following command to install the project dependencies:

   ```bash
   npm install
   ```

3. **Start the development server:**

   After installation, start the app by running:

   ```bash
   npm start
   ```

4. **View the app:**

   Open your browser and navigate to `http://localhost:3000` to view the running app.

## Code Overview

### Component Breakdown

The app uses a functional component `App` that displays the current person’s data based on their index. The navigation is controlled by the following functions:

- **`nextPerson`**: Moves to the next person in the array.
- **`prevPerson`**: Moves to the previous person.
- **`randomPerson`**: Picks a random person from the array, and if the random selection matches the current person, it picks the next one.

### Key Functions

#### `checkNumber(number)`

This utility function ensures that the index number stays within the valid range. It wraps the index around if it exceeds the array length or goes below zero.

```javascript
const checkNumber = (number) => {
  if (number > people.length - 1) return 0;
  if (number < 0) return people.length - 1;
  return number;
};
```

**nextPerson()**
Increments the current index by 1, wrapping around to the start of the array if necessary.

```javascript
Copy code
const nextPerson = () => {
setIndex((currentIndex) => {
const newIndex = currentIndex + 1;
return checkNumber(newIndex);
});
};
```

**prevPerson()**
Decrements the current index by 1, wrapping around to the end of the array if necessary.

```javascript
const prevPerson = () => {
  setIndex((currentIndex) => {
    const newIndex = currentIndex - 1;
    return checkNumber(newIndex);
  });
};
```

**randomPerson()**
Selects a random person. If the random index matches the current index, it picks the next person in the list.

```javascript
const randomPerson = () => {
let randomNumber = Math.floor(Math.random() \* people.length);
if (randomNumber === index) {
randomNumber = checkNumber(index + 1);
}
setIndex(randomNumber);
};
```

### Stale State Issue

Issue Description
When working with React state and updating it inside a function, there's a potential stale state issue. For instance, if you use the previous index value inside a setter function (setIndex) without accessing the latest state, you might get an outdated value.

In this case, the setIndex function inside nextPerson, prevPerson, and randomPerson uses a functional update pattern. This ensures that the most recent state is used when updating the index:

```javascript
setIndex((currentIndex) => {
  // Logic using currentIndex, which is always up-to-date
});
```

Why This Matters
Using the current state directly (index instead of currentIndex in the setter) can lead to unexpected behavior when the state is updated asynchronously. By using a functional update, React guarantees that the function will always receive the most recent state, avoiding stale state problems.

### Dependencies

This app uses the following dependencies:

- React: Core library for building the user interface.
- React Icons: Provides icon components for use in the app. We use Chevron icons (FaChevronLeft and FaChevronRight) for navigation.
  You can install additional dependencies using npm:
