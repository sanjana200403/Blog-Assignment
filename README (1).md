# Blog Application

The Blog Application is a full-stack web app built with the MERN stack (MongoDB, Express, React, Node.js). This application allows users to create, edit, and manage blog posts, as well as interact with other users through comments.

## Table of Contents

1. [Introduction](#introduction)
2. [Features](#features)
3. [Tech Stack](#tech-stack)
4. [Installation](#installation)
5. [Running the Project](#running-the-project)
6. [Usage](#usage)
7. [ CI/CD Pipeline ](#)
8. [Docker](#Docker)
9. [Contributing](#contributing)
10. [License](#license)

## Introduction

The Blog Application provides a platform for users to share their thoughts and engage with others through comments. Users can manage their profiles and follow other users, creating a community of writers and readers.

## Features

- User Authentication: Secure login and signup functionality..
- Create, Read, Update, Delete (CRUD): Full CRUD operations for blog posts.
- Commenting System: Users can comment on posts and engage in discussions.
-  Admins have complete visibility over all user and their Posts.
- Secure user authentication and role-based access control.

## Tech Stack

- **Frontend**: React, Javascript, HTML
- **Backend**: Node.js, Express, MongoDB (Mongoose)
- **Styling**: CSS

## Installation

Follow these steps to set up the project locally:

### Prerequisites

- **Node.js** (version 14.x or above)
- **npm** 
- **MongoDB** (Ensure MongoDB is running locally or provide a remote connection string)

### Steps to Install

1. **Clone the Repository**

   ```bash
   git clone https://github.com/sanjana200403/Blog-Assignment
   cd Blog-Assignment

2. **Install server dependencies**

   ```bash
   cd backend
   npm install

3. **Install client dependencies**

   ```bash
   cd frontend
   npm install

### Running the Project

  1. **Navigate to the backend directory**
     ```bash
     cd backend

  2. **Start the backend server:**
     ```bash
     npm Start
  2. **Navigate to the Frontend directory**
     ```bash
      cd frontend
   2. **Start the Frontend**
     ```bash
     npm  run dev  

### Usage
Once the application is running:

Open Your Browser: Navigate to http://localhost:3000.

Login or Signup: If you don't have an account, use the signup feature to create one.

Create Blog Posts: Users can create new posts and manage existing ones.

Engage with Other Users: Comment on posts and interact with the community.


Admin Panel: Admins can view all users and their blogs

## Tech Stack
- To containerize the application, follow these steps:
## Dockerfile (for Backend)

### Backend Dockerfile

FROM node:14

### Set the working directory
WORKDIR /app

### Copy package.json and package-lock.json
COPY backend/package*.json ./

### Install dependencies
RUN npm install

### Copy the rest of the application
COPY backend/ .

### Expose the backend port
EXPOSE 5000

### Start the server
CMD ["npm", "start"]

## Dockerfile (for Frontend)
 
### Frontend Dockerfile

FROM node:14

### Set the working directory
WORKDIR /app

### Copy package.json and package-lock.json
COPY frontend/package*.json ./

### Install dependencies
RUN npm install

### Copy the rest of the application
COPY frontend/ .

### Build the app
RUN npm run build

### Expose the frontend port
EXPOSE 3000

### Start the server
CMD ["npx", "serve", "-s", "build"]


  ## CI/CD Pipeline
- To set up a CI/CD pipeline using GitHub Actions, create a .github/workflows/ci-cd.yml file: 
    ```bash
      name: CI/CD Pipeline

      on:
      push:
    branches:
      - main

    jobs:
    build:

    runs-on: ubuntu-latest

    services:
      mongo:
        image: mongo
        ports:
          - 27017:27017

      steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'

      - name: Install backend dependencies
        run: |
          cd backend
          npm install

      - name: Run backend tests
        run: |
          cd backend
          npm test

      - name: Install frontend dependencies
        run: |
          cd frontend
          npm install

      - name: Run frontend tests
        run: |
          cd frontend
          npm test
 

## Docker Compose
To run both services together:
  ```bash
     version: '3.8'

     services:
     backend:
     build:
       context: .
       dockerfile: Dockerfile.backend
     ports:
      - "5000:5000"
     depends_on:
      - mongo

     frontend:
      build:
      context: .
      dockerfile: Dockerfile.frontend
     ports:
      - "3000:3000"

     mongo:
       image: mongo
       ports:
          - "27017:27017"

