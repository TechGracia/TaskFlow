# TaskFlow – Task Manager using Svelte

TaskFlow is a task management application built using Svelte.

This project was created to practice Svelte concepts such as state management, components, props, event handling, lifecycle methods, and local storage.

---

## Features

* Add tasks
* Edit tasks
* Delete tasks
* Mark tasks as completed
* Filter tasks (All / Active / Completed)
* Clear completed tasks
* Progress tracking
* Persistent storage using localStorage
* Responsive UI

---

## Tech Stack

* Svelte
* JavaScript
* HTML
* CSS
* Vite

---

## Concepts Used

### State Management

Used `$state()` to manage reactive data.

### Components

Split UI into reusable components.

### Props

Used `$props()` to pass data between components.

### Event Handling

Handled user interactions such as adding, editing, and deleting tasks.

### Lifecycle

Used `onMount()` to load saved tasks.

### Local Storage

Stored tasks in browser storage to persist data after refresh.

---

## Project Structure

```text
src/
│
├── routes/
│   └── +page.svelte
│
├── lib/
│   └── components/
│       └── TaskItem.svelte
```

---

## Installation

Clone repository:

```bash
git clone <repository-url>
```

Install dependencies:

```bash
npm install
```

Run locally:

```bash
npm run dev
```

---

## Future Improvements

* Backend integration
* Authentication
* Database storage
* User accounts

---

## Author

Built by Gracia using Svelte.
