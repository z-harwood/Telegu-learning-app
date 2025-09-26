Telugu Learning Hub Telugu Learning Hub
A modern, interactive web application designed to help English speakers learn to read and write the Telugu script, from the basic alphabet to more complex symbols. This project is a single, self-contained HTML file powered by Firebase for progress tracking.

Live Demo: [Link to your live app here!]

✨ Key Features
Comprehensive Curriculum: Learn the complete Telugu script, including:

Alphabet: All vowels and consonants.

Gunintalu: Essential vowel combinations.

Vottulu: Consonant conjuncts for forming complex sounds.

Interactive Learning:

Animated Writing Guide: A clean "reveal" animation shows how each letter is formed.

Audio Pronunciation: Click the speaker icon to hear a clear, native pronunciation of each letter.

Confidence Tracking: Rate your confidence ("Not Sure," "Getting There," "Confident") for each letter to focus your practice.

Gamified Progress:

Progress Dashboard: Visually track your mastery of each learning module.

Achievements: Unlock badges for reaching learning milestones.

Cloud Sync: All progress is saved in real-time to the cloud with Firebase, allowing you to continue your learning journey on any device.

Android Ready: Built with Capacitor to be easily packaged as a native Android application for the Google Play Store.

🚀 How to Use the App
Navigate the Sections: Use the "Progress," "Learn," and "Practice" tabs at the top to switch between views.

Learn the Letters: In the "Learn" tab, click on any letter card to open a detailed view.

Hear the Sound: Click the speaker icon to listen to the correct pronunciation.

Rate Your Confidence: Use the buttons at the bottom of the detail view to track how well you know each letter. Your progress is saved automatically.

🛠️ Setup and Development
This project is a single index.html file but uses modern tools for development and packaging.

Prerequisites
Node.js: Download & Install Node.js

Android Studio: Download & Install Android Studio for Android packaging.

A Firebase Project: You will need a free Firebase project to handle user progress saving.

Local Development
Because the app uses JavaScript modules, you need to serve it from a local web server to test it in your browser.

Place the index.html file in a project folder.

Open a terminal in that folder.

Run the following command (requires Python): python -m http.server

Open your browser and navigate to http://localhost:8000.

Packaging for Android
This project uses Capacitor to wrap the web app in a native Android shell. The guide.md file in this repository contains a full, step-by-step guide for this process.

💻 Technology Stack
Frontend: HTML5, Tailwind CSS, Vanilla JavaScript (ESM)

Animation: D3.js

Backend & Database: Google Firebase (Firestore & Anonymous Authentication)

Mobile Packaging: Capacitor.js

📄 License
This project is open-source and available under the MIT License.
