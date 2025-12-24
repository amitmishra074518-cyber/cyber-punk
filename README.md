
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Mishra Archives | History Unearthed</title>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700;900&family=Lato:wght@300;400;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-dark: #0a0a0a;
            --bg-panel: rgba(255, 255, 255, 0.05);
            --gold-gradient: linear-gradient(45deg, #bf953f, #fcf6ba, #b38728, #fbf5b7, #aa771c);
            --font-head: 'Cinzel', serif;
            --font-body: 'Lato', sans-serif;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        body {
            background-color: var(--bg-dark);
            color: #e0e0e0;
            font-family: var(--font-body);
            overflow-x: hidden;
            min-height: 100vh;
        }

        /* --- Animations --- */
        @keyframes slideUp {
            from { opacity: 0; transform: translateY(40px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .fade-in { animation: slideUp 0.6s ease-out forwards; }

        /* --- Navigation --- */
        nav {
            position: fixed;
            top: 0; width: 100%;
            padding: 20px 50px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 100;
            background: rgba(0, 0, 0, 0.9);
            border-bottom: 1px solid rgba(191, 149, 63, 0.2);
        }

        .logo { 
            font-family: var(--font-head);
            font-weight: 700;
            font-size: 1.5rem; 
            background: var(--gold-gradient);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            cursor: pointer;
        }

        .nav-links button {
            background: none; border: none; color: #fff;
            margin-left: 30px; text-transform: uppercase;
            font-size: 0.8rem; letter-spacing: 2px; cursor: pointer;
            transition: color 0.3s; font-family: var(--font-body);
        }
        .nav-links button:hover { color: #bf953f; }

        /* --- SECTIONS --- */
        .page-section {
            min-height: 100vh; width: 100%;
            padding-top: 100px;
            display: none; /* Hidden by default */
            flex-direction: column; align-items: center;
        }

        .page-section.active { display: flex; }

        /* --- HOME --- */
        #home {
            justify-content: center; text-align: center;
            background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.9)), url('https://images.unsplash.com/photo-1461360370896-922624d12aa1?q=80&w=2074&auto=format&fit=crop') no-repeat center center/cover;
            padding-top: 0;
        }
        #home h1 { font-size: 4rem; font-family: var(--font-head); background: var(--gold-gradient); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        
        .btn-gold {
            padding: 15px 40px; background: var(--gold-gradient); color: #000;
            border: none; font-weight: bold; text-transform: uppercase;
            letter-spacing: 2px; cursor: pointer; transition: 0.3s; margin-top: 20px;
        }
        .btn-gold:hover { transform: scale(1.05); box-shadow: 0 0 20px rgba(191, 149, 63, 0.5); }

        /* --- TIMELINE GRID --- */
        .grid {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px; width: 85%; max-width: 1200px; margin-top: 40px; padding-bottom: 50px;
        }
        .card {
            background: var(--bg-panel); padding: 40px 30px;
            border: 1px solid rgba(255,255,255,0.1); transition: 0.3s; cursor: pointer;
        }
        .card:hover { border-color: #bf953f; transform: translateY(-5px); background: rgba(255,255,255,0.08); }
        .card h3 { color: #bf953f; font-family: var(--font-head); margin-bottom: 10px; }

        /* --- ERA DETAIL VIEWER (The New Content Section) --- */
        #era-viewer { padding: 100px 10%; align-items: flex-start; }
        
        .back-btn {
            background: none; border: 1px solid #bf953f; color: #bf953f;
            padding: 10px 20px; cursor: pointer; margin-bottom: 30px;
            text-transform: uppercase; font-size: 0.8rem; letter-spacing: 2px;
            transition: 0.3s;
        }
        .back-btn:hover { background: #bf953f; color: #000; }

        #era-image {
            width: 100%; height: 300px; object-fit: cover;
            border-bottom: 3px solid #bf953f; margin-bottom: 40px;
            opacity: 0.8;
        }

        #era-title { font-size: 3rem; font-family: var(--font-head); color: #fff; margin-bottom: 20px; }
        #era-text { font-size: 1.1rem; line-height: 1.8; color: #ccc; max-width: 800px; white-space: pre-line; }

        /* --- PRELOADER --- */
        #preloader {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: #000; z-index: 9999; display: flex;
            justify-content: center; align-items: center; flex-direction: column;
            transition: opacity 0.8s ease;
        }
        .loader-ring {
            width: 80px; height: 80px; border: 4px solid transparent;
            border-top: 4px solid #bf953f; border-radius: 50%;
            animation: spin 1s linear infinite;
        }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

        @media (max-width: 768px) {
            #home h1 { font-size: 2.5rem; }
            .nav-links { display: none; }
        }
    </style>
</head>
<body>

    <div id="preloader">
        <div class="loader-ring"></div>
        <div style="margin-top: 20px; color: #bf953f; font-family: 'Cinzel';">Loading Archives...</div>
    </div>

    <nav>
        <div class="logo" onclick="showSection('home')">THE MISHRA ARCHIVES</div>
        <div class="nav-links">
            <button onclick="showSection('home')">Home</button>
            <button onclick="showSection('about')">About Amit</button>
            <button onclick="showSection('timeline')">Timeline</button>
        </div>
    </nav>

    <section id="home" class="page-section active fade-in">
        <div>
            <h1>History Unearthed</h1>
            <p style="color: #ccc; margin-bottom: 30px; letter-spacing: 1px;">The Collected Works of Amit Mishra</p>
            <button class="btn-gold" onclick="showSection('timeline')">Enter The Archives</button>
        </div>
    </section>

    <section id="about" class="page-section">
        <div class="fade-in" style="background: var(--bg-panel); padding: 50px; border: 1px solid #bf953f; max-width: 800px; text-align: center;">
            <h2 style="font-family: 'Cinzel'; color: #bf953f; font-size: 2.5rem; margin-bottom: 20px;">The Curator</h2>
            <p style="line-height: 1.8; color: #ccc;">
                Amit Mishra has dedicated years to curating the most significant events of human civilization. This archive is an attempt to bridge the gap between academic history and modern storytelling.
            </p>
        </div>
    </section>

    <section id="timeline" class="page-section">
        <h2 style="font-family: 'Cinzel'; color: #fff; font-size: 2.5rem;">Select an Era</h2>
        <div class="grid fade-in">
            <div class="card" onclick="openEra('antiquity')">
                <h3>01. Antiquity</h3>
                <p>The cradle of civilization. Sumer, Egypt, and the Indus Valley.</p>
            </div>
            <div class="card" onclick="openEra('classical')">
                <h3>02. Classical Age</h3>
                <p>The rise of Greece, Rome, and the great philosophies.</p>
            </div>
            <div class="card" onclick="openEra('medieval')">
                <h3>03. Middle Ages</h3>
                <p>Knights, Caliphates, and the shifting borders of faith.</p>
            </div>
            <div class="card" onclick="openEra('discovery')">
                <h3>04. Age of Discovery</h3>
                <p>The rebirth of art, science, and global exploration.</p>
            </div>
            <div class="card" onclick="openEra('industry')">
                <h3>05. Industry</h3>
                <p>Steam power, factories, and the age of machines.</p>
            </div>
            <div class="card" onclick="openEra('modern')">
                <h3>06. Modern Era</h3>
                <p>The atomic age, cold wars, and the digital revolution.</p>
            </div>
        </div>
    </section>

    <section id="era-viewer" class="page-section">
        <button class="back-btn" onclick="showSection('timeline')">← Back to Timeline</button>
        
        <img id="era-image" src="" alt="Historical Era">
        <h1 id="era-title">Era Title</h1>
        <div id="era-text">Era description goes here...</div>
    </section>

    <script>
        // --- 1. THE DATA (Content for Amit's Website) ---
        const eraContent = {
            'antiquity': {
                title: "Antiquity & The Dawn",
                img: "https://images.unsplash.com/photo-1599739376686-35d5a7b0ebc3?q=80&w=1976&auto=format&fit=crop", // Pyramids
                text: "The story of humanity begins here.\n\nFrom the fertile crescent of Mesopotamia to the banks of the Nile and the Indus Valley, this era marks the transition from hunter-gatherers to city-builders.\n\nWe explore the Code of Hammurabi, the construction of the Great Pyramids, and the mysterious disappearance of the Harappan civilization. It is a time of god-kings, the invention of writing, and the first wheel turning in the dust of Sumer."
            },
            'classical': {
                title: "The Classical Empires",
                img: "https://images.unsplash.com/photo-1555661530-68c8e23336c9?q=80&w=2001&auto=format&fit=crop", // Rome/Greece
                text: "The foundations of the modern Western world were laid in marble.\n\nIn Greece, democracy and philosophy flourished under the likes of Socrates and Plato. In Rome, a Republic transformed into an Empire that spanned continents. Meanwhile, in the East, the Han Dynasty solidified the identity of China.\n\nThis section covers the Punic Wars, the rise of Christianity, and the eventual fall of Rome that plunged Europe into chaos."
            },
            'medieval': {
                title: "The Middle Ages",
                img: "https://images.unsplash.com/photo-1599725427295-58476f924e23?q=80&w=2070&auto=format&fit=crop", // Castles/Europe
                text: "Often called the 'Dark Ages,' this was actually a time of immense transformation.\n\nWhile Europe fractured into feudal kingdoms defined by knights and castles, the Islamic Golden Age brought advances in mathematics, medicine, and astronomy. The Silk Road connected the East and West, bringing goods—and the Black Death.\n\nWe analyze the Crusades, the Mongol conquests of Genghis Khan, and the Magna Carta."
            },
            'discovery': {
                title: "Renaissance & Discovery",
                img: "https://images.unsplash.com/photo-1544256273-026c48325a7a?q=80&w=1964&auto=format&fit=crop", // Art/Map
                text: "Humanity awakens.\n\nThe Renaissance brought a revival of art and science in Italy, with Da Vinci and Michelangelo challenging the status quo. Simultaneously, the Age of Exploration saw ships sailing into the unknown.\n\nColumbus reached the Americas, triggering the Columbian Exchange that altered global diets and populations forever. Empires like Spain and Portugal divided the world between them."
            },
            'industry': {
                title: "The Industrial Revolution",
                img: "https://images.unsplash.com/photo-1505567745926-ba89000d255a?q=80&w=2071&auto=format&fit=crop", // Train/Industry
                text: "The world gets faster.\n\nBeginning in Britain, the steam engine revolutionized how we work, travel, and live. Agrarian societies transformed into urban powerhouses. \n\nThis era covers the rise of factories, the American Civil War, the colonization of Africa, and the social upheavals that led to the demand for workers' rights."
            },
            'modern': {
                title: "The Modern Era",
                img: "https://images.unsplash.com/photo-1526304640152-d4619684e484?q=80&w=2070&auto=format&fit=crop", // Modern City/Tech
                text: "The century of total war and total connection.\n\nThe 20th century saw two World Wars, the rise and fall of Communism, and the splitting of the atom. We moved from horse-drawn carriages to landing on the Moon in 60 years.\n\nThis section explores the Cold War, the Civil Rights movement, and the Digital Revolution that created the Information Age we live in today."
            }
        };

        // --- 2. LOGIC TO OPEN AN ERA ---
        function openEra(eraKey) {
            // A. Get the data
            const data = eraContent[eraKey];
            
            // B. Populate the 'era-viewer' HTML elements
            document.getElementById('era-title').innerText = data.title;
            document.getElementById('era-text').innerText = data.text;
            document.getElementById('era-image').src = data.img;

            // C. Switch view
            showSection('era-viewer');
            
            // D. Scroll to top
            window.scrollTo(0,0);
        }

        // --- 3. STANDARD NAVIGATION ---
        function showSection(sectionId) {
            // Hide all
            document.querySelectorAll('.page-section').forEach(sec => {
                sec.classList.remove('active');
                sec.style.display = 'none';
            });

            // Show Target
            const target = document.getElementById(sectionId);
            target.style.display = 'flex';
            setTimeout(() => target.classList.add('active'), 10);
        }

        // --- 4. PRELOADER ---
        window.addEventListener('load', () => {
            const pre = document.getElementById('preloader');
            setTimeout(() => {
                pre.style.opacity = '0';
                setTimeout(() => pre.style.display = 'none', 800);
            }, 1000);
        });

        // Start at home
        showSection('home');
    </script>

</body>
</html>
