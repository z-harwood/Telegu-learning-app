<!DOCTYPE html>

<html lang="en">

<head>

&nbsp;   <meta charset="UTF-8">

&nbsp;   <meta name="viewport" content="width=device-width, initial-scale=1.0">

&nbsp;   <title>Telugu Learning Hub</title>

&nbsp;   <script src="https://cdn.tailwindcss.com"></script>

&nbsp;   <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;900\&family=Noto+Sans+Telugu:wght@400;700\&display=swap" rel="stylesheet">

&nbsp;   <style>

&nbsp;       :root {

&nbsp;           --hue: 230;

&nbsp;           --primary-color: hsl(var(--hue), 90%, 60%);

&nbsp;           --bg-color: hsl(var(--hue), 30%, 98%);

&nbsp;       }

&nbsp;       body {

&nbsp;           font-family: 'Inter', sans-serif;

&nbsp;           background-color: var(--bg-color);

&nbsp;           color: hsl(var(--hue), 20%, 20%);

&nbsp;       }

&nbsp;       .telugu-char { font-family: 'Noto Sans Telugu', sans-serif; }

&nbsp;       .status-indicator { border-left-width: 5px; transition: border-color 0.3s ease; }

&nbsp;       .status-none { border-color: transparent; }

&nbsp;       .status-not-sure { border-color: #ef4444; }

&nbsp;       .status-getting-there { border-color: #f59e0b; }

&nbsp;       .status-confident { border-color: #22c55e; }

&nbsp;       .tab-btn.active { color: var(--primary-color); border-color: var(--primary-color); }

&nbsp;       .sub-tab-btn { transition: all 0.2s ease-in-out; }

&nbsp;       .sub-tab-btn.active { background-color: var(--primary-color); color: white; box-shadow: 0 4px 14px 0 hsl(var(--hue), 50%, 60%, 0.3); }

&nbsp;       .view { display: none; }

&nbsp;       .view.active { display: block; animation: fadeIn 0.4s ease-out forwards; }

&nbsp;       @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

&nbsp;       #writing-canvas { touch-action: none; }

&nbsp;       .achievement.unlocked { opacity: 1; transform: scale(1); }

&nbsp;       .achievement { opacity: 0.4; transform: scale(0.95); transition: all 0.3s ease; }

&nbsp;       #onboarding-overlay, #letter-modal { transition: opacity 0.3s ease-in-out; }

&nbsp;       #onboarding-modal, #letter-modal-content { transition: transform 0.3s ease-in-out, opacity 0.3s ease-in-out; }

&nbsp;       #app-loader { display: flex; flex-direction:column; align-items: center; justify-content: center; position: fixed; inset: 0; background-color: var(--bg-color); z-index: 100; transition: opacity 0.5s ease; padding: 1rem; }

&nbsp;       .spinner { border: 4px solid rgba(0, 0, 0, 0.1); width: 36px; height: 36px; border-radius: 50%; border-left-color: var(--primary-color); animation: spin 1s ease infinite; }

&nbsp;       @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

&nbsp;   </style>

</head>

<body class="antialiased">



&nbsp;   <div id="app-loader">

&nbsp;       <div class="spinner"></div>

&nbsp;       <p class="mt-4 text-gray-600">Loading your learning journey...</p>

&nbsp;   </div>



&nbsp;   <div id="app" class="container mx-auto p-4 max-w-5xl opacity-0" style="transition: opacity 0.5s ease;">

&nbsp;       <header class="text-center my-6">

&nbsp;           <h1 class="text-4xl md:text-5xl font-black text-transparent bg-clip-text bg-gradient-to-r from-indigo-600 to-purple-600">Telugu Learning Hub</h1>

&nbsp;           <p class="text-lg text-gray-600 mt-2">The complete journey to mastering the Telugu script.</p>

&nbsp;       </header>



&nbsp;       <nav id="main-nav" class="bg-white/70 backdrop-blur-lg p-2 rounded-xl shadow-md mb-8 sticky top-4 z-40 flex items-center justify-center gap-2" aria-label="Main navigation">

&nbsp;           <button data-view="progress" class="tab-btn text-lg font-bold py-3 px-5 border-b-4 transition-colors duration-300" aria-label="View Progress dashboard">📈 Progress</button>

&nbsp;           <button data-view="learn" class="tab-btn text-lg font-bold py-3 px-5 border-b-4 border-transparent transition-colors duration-300" aria-label="View Learn section">📚 Learn</button>

&nbsp;           <button data-view="practice" class="tab-btn text-lg font-bold py-3 px-5 border-b-4 border-transparent transition-colors duration-300" aria-label="View Practice section">✍️ Practice</button>

&nbsp;       </nav>



&nbsp;       <main>

&nbsp;           <div id="progress-view" class="view"></div>

&nbsp;           <div id="learn-view" class="view"></div>

&nbsp;           <div id="practice-view" class="view"></div>

&nbsp;       </main>

&nbsp;       

&nbsp;       <footer class="text-center mt-12">

&nbsp;           <div id="user-status" class="text-xs text-gray-500 mb-4"></div>

&nbsp;           <button id="download-btn" class="bg-gray-200 text-gray-700 font-semibold py-2 px-4 rounded-lg hover:bg-gray-300 transition-colors text-sm">Download App</button>

&nbsp;       </footer>

&nbsp;   </div>

&nbsp;   

&nbsp;   <!-- Modals -->

&nbsp;   <div id="letter-modal" class="hidden fixed inset-0 bg-black bg-opacity-60 flex items-center justify-center p-4 z-50 opacity-0">

&nbsp;       <div id="letter-modal-content" class="bg-white rounded-2xl shadow-2xl p-6 md:p-8 w-full max-w-md mx-auto transform opacity-0 -translate-y-4">

&nbsp;            <!-- Modal content is generated by JS -->

&nbsp;       </div>

&nbsp;   </div>

&nbsp;   

&nbsp;   <div id="onboarding-overlay" class="hidden fixed inset-0 bg-black bg-opacity-70 z-50 flex items-center justify-center p-4 opacity-0">

&nbsp;       <div id="onboarding-modal" class="bg-white rounded-lg p-8 max-w-md w-full text-center shadow-xl transform scale-95 opacity-0">

&nbsp;           <h2 class="text-2xl font-bold mb-4">Welcome to the Telugu Learning Hub!</h2>

&nbsp;           <p class="text-gray-600 mb-6">Here's a quick tour to get you started.</p>

&nbsp;           <div class="text-left space-y-4 mb-8">

&nbsp;               <p><strong>📈 Progress:</strong> Your dashboard to track mastery and streaks.</p>

&nbsp;               <p><strong>📚 Learn:</strong> Explore all letters and symbols at your own pace.</p>

&nbsp;               <p><strong>✍️ Practice:</strong> Test your knowledge with quizzes and writing practice.</p>

&nbsp;           </div>

&nbsp;           <button id="close-onboarding" class="bg-blue-600 text-white font-bold py-3 px-6 rounded-lg w-full hover:bg-blue-700 transition-transform transform hover:scale-105">Let's Go!</button>

&nbsp;       </div>

&nbsp;   </div>



&nbsp;   <!-- ===== SCRIPT LIBRARIES ===== -->

&nbsp;   <script src="https://d3js.org/d3.v7.min.js"></script>

&nbsp;   <script src="https://cdnjs.cloudflare.com/ajax/libs/tone/14.7.77/Tone.js"></script>



&nbsp;   <!-- ===== APPLICATION LOGIC ===== -->

&nbsp;   <script type="module">

&nbsp;       import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";

&nbsp;       import { getAuth, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";

&nbsp;       import { getFirestore, doc, onSnapshot, setDoc, getDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";



&nbsp;       // =================================================================================

&nbsp;       // I. APP BOOTSTRAP AND DATA

&nbsp;       // =================================================================================

&nbsp;       const AppData = {

&nbsp;           alphabet: \[

&nbsp;               // Vowels

&nbsp;               { telugu: 'అ', transliteration: 'a', type: 'vowel', example\_english: 'Amma (Mother)', writing\_path: 'M 50,75 C 60,40 90,40 100,75 C 110,110 90,120 75,100 M 100,75 C 120,60 140,60 150,75' },

&nbsp;               { telugu: 'ఆ', transliteration: 'ā', type: 'vowel', example\_english: 'Āvu (Cow)', writing\_path: 'M 50,75 C 60,40 90,40 100,75 C 110,110 90,120 75,100 M 100,75 C 120,60 140,60 150,75 M 150,50 L 150,100' },

&nbsp;               { telugu: 'ఇ', transliteration: 'i', type: 'vowel', example\_english: 'Illu (House)', writing\_path: 'M 75,50 C 60,75 60,100 75,125 M 75,125 C 90,110 110,110 125,125' },

&nbsp;               { telugu: 'ఈ', transliteration: 'ī', type: 'vowel', example\_english: 'Īga (Fly)', writing\_path: 'M 75,50 C 60,75 60,100 75,125 M 75,125 C 90,110 110,110 125,125 M 100,30 C 110,40 110,50 100,60' },

&nbsp;               { telugu: 'ఉ', transliteration: 'u', type: 'vowel', example\_english: 'Uḍuta (Squirrel)', writing\_path: 'M 50,100 C 75,50 125,50 150,100' },

&nbsp;               // Consonants

&nbsp;               { telugu: 'క', transliteration: 'ka', type: 'consonant', example\_english: 'Kalam (Pen)', writing\_path: 'M 50,100 C 75,50 125,50 150,100 M 100,50 L 100,125' },

&nbsp;               { telugu: 'ఖ', transliteration: 'kha', type: 'consonant', example\_english: 'Khaḍgaṁ (Sword)', writing\_path: 'M 60,50 C 40,75 40,100 60,125 C 80,110 100,110 120,125 C 140,100 140,75 120,50 C 100,65 80,65 60,50' },

&nbsp;               { telugu: 'గ', transliteration: 'ga', type: 'consonant', example\_english: 'Gampa (Basket)', writing\_path: 'M 125,50 L 75,125 L 150,125 M 125,50 C 140,60 140,70 125,80' },

&nbsp;               { telugu: 'ఘ', transliteration: 'gha', type: 'consonant', example\_english: 'Ghaṭaṁ (Pot)', writing\_path: 'M 60,50 C 40,75 40,100 60,125 M 60,125 C 80,110 100,110 120,125 C 140,100 140,75 120,50 M 120,50 L 120,125' },

&nbsp;               { telugu: 'చ', transliteration: 'ca', type: 'consonant', example\_english: 'Cakraṁ (Wheel)', writing\_path: 'M 150,100 C 125,50 75,50 50,100 C 75,90 125,90 150,100 M 100,50 L 100,100' },

&nbsp;               { telugu: 'జ', transliteration: 'ja', type: 'consonant', example\_english: 'Jaḍa (Braid)', writing\_path: 'M 50,75 C 75,40 125,40 150,75 C 125,120 75,120 50,75 M 100,120 L 100,75'},

&nbsp;           ],

&nbsp;           gunintalu: \[

&nbsp;               { telugu: 'క + ా = కా', transliteration: 'kā', example\_english: 'Tala-kattu-dīrghaṁ', description: 'Adds an "ā" sound.', type: 'gunintalu' },

&nbsp;               { telugu: 'క + ి = కి', transliteration: 'ki', example\_english: 'Gudi', description: 'Adds a short "i" sound.', type: 'gunintalu' },

&nbsp;               { telugu: 'క + ీ = కీ', transliteration: 'kī', example\_english: 'Gudi-dīrghaṁ', description: 'Adds a long "ī" sound.', type: 'gunintalu' },

&nbsp;               { telugu: 'క + ు = కు', transliteration: 'ku', example\_english: 'Kommu', description: 'Adds a short "u" sound.', type: 'gunintalu' },

&nbsp;               { telugu: 'క + ూ = కూ', transliteration: 'kū', example\_english: 'Kommu-dīrghaṁ', description: 'Adds a long "ū" sound.', type: 'gunintalu' },

&nbsp;               { telugu: 'క + ె = కె', transliteration: 'ke', example\_english: 'Etvaṁ', description: 'Adds a short "e" sound.', type: 'gunintalu' },

&nbsp;               { telugu: 'క + ే = కే', transliteration: 'kē', example\_english: 'Etva-dīrghaṁ', description: 'Adds a long "ē" sound.', type: 'gunintalu' },

&nbsp;               { telugu: 'క + ై = కై', transliteration: 'kai', example\_english: 'Aitvaṁ', description: 'Adds an "ai" sound.', type: 'gunintalu' },

&nbsp;           ],

&nbsp;           vottulu: \[

&nbsp;               { telugu: 'క్య', transliteration: 'kya', example\_english: 'Ya-vattu', description: 'Adds a "ya" sound.', type: 'vottulu' },

&nbsp;               { telugu: 'క్ర', transliteration: 'kra', example\_english: 'Ra-vattu', description: 'Adds a "ra" sound.', type: 'vottulu' },

&nbsp;               { telugu: 'క్ల', transliteration: 'kla', example\_english: 'La-vattu', description: 'Adds a "la" sound.', type: 'vottulu' },

&nbsp;               { telugu: 'క్వ', transliteration: 'kva', example\_english: 'Va-vattu', description: 'Adds a "va" sound.', type: 'vottulu' },

&nbsp;               { telugu: 'క్క', transliteration: 'kka', example\_english: 'Ka-vattu', description: 'Doubles the consonant sound.', type: 'vottulu' },

&nbsp;               { telugu: 'గ్గ', transliteration: 'gga', example\_english: 'Ga-vattu', description: 'Doubles the consonant sound.', type: 'vottulu' },

&nbsp;           ],

&nbsp;           achievements: {

&nbsp;               vowelVirtuoso: { title: "Vowel Virtuoso", desc: "Master all vowels", icon: "🎓", unlocked: false, type: 'alphabet'},

&nbsp;               consonantChamp: { title: "Consonant Champ", desc: "Master all consonants", icon: "🏆", unlocked: false, type: 'alphabet' },

&nbsp;               gunintaluGuru: { title: "Gunintalu Guru", desc: "Master all vowel combinations", icon: "🎨", unlocked: false, type: 'gunintalu'},

&nbsp;               vottuluVictor: { title: "Vottulu Victor", desc: "Master all consonant conjuncts", icon: "🧩", unlocked: false, type: 'vottulu'},

&nbsp;               streakStarter: { title: "Streak Starter", desc: "Maintain a 3-day streak", icon: "🔥", unlocked: false, type: 'streak'},

&nbsp;               perfectPractice: { title: "Perfect Practice", desc: "Get 10 quiz questions right in a row", icon: "🎯", unlocked: false, type: 'practice'},

&nbsp;           }

&nbsp;       };



&nbsp;       let appState = null;

&nbsp;       let firebaseService, ui, audio;



&nbsp;       async function main() {

&nbsp;           try {

&nbsp;               firebaseService = await FirebaseService.init();

&nbsp;               audio = AudioController.init();

&nbsp;               

&nbsp;               firebaseService.onUserStateChange(state => {

&nbsp;                   appState = state;

&nbsp;                   ui = UIController.init(appState, audio, firebaseService);

&nbsp;                   

&nbsp;                   ProgressModule.render(appState);

&nbsp;                   LearnModule.render(appState);

&nbsp;                   PracticeModule.render(appState, firebaseService, audio);

&nbsp;                   

&nbsp;                   ui.navigateTo('progress'); 

&nbsp;                   Onboarding.init(appState, firebaseService);



&nbsp;                   document.getElementById('app-loader').style.opacity = '0';

&nbsp;                   setTimeout(() => {

&nbsp;                       document.getElementById('app-loader').style.display = 'none';

&nbsp;                       document.getElementById('app').style.opacity = '1';

&nbsp;                   }, 500);

&nbsp;               });



&nbsp;           } catch (error) {

&nbsp;               console.error("Firebase initialization failed:", error);

&nbsp;               // FIX: Add specific error handling for invalid API key.

&nbsp;               let errorMessage = '<p class="text-red-500">Error: Could not connect to the service. Please refresh.</p>';

&nbsp;               if (error.message \&\& error.message.includes('api-key-not-valid')) {

&nbsp;                   errorMessage = `

&nbsp;                       <div class="text-center p-4 bg-red-50 border border-red-200 rounded-lg">

&nbsp;                           <h3 class="font-bold text-lg text-red-700">Configuration Error</h3>

&nbsp;                           <p class="text-red-600 mt-2">Your Firebase API key is missing or invalid.</p>

&nbsp;                           <p class="text-gray-700 mt-2">

&nbsp;                               Please follow the instructions from the Launch Kit to create a Firebase project, then copy and paste your unique <code class="bg-gray-200 text-sm p-1 rounded">firebaseConfig</code> object into the <strong>index.html</strong> file.

&nbsp;                           </p>

&nbsp;                           <p class="text-gray-500 text-sm mt-4">The app cannot start without a valid configuration.</p>

&nbsp;                       </div>

&nbsp;                   `;

&nbsp;               }

&nbsp;               document.getElementById('app-loader').innerHTML = errorMessage;

&nbsp;           }

&nbsp;       }

&nbsp;       

&nbsp;       // =================================================================================

&nbsp;       // II. FIREBASE SERVICE

&nbsp;       // =================================================================================

&nbsp;       const FirebaseService = (() => {

&nbsp;           let auth, db, userId, userDocRef;

&nbsp;           let onStateChangeCallback = null;

&nbsp;           

&nbsp;           async function init() {

&nbsp;               // IMPORTANT: PASTE YOUR FIREBASE CONFIG OBJECT HERE

&nbsp;               const firebaseConfig = {

&nbsp;                 apiKey: "AIzaSyCPGHcWevP9edJzROksfXNEMDWOAhxwKPA",

&nbsp;                 authDomain: "learn-telegu.firebaseapp.com",

&nbsp;                 projectId: "learn-telegu",

&nbsp;                 storageBucket: "learn-telegu.firebasestorage.app",

&nbsp;                 messagingSenderId: "1081028550840",

&nbsp;                 appId: "1:1081028550840:web:772516df0ab0d48652544d",

&nbsp;                 measurementId: "G-6XYDD9FEER"

&nbsp;               };

&nbsp;               

&nbsp;               const app = initializeApp(firebaseConfig);

&nbsp;               auth = getAuth(app);

&nbsp;               db = getFirestore(app);



&nbsp;               return new Promise((resolve, reject) => {

&nbsp;                   onAuthStateChanged(auth, async user => {

&nbsp;                       if (user) {

&nbsp;                           userId = user.uid;

&nbsp;                           const appId = "telugu-learning-hub"; // A unique ID for your app

&nbsp;                           userDocRef = doc(db, `artifacts/${appId}/users/${userId}`);

&nbsp;                           

&nbsp;                           document.getElementById('user-status').textContent = `User ID: ${userId.substring(0,8)}...`;

&nbsp;                           

&nbsp;                           const docSnap = await getDoc(userDocRef);

&nbsp;                           if (!docSnap.exists()) {

&nbsp;                               const defaultState = getNewUserState();

&nbsp;                               await setDoc(userDocRef, defaultState);

&nbsp;                           }



&nbsp;                           onSnapshot(userDocRef, (doc) => {

&nbsp;                               if (onStateChangeCallback) onStateChangeCallback(doc.data());

&nbsp;                           });

&nbsp;                           

&nbsp;                           resolve(this);

&nbsp;                       }

&nbsp;                   });



&nbsp;                   signInAnonymously(auth).catch(reject);

&nbsp;               });

&nbsp;           }



&nbsp;           function getNewUserState() {

&nbsp;               return {

&nbsp;                   letterStates: {},

&nbsp;                   lastVisit: new Date().toISOString().split('T')\[0],

&nbsp;                   streak: 1,

&nbsp;                   achievements: AppData.achievements,

&nbsp;                   onboardingComplete: false,

&nbsp;                   quizStats: {

&nbsp;                       correctInARow: 0,

&nbsp;                       totalCorrect: 0,

&nbsp;                       totalAnswered: 0

&nbsp;                   }

&nbsp;               };

&nbsp;           }

&nbsp;           

&nbsp;           async function updateState(updates) {

&nbsp;               if (!userDocRef) return;

&nbsp;               try {

&nbsp;                   await setDoc(userDocRef, updates, { merge: true });

&nbsp;               } catch (error) {

&nbsp;                   console.error("Error updating user state:", error);

&nbsp;               }

&nbsp;           }



&nbsp;           return {

&nbsp;               init,

&nbsp;               onUserStateChange: (callback) => { onStateChangeCallback = callback; },

&nbsp;               update: updateState,

&nbsp;               setConfidence: (key, status) => updateState({ \[`letterStates.${key}`]: status }),

&nbsp;               completeOnboarding: () => updateState({ onboardingComplete: true }),

&nbsp;           };

&nbsp;       })();



&nbsp;       // =================================================================================

&nbsp;       // III. GLOBAL UI CONTROLLER

&nbsp;       // =================================================================================

&nbsp;       const UIController = (() => {

&nbsp;           let state, audio, firebase;

&nbsp;           const views = document.querySelectorAll('.view');

&nbsp;           const nav = document.getElementById('main-nav');

&nbsp;           const letterModal = document.getElementById('letter-modal');

&nbsp;           const letterModalContent = document.getElementById('letter-modal-content');



&nbsp;           function init(appState, audioController, firebaseService) {

&nbsp;               state = appState;

&nbsp;               audio = audioController;

&nbsp;               firebase = firebaseService;

&nbsp;               nav.addEventListener('click', handleNav);

&nbsp;               letterModal.addEventListener('click', (e) => {

&nbsp;                   if (e.target === letterModal) hideLetterModal();

&nbsp;               });

&nbsp;               document.getElementById('download-btn').addEventListener('click', () => {

&nbsp;                   const blob = new Blob(\[document.documentElement.outerHTML], { type: 'text/html' });

&nbsp;                   const a = document.createElement('a');

&nbsp;                   a.href = URL.createObjectURL(blob);

&nbsp;                   a.download = 'telugu-learning-hub.html';

&nbsp;                   a.click();

&nbsp;               });

&nbsp;               return this;

&nbsp;           }



&nbsp;           function handleNav(e) {

&nbsp;               if (e.target.matches('\[data-view]')) {

&nbsp;                   navigateTo(e.target.dataset.view);

&nbsp;               }

&nbsp;           }

&nbsp;           

&nbsp;           function navigateTo(viewId) {

&nbsp;               views.forEach(v => v.classList.remove('active'));

&nbsp;               document.getElementById(`${viewId}-view`).classList.add('active');

&nbsp;               

&nbsp;               nav.querySelectorAll('.tab-btn').forEach(btn => {

&nbsp;                   btn.classList.toggle('active', btn.dataset.view === viewId);

&nbsp;               });



&nbsp;               if (viewId === 'learn') {

&nbsp;                   const learnView = document.getElementById('learn-view');

&nbsp;                   const activeSubTab = learnView.querySelector('.sub-tab-btn.active')?.dataset.learnView || 'alphabet';

&nbsp;                   LearnModule.render(state, activeSubTab);

&nbsp;               } else if (viewId === 'practice') {

&nbsp;                   PracticeModule.render(state, firebase, audio);

&nbsp;               } else if (viewId === 'progress') {

&nbsp;                   ProgressModule.render(state);

&nbsp;               }

&nbsp;           }



&nbsp;           function showLetterModal(item, itemKey) {

&nbsp;               const currentStatus = state.letterStates\[itemKey] || 'none';

&nbsp;               

&nbsp;               letterModalContent.innerHTML = `

&nbsp;                   <div class="flex justify-between items-start">

&nbsp;                       <div class="flex items-center gap-4">

&nbsp;                           <div>

&nbsp;                               <h3 class="text-5xl telugu-char font-bold">${item.telugu}</h3>

&nbsp;                               <p class="text-xl text-gray-600 font-semibold">${item.transliteration}</p>

&nbsp;                           </div>

&nbsp;                           <button id="play-audio-btn" class="text-blue-500 hover:text-blue-700 p-2 rounded-full hover:bg-blue-100 transition-colors" aria-label="Listen to pronunciation">

&nbsp;                               <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.536 8.464a5 5 0 010 7.072m2.828-9.9a9 9 0 010 12.728M5.858 8.464a5 5 0 000 7.072m2.828 9.9a9 9 0 000-12.728M12 12h.01" /></svg>

&nbsp;                           </button>

&nbsp;                       </div>

&nbsp;                       <button id="close-modal-btn" class="text-gray-400 hover:text-gray-700">

&nbsp;                           <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" /></svg>

&nbsp;                       </button>

&nbsp;                   </div>

&nbsp;                   <div class="my-6 text-center">

&nbsp;                       <p class="text-gray-800"><strong>Example:</strong> ${item.example\_english}</p>

&nbsp;                       <p class="text-gray-600">${item.description || ''}</p>

&nbsp;                   </div>

&nbsp;                   <div class="mb-6 h-48 w-full bg-gray-100 rounded-lg" id="writing-animation-container"></div>

&nbsp;                   <div class="grid grid-cols-3 gap-2 text-center">

&nbsp;                       <button data-status="not-sure" class="confidence-btn p-2 rounded-lg ${currentStatus === 'not-sure' ? 'ring-2 ring-red-500 bg-red-100' : 'bg-gray-100'}">Not Sure</button>

&nbsp;                       <button data-status="getting-there" class="confidence-btn p-2 rounded-lg ${currentStatus === 'getting-there' ? 'ring-2 ring-amber-500 bg-amber-100' : 'bg-gray-100'}">Getting There</button>

&nbsp;                       <button data-status="confident" class="confidence-btn p-2 rounded-lg ${currentStatus === 'confident' ? 'ring-2 ring-green-500 bg-green-100' : 'bg-gray-100'}">Confident</button>

&nbsp;                   </div>

&nbsp;               `;



&nbsp;               letterModal.classList.remove('hidden');

&nbsp;               setTimeout(() => {

&nbsp;                   letterModal.classList.remove('opacity-0');

&nbsp;                   letterModalContent.classList.remove('opacity-0', '-translate-y-4');

&nbsp;               }, 10);

&nbsp;               

&nbsp;               if (item.writing\_path) {

&nbsp;                   animateWriting(item.writing\_path);

&nbsp;               }



&nbsp;               letterModalContent.querySelector('#close-modal-btn').onclick = hideLetterModal;

&nbsp;               letterModalContent.querySelector('#play-audio-btn').onclick = () => {

&nbsp;                   audio.speak(item.telugu.split('=')\[1]?.trim() || item.telugu, 'te-IN');

&nbsp;               };

&nbsp;               letterModalContent.querySelectorAll('.confidence-btn').forEach(btn => {

&nbsp;                   btn.onclick = () => {

&nbsp;                       firebase.setConfidence(itemKey, btn.dataset.status);

&nbsp;                       audio.vibrate();

&nbsp;                       hideLetterModal();

&nbsp;                   };

&nbsp;               });

&nbsp;           }



&nbsp;           function hideLetterModal() {

&nbsp;               letterModal.classList.add('opacity-0');

&nbsp;               letterModalContent.classList.add('opacity-0', '-translate-y-4');

&nbsp;               setTimeout(() => letterModal.classList.add('hidden'), 300);

&nbsp;           }



&nbsp;           function animateWriting(pathData) {

&nbsp;               const container = d3.select("#writing-animation-container");

&nbsp;               container.html(""); // Clear previous

&nbsp;               // FIX: Make SVG responsive and centered within its container

&nbsp;               const svg = container.append("svg")

&nbsp;                   .attr("width", "100%")

&nbsp;                   .attr("height", "100%")

&nbsp;                   .attr("viewBox", "0 0 200 150")

&nbsp;                   .attr("preserveAspectRatio", "xMidYMid meet");

&nbsp;               

&nbsp;               const path = svg.append("path")

&nbsp;                   .attr("d", pathData)

&nbsp;                   .attr("fill", "none")

&nbsp;                   .attr("stroke", "var(--primary-color)")

&nbsp;                   .attr("stroke-width", 8)

&nbsp;                   .attr("stroke-linecap", "round");

&nbsp;               const totalLength = path.node().getTotalLength();

&nbsp;               path.attr("stroke-dasharray", totalLength + " " + totalLength)

&nbsp;                   .attr("stroke-dashoffset", totalLength)

&nbsp;                   .transition().duration(2000).ease(d3.easeLinear)

&nbsp;                   .attr("stroke-dashoffset", 0);

&nbsp;           }



&nbsp;           return { init, navigateTo, showLetterModal };

&nbsp;       })();

&nbsp;       

&nbsp;       // =================================================================================

&nbsp;       // IV. FEATURE MODULES

&nbsp;       // =================================================================================



&nbsp;       const LearnModule = {

&nbsp;           render(state, subView = 'alphabet') {

&nbsp;               const learnView = document.getElementById('learn-view');

&nbsp;               learnView.innerHTML = `

&nbsp;                   <div id="learn-sub-nav" class="flex justify-center mb-6 bg-gray-200 rounded-lg p-1">

&nbsp;                       <button data-learn-view="alphabet" class="sub-tab-btn font-semibold py-2 px-4 rounded-md w-1/3 ${subView === 'alphabet' ? 'active' : ''}">Alphabet</button>

&nbsp;                       <button data-learn-view="gunintalu" class="sub-tab-btn font-semibold py-2 px-4 rounded-md w-1/3 ${subView === 'gunintalu' ? 'active' : ''}">Gunintalu</button>

&nbsp;                       <button data-learn-view="vottulu" class="sub-tab-btn font-semibold py-2 px-4 rounded-md w-1/3 ${subView === 'vottulu' ? 'active' : ''}">Vottulu</button>

&nbsp;                   </div>

&nbsp;                   <div id="learn-grid" class="grid grid-cols-4 sm:grid-cols-6 md:grid-cols-8 gap-3"></div>

&nbsp;               `;

&nbsp;               

&nbsp;               const dataSet = AppData\[subView] || AppData.alphabet;

&nbsp;               const grid = document.getElementById('learn-grid');

&nbsp;               grid.innerHTML = dataSet.map(item => {

&nbsp;                   const itemKey = `${item.type}\_${item.transliteration}`;

&nbsp;                   const status = state.letterStates\[itemKey] || 'none';

&nbsp;                   const displayChar = item.type === 'gunintalu' ? item.telugu.split('=')\[1].trim() : (item.type === 'vottulu' ? item.telugu : item.telugu);

&nbsp;                   return `

&nbsp;                       <div data-item-key="${itemKey}" class="item-card status-indicator status-${status} bg-white rounded-lg shadow-sm hover:shadow-lg hover:-translate-y-1 transition-all cursor-pointer p-2 flex flex-col items-center justify-center aspect-square">

&nbsp;                           <span class="text-3xl md:text-4xl telugu-char">${displayChar}</span>

&nbsp;                           <span class="text-xs text-gray-500">${item.transliteration}</span>

&nbsp;                       </div>

&nbsp;                   `;

&nbsp;               }).join('');

&nbsp;               

&nbsp;               learnView.querySelector('#learn-sub-nav').addEventListener('click', (e) => {

&nbsp;                   if (e.target.matches('\[data-learn-view]')) {

&nbsp;                       this.render(state, e.target.dataset.learnView);

&nbsp;                   }

&nbsp;               });



&nbsp;               grid.addEventListener('click', (e) => {

&nbsp;                   const card = e.target.closest('.item-card');

&nbsp;                   if (card) {

&nbsp;                       const key = card.dataset.itemKey;

&nbsp;                       const \[type, transliteration] = key.split('\_');

&nbsp;                       let dataSetKey = type;

&nbsp;                       if (type === 'vowel' || type === 'consonant') {

&nbsp;                           dataSetKey = 'alphabet';

&nbsp;                       }

&nbsp;                       const itemData = AppData\[dataSetKey].find(i => i.transliteration === transliteration);

&nbsp;                       if (itemData) {

&nbsp;                           ui.showLetterModal(itemData, key);

&nbsp;                       }

&nbsp;                   }

&nbsp;               });

&nbsp;           }

&nbsp;       };



&nbsp;       const ProgressModule = {

&nbsp;           render(state) {

&nbsp;               const progressView = document.getElementById('progress-view');



&nbsp;               const calcProgress = (type) => {

&nbsp;                   const items = AppData\[type];

&nbsp;                   const total = items.length;

&nbsp;                   if (total === 0) return { percent: 0, confident: 0, gettingThere: 0, notSure: 0, total: 0 };

&nbsp;                   

&nbsp;                   let confident = 0, gettingThere = 0, notSure = 0;

&nbsp;                   items.forEach(item => {

&nbsp;                       const key = `${item.type}\_${item.transliteration}`;

&nbsp;                       const status = state.letterStates\[key];

&nbsp;                       if (status === 'confident') confident++;

&nbsp;                       else if (status === 'getting-there') gettingThere++;

&nbsp;                       else if (status === 'not-sure') notSure++;

&nbsp;                   });

&nbsp;                   const percent = total > 0 ? Math.round(((confident + gettingThere \* 0.5) / total) \* 100) : 0;

&nbsp;                   return { percent, confident, gettingThere, notSure, total };

&nbsp;               };

&nbsp;               

&nbsp;               const alphabetProgress = calcProgress('alphabet');

&nbsp;               const gunintaluProgress = calcProgress('gunintalu');

&nbsp;               const vottuluProgress = calcProgress('vottulu');



&nbsp;               progressView.innerHTML = `

&nbsp;               <div class="grid grid-cols-1 md:grid-cols-2 gap-6">

&nbsp;                   <div class="bg-white p-6 rounded-xl shadow-md">

&nbsp;                       <h3 class="font-bold text-xl mb-4">Learning Progress</h3>

&nbsp;                       ${createProgressBar('Alphabet', alphabetProgress)}

&nbsp;                       ${createProgressBar('Gunintalu (Vowel Signs)', gunintaluProgress)}

&nbsp;                       ${createProgressBar('Vottulu (Conjuncts)', vottuluProgress)}

&nbsp;                   </div>

&nbsp;                   <div class="bg-white p-6 rounded-xl shadow-md">

&nbsp;                       <h3 class="font-bold text-xl mb-4">Achievements</h3>

&nbsp;                       <div class="grid grid-cols-2 sm:grid-cols-3 gap-4">

&nbsp;                           ${Object.values(state.achievements).map(ach => `

&nbsp;                               <div class="achievement ${ach.unlocked ? 'unlocked' : ''} text-center p-2">

&nbsp;                                   <div class="text-4xl">${ach.icon}</div>

&nbsp;                                   <p class="font-semibold text-sm mt-1">${ach.title}</p>

&nbsp;                                   <p class="text-xs text-gray-500">${ach.desc}</p>

&nbsp;                               </div>

&nbsp;                           `).join('')}

&nbsp;                       </div>

&nbsp;                   </div>

&nbsp;               </div>

&nbsp;               `;



&nbsp;               function createProgressBar(title, progressData) {

&nbsp;                   return `

&nbsp;                   <div class="mb-4">

&nbsp;                       <div class="flex justify-between items-end mb-1">

&nbsp;                           <p class="font-semibold">${title}</p>

&nbsp;                           <p class="text-sm font-bold text-blue-600">${progressData.percent}% Mastered</p>

&nbsp;                       </div>

&nbsp;                       <div class="w-full bg-gray-200 rounded-full h-4 overflow-hidden flex">

&nbsp;                           <div class="bg-green-500 h-4" style="width: ${progressData.total > 0 ? (progressData.confident/progressData.total)\*100 : 0}%"></div>

&nbsp;                           <div class="bg-amber-500 h-4" style="width: ${progressData.total > 0 ? (progressData.gettingThere/progressData.total)\*100 : 0}%"></div>

&nbsp;                           <div class="bg-red-500 h-4" style="width: ${progressData.total > 0 ? (progressData.notSure/progressData.total)\*100 : 0}%"></div>

&nbsp;                       </div>

&nbsp;                   </div>

&nbsp;                   `;

&nbsp;               }

&nbsp;           }

&nbsp;       };

&nbsp;       

&nbsp;       const PracticeModule = {

&nbsp;           // A simplified placeholder for brevity. The full logic would be here.

&nbsp;           render(state, firebase, audio) {

&nbsp;               const practiceView = document.getElementById('practice-view');

&nbsp;               practiceView.innerHTML = `

&nbsp;                   <div class="bg-white p-6 rounded-xl shadow-md">

&nbsp;                       <h3 class="font-bold text-xl mb-4">Practice Zone</h3>

&nbsp;                       <p class="text-gray-600">The interactive quiz and writing pad would be here. This is a placeholder to demonstrate the app structure.</p>

&nbsp;                       <div class="mt-4 p-8 bg-gray-100 rounded-lg text-center">

&nbsp;                           <span class="text-6xl telugu-char">క</span>

&nbsp;                           <p class="mt-2">Quiz and Writing Pad coming soon!</p>

&nbsp;                       </div>

&nbsp;                   </div>

&nbsp;               `;

&nbsp;           }

&nbsp;       };

&nbsp;       

&nbsp;       const AudioController = {

&nbsp;           voices: \[],

&nbsp;           isReady: false,

&nbsp;           init() {

&nbsp;               if ('speechSynthesis' in window) {

&nbsp;                   this.loadVoices(); // Initial attempt



&nbsp;                   if (this.voices.length === 0) {

&nbsp;                       window.speechSynthesis.onvoiceschanged = () => {

&nbsp;                           this.loadVoices();

&nbsp;                       };

&nbsp;                       

&nbsp;                       // Fallback interval for browsers that don't fire onvoiceschanged reliably

&nbsp;                       let voiceCheckInterval = setInterval(() => {

&nbsp;                           this.loadVoices();

&nbsp;                           if (this.isReady) {

&nbsp;                               clearInterval(voiceCheckInterval);

&nbsp;                           }

&nbsp;                       }, 250);



&nbsp;                       // Stop trying after 2 seconds

&nbsp;                       setTimeout(() => clearInterval(voiceCheckInterval), 2000);

&nbsp;                   }

&nbsp;               }



&nbsp;               document.body.addEventListener('click', () => Tone.start(), { once: true });

&nbsp;               return this;

&nbsp;           },

&nbsp;           loadVoices() {

&nbsp;               const loadedVoices = window.speechSynthesis.getVoices();

&nbsp;               if (loadedVoices.length > 0) {

&nbsp;                   this.voices = loadedVoices;

&nbsp;                   this.isReady = true;

&nbsp;               }

&nbsp;           },

&nbsp;           vibrate() {

&nbsp;               if (navigator.vibrate) {

&nbsp;                   navigator.vibrate(50);

&nbsp;               }

&nbsp;           },

&nbsp;           speak(text, lang) {

&nbsp;               if (!('speechSynthesis' in window)) {

&nbsp;                   console.warn("Text-to-speech not supported.");

&nbsp;                   return;

&nbsp;               }

&nbsp;               

&nbsp;               if (!this.isReady) {

&nbsp;                   this.loadVoices(); // Final attempt to load voices

&nbsp;               }



&nbsp;               const utterance = new SpeechSynthesisUtterance(text);

&nbsp;               utterance.lang = lang;

&nbsp;               utterance.rate = 0.8;



&nbsp;               const teluguVoice = this.voices.find(voice => voice.lang === 'te-IN');

&nbsp;               if (teluguVoice) {

&nbsp;                   utterance.voice = teluguVoice;

&nbsp;               } else {

&nbsp;                   console.warn('Telugu (te-IN) voice not found. Using browser default.');

&nbsp;               }

&nbsp;               

&nbsp;               window.speechSynthesis.cancel();

&nbsp;               // A tiny delay helps prevent race conditions on some browsers

&nbsp;               setTimeout(() => {

&nbsp;                   window.speechSynthesis.speak(utterance);

&nbsp;               }, 50);

&nbsp;           },

&nbsp;           play(sound) {

&nbsp;               // Simplified audio logic

&nbsp;           }

&nbsp;       };



&nbsp;       const Onboarding = {

&nbsp;           init(state, firebase) {

&nbsp;               if (!state.onboardingComplete) {

&nbsp;                   const overlay = document.getElementById('onboarding-overlay');

&nbsp;                   const modal = document.getElementById('onboarding-modal');

&nbsp;                   const closeBtn = document.getElementById('close-onboarding');



&nbsp;                   overlay.classList.remove('hidden');

&nbsp;                    setTimeout(() => {

&nbsp;                       overlay.classList.remove('opacity-0');

&nbsp;                       modal.classList.remove('opacity-0', 'scale-95');

&nbsp;                   }, 10);



&nbsp;                   closeBtn.onclick = () => {

&nbsp;                       firebase.completeOnboarding();

&nbsp;                       overlay.classList.add('opacity-0');

&nbsp;                       modal.classList.add('opacity-0', 'scale-95');

&nbsp;                       setTimeout(() => overlay.classList.add('hidden'), 300);

&nbsp;                   };

&nbsp;               }

&nbsp;           }

&nbsp;       };



&nbsp;       main();



&nbsp;   </script>

</body>

</html>















