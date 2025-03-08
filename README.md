# SmartMate

SmartMate is an intelligent personal assistant to-do list application designed to help users efficiently manage their tasks and schedules. Built with uni-app + Vue3 + TypeScript and Element-plus for the UI, SmartMate combines the best of modern web technologies with native app capabilities.

---

## Overview

SmartMate enables users to organize their daily tasks, set reminders, and even leverage external LLM APIs for smart task planning. The application is structured to be easily extensible in the future, with local data storage via plus.sqlite for native platforms and plans for cloud/back-end synchronization when needed.

---

## Key Features

### 1. To-do List Management
- **Multiple To-do Lists:** Create and manage several to-do lists.
- **Grouping:** Organize lists into groups/categories for better structure.
- **Task Management:**
    - **Basic Task Information:** Each task includes a title, due date, and notes.
    - **Subtasks Support:** Break tasks into smaller, manageable actions.
    - **Subtask Upgrading:** Subtasks can be upgraded to full tasks when needed.

### 2. Schedule Reminders
- **Deadline Reminders:** Set due dates for tasks with timely notifications.
- **Customizable Alerts:** Configure reminder intervals and alert settings to suit personal needs.

### 3. Intelligent Task Planning
- **LLM Integration:** Use external LLM APIs (such as OpenAI GPT) to help break down complex tasks into actionable subtasks.
- **User-configurable Tokens:** Users can enter their API tokens to connect with popular LLM services.
- **Smart Suggestions:** Receive AI-driven insights for task prioritization and planning.

---

## Development Roadmap

### Short-Term Goals
- [ ] **Core To-do Management:** Implement comprehensive to-do list and task management (including grouping and subtasks).
- [ ] **Schedule Reminders:** Integrate local notifications for task deadlines.
- [ ] **Basic LLM Integration:** Develop the interface to call external LLM APIs for task decomposition and planning.

### Long-Term Goals
- [ ] **Enhanced AI Planning:** Further improve the intelligent planning module with more advanced AI suggestions.
- [ ] **Multi-Platform Support:** Extend functionality to additional platforms (e.g., small programs) and add data synchronization with a backend.
- [ ] **User Experience:** Continuously optimize the UI/UX based on user feedback and industry best practices.

---

## Feature List

The following is a list of features planned for development, with checkboxes to track the development status:

- [ ] **To-do List Creation & Management**
  - [ ] Create/Edit/Delete to-do lists.
  - [ ] Grouping of to-do lists.
- [ ] **Task Management**
  - [ ] Add tasks within a to-do list.
  - [ ] Task details: title, due date, and notes.
  - [ ] Support for subtasks and subtask promotion.
- [ ] **Schedule Reminders**
  - [ ] Set task deadlines.
  - [ ] Local notifications for reminders.
- [ ] **Intelligent Task Planning**
  - [ ] Integration with external LLM APIs (e.g., OpenAI GPT).
  - [ ] User-configurable API token settings.
  - [ ] AI-powered task decomposition and suggestions.
- [ ] **Data Storage & Synchronization**
  - [ ] Use plus.sqlite for local data storage on native platforms.
  - [ ] Future support for cloud/back-end data synchronization.
- [ ] **Cross-Platform Compatibility**
  - [ ] Support for App, mini-programs, H5, etc.

---

## Technologies Used
- **Framework:** uni-app + Vue3
- **Language:** TypeScript
- **UI Library:** Element-plus
- **Package Manager:** Yarn
- **Local Storage:** plus.sqlite (native), uni.setStorageSync for quick prototyping on other platforms
- **LLM API Integration:** Support for popular LLM interfaces via user-supplied tokens
