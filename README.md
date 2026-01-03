<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DeepThought Frontend Task</title>
    <!-- Google Fonts for better aesthetics -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&family=Open+Sans:wght@400;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-blue: #0029FF;
            --bg-gray: #F0F2F5;
            --text-dark: #333333;
            --shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
            --border-radius: 15px;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background-color: var(--bg-gray);
            color: var(--text-dark);
        }

        /* Task 1: Header & Layout */
        header {
            background: #F0F2F5;
            height: 90px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 50px;
            box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.1);
        }

        .logo {
            width: 311px;
            height: 49px;
            background: #fff; /* Placeholder for Logo */
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            color: var(--primary-blue);
        }

        .nav-icons {
            display: flex;
            gap: 20px;
        }

        .icon-circle {
            width: 30px;
            height: 30px;
            background: #3683F0;
            border-radius: 50%;
            cursor: pointer;
        }

        main {
            padding: 40px 100px;
        }

        .title-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
        }

        .btn-submit {
            background: var(--primary-blue);
            color: white;
            padding: 10px 25px;
            border-radius: 10px;
            border: none;
            cursor: pointer;
            font-weight: 600;
        }

        .intro-box {
            background: #E9ECEF;
            padding: 25px;
            border-radius: 5px;
            margin-bottom: 40px;
        }

        /* Task 2: Dynamic Grid System */
        #project-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(450px, 1fr));
            gap: 40px;
        }

        .asset-card {
            background: #FFFFFF;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            overflow: hidden;
            display: flex;
            flex-direction: column;
            min-height: 500px;
        }

        .asset-header {
            background: black;
            color: white;
            padding: 15px;
            text-align: center;
            position: relative;
        }

        .asset-content {
            padding: 20px;
            flex-grow: 1;
        }

        .description {
            font-size: 14px;
            margin-bottom: 20px;
            line-height: 1.6;
        }

        .dynamic-input-area {
            border-top: 1px solid #ddd;
            padding-top: 15px;
        }

        /* Collapsible Logic Styles */
        .collapsible {
            background: #F2F2F2;
            padding: 10px;
            margin-bottom: 10px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: 600;
            display: flex;
            justify-content: space-between;
        }

        .collapsible-content {
            display: none;
            padding: 10px;
            background: #fff;
            border: 1px solid #ddd;
            margin-bottom: 10px;
        }

        textarea {
            width: 100%;
            height: 80px;
            margin-top: 10px;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }

        /* Responsive */
        @media (max-width: 768px) {
            main { padding: 20px; }
            #project-container { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>

    <header>
        <div class="logo">DEEP THOUGHT LOGO</div>
        <div class="nav-icons">
            <div class="icon-circle"></div>
            <div class="icon-circle"></div>
            <div class="icon-circle"></div>
        </div>
    </header>

    <main>
        <div class="title-bar">
            <h1 style="color: var(--primary-blue);">Technical Project Management</h1>
            <button class="btn-submit">Submit Task</button>
        </div>

        <div class="intro-box">
            <h3>Explore the world of management</h3>
            <p>As a project manager, you play a multi-faceted role... (DeepTech Research Intro)</p>
        </div>

        <!-- This is where JS will inject the JSON data -->
        <div id="project-container"></div>
    </main>

    <script>
        // Task 2: JSON Data Object
        const projectData = {
            title: "Technical Project Management",
            assets: [
                {
                    id: 1,
                    title: "Technical Project Management",
                    description: "Story of Alignment Scope of Agility Specific Accountable...",
                    type: "video",
                    content: "https://www.youtube.com/embed/TiMRwbaL37U"
                },
                {
                    id: 2,
                    title: "Threadbuild",
                    description: "Watch the video and threadbuild, and jot out key threads while watching the video.",
                    type: "thread"
                },
                {
                    id: 3,
                    title: "Structure you pointers",
                    description: "Write a 400-500 word article, from your thread. Publish your understanding.",
                    type: "article"
                },
                {
                    id: 4,
                    title: "4SA Method",
                    description: "To explore more read more",
                    type: "method"
                }
            ]
        };

        // Function to render assets dynamically
        function renderAssets() {
            const container = document.getElementById('project-container');
            
            projectData.assets.forEach(asset => {
                const card = document.createElement('div');
                card.className = 'asset-card';
                
                let innerContent = '';

                // Logic based on content type (Execution of Logic)
                if(asset.type === 'video') {
                    innerContent = `<iframe width="100%" height="300" src="${asset.content}" frameborder="0" allowfullscreen></iframe>`;
                } else if(asset.type === 'thread') {
                    innerContent = `
                        <div class="collapsible" onclick="toggleSection(this)">
                            <span>Thread A</span>
                            <span>▼</span>
                        </div>
                        <div class="collapsible-content">
                            <label>Sub Thread 1</label>
                            <textarea placeholder="Enter text here"></textarea>
                        </div>
                    `;
                } else {
                    innerContent = `
                        <div class="dynamic-input-area">
                            <label><b>Title</b></label>
                            <input type="text" style="width:100%; padding:8px; margin: 10px 0;">
                            <label><b>Content</b></label>
                            <textarea placeholder="Write your thoughts..."></textarea>
                        </div>
                    `;
                }

                card.innerHTML = `
                    <div class="asset-header">
                        <h3>${asset.title}</h3>
                    </div>
                    <div class="asset-content">
                        <p class="description"><b>Description:</b> ${asset.description}</p>
                        ${innerContent}
                    </div>
                `;
                
                container.appendChild(card);
            });
        }

        // Toggle functionality (Simple Vanilla JS Logic)
        function toggleSection(element) {
            const content = element.nextElementSibling;
            content.style.display = content.style.display === 'block' ? 'none' : 'block';
        }

        // Initialize on load
        window.onload = renderAssets;
    </script>
</body>
</html>
