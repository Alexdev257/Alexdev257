<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Alex - Developer Portfolio</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #0a0e27;
            color: #fff;
            overflow-x: hidden;
        }

        #canvas-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
        }

        .content {
            position: relative;
            z-index: 1;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px 15px;
        }

        .hero {
            text-align: center;
            padding: 40px 20px;
            background: rgba(10, 14, 39, 0.7);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            margin-bottom: 30px;
            border: 1px solid rgba(255, 165, 0, 0.2);
        }

        .hero img.myname {
            max-width: 100%;
            height: auto;
            margin-bottom: 20px;
            animation: fadeInDown 1s ease;
        }

        .hero p {
            font-size: clamp(0.9rem, 2vw, 1.2rem);
            color: #ccc;
            margin: 10px 0;
            padding: 0 10px;
        }

        .hero img.coding-gif {
            max-width: 280px;
            width: 100%;
            height: auto;
            border-radius: 20px;
            margin: 30px 0;
            box-shadow: 0 10px 30px rgba(255, 165, 0, 0.3);
        }

        .section {
            background: rgba(20, 25, 50, 0.8);
            backdrop-filter: blur(10px);
            padding: 30px 20px;
            margin: 20px 0;
            border-radius: 20px;
            border: 1px solid rgba(255, 165, 0, 0.1);
            opacity: 0;
            transform: translateY(30px);
        }

        .section h2 {
            text-align: center;
            font-size: clamp(1.5rem, 4vw, 2.5rem);
            margin-bottom: 25px;
            color: #ffa500;
        }

        .tech-icons {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 8px;
            margin: 20px 0;
        }

        .tech-icons img {
            max-width: 100%;
            height: auto;
            transition: all 0.3s ease;
            filter: drop-shadow(0 5px 10px rgba(255, 165, 0, 0.2));
        }

        .tech-icons img:hover {
            transform: translateY(-10px) scale(1.1);
            filter: drop-shadow(0 10px 20px rgba(255, 165, 0, 0.5));
        }

        .badge-container {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 15px;
        }

        .badge-container img {
            max-width: 100%;
            height: auto;
            transition: all 0.3s ease;
        }

        .badge-container img:hover {
            transform: translateY(-5px);
            filter: brightness(1.2);
        }

        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .stat-img {
            width: 100%;
            height: auto;
            border-radius: 12px;
            border: 2px solid rgba(255, 165, 0, 0.3);
            transition: all 0.3s ease;
        }

        .stat-img:hover {
            border-color: #ffa500;
            transform: translateY(-5px);
            box-shadow: 0 10px 30px rgba(255, 165, 0, 0.4);
        }

        .social-links {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-top: 30px;
            flex-wrap: wrap;
        }

        .social-links a {
            display: inline-block;
        }

        .social-links img {
            max-width: 100%;
            height: auto;
            transition: all 0.3s ease;
        }

        .social-links img:hover {
            transform: translateY(-5px) scale(1.1);
            filter: brightness(1.2);
        }

        .animation-footer {
            text-align: center;
            margin: 40px 0;
        }

        .animation-footer img {
            max-width: 100%;
            height: auto;
            border-radius: 15px;
            margin: 20px 0;
            box-shadow: 0 10px 30px rgba(255, 165, 0, 0.3);
        }

        .animation-footer img.code-gif {
            max-width: 200px;
            width: 100%;
        }

        .animation-footer img.typing-svg {
            max-width: 435px;
            width: 100%;
        }

        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Tablet landscape and smaller desktop */
        @media (max-width: 1024px) {
            .content {
                padding: 20px 20px;
            }

            .hero {
                padding: 35px 20px;
            }

            .section {
                padding: 25px 20px;
            }
        }

        /* Tablet portrait */
        @media (max-width: 768px) {
            .content {
                padding: 15px 15px;
            }

            .hero {
                padding: 30px 15px;
                margin-bottom: 20px;
            }

            .hero img.coding-gif {
                max-width: 220px;
                margin: 20px 0;
            }

            .section {
                padding: 20px 15px;
                margin: 15px 0;
            }

            .section h2 {
                margin-bottom: 20px;
            }

            .stats {
                grid-template-columns: 1fr;
                gap: 15px;
            }

            .tech-icons {
                gap: 6px;
            }

            .badge-container {
                gap: 8px;
            }

            .social-links {
                gap: 8px;
            }

            .animation-footer img.code-gif {
                max-width: 150px;
            }
        }

        /* Mobile landscape */
        @media (max-width: 640px) {
            .hero {
                padding: 25px 15px;
            }

            .hero img.coding-gif {
                max-width: 180px;
            }

            .section {
                padding: 20px 12px;
            }

            .tech-icons img {
                max-width: 45px;
            }
        }

        /* Mobile portrait */
        @media (max-width: 480px) {
            .content {
                padding: 10px 10px;
            }

            .hero {
                padding: 20px 10px;
                border-radius: 15px;
            }

            .hero img.coding-gif {
                max-width: 160px;
                margin: 15px 0;
            }

            .section {
                padding: 20px 10px;
                margin: 15px 0;
                border-radius: 15px;
            }

            .tech-icons {
                gap: 5px;
            }

            .tech-icons img {
                max-width: 40px;
            }

            .badge-container {
                gap: 6px;
            }

            .badge-container img {
                max-width: 140px;
            }

            .social-links {
                gap: 6px;
            }

            .social-links img {
                max-width: 120px;
            }

            .animation-footer {
                margin: 30px 0;
            }

            .animation-footer img.code-gif {
                max-width: 120px;
            }

            .stats {
                gap: 12px;
            }
        }

        /* Very small devices */
        @media (max-width: 360px) {
            .hero {
                padding: 15px 8px;
            }

            .hero img.coding-gif {
                max-width: 140px;
            }

            .section {
                padding: 15px 8px;
            }

            .tech-icons img {
                max-width: 35px;
            }

            .badge-container img {
                max-width: 120px;
            }

            .social-links img {
                max-width: 100px;
            }

            .animation-footer img.code-gif {
                max-width: 100px;
            }
        }
    </style>
</head>
<body>
    <div id="canvas-container"></div>
    
    <div class="content">
        <div class="hero">
            <img class="myname" src="https://readme-typing-svg.herokuapp.com/?font=Righteous&size=35&center=true&vCenter=true&width=500&height=70&duration=4000&lines=Hi+There!+👋;+I'm+Alex!" alt="Name Animation" />
            <p>🎓 <strong>Currently studying at FPT University</strong></p>
            <p>💻 <em>Full-Stack Developer | Focused on Performance, Security, and Clean Code</em></p>
            <img class="coding-gif" src="https://genk.mediacdn.vn/2017/giphy-1504888368602.gif" alt="Coding Animation" />
        </div>

        <div class="section" id="frontend">
            <h2>⚒️ Front End ⚒️</h2>
            <div class="tech-icons">
                <img src="https://skillicons.dev/icons?i=html,css,js,ts,nodejs,react,next,vue,angular,bootstrap,tailwind,sass" alt="Frontend Technologies" />
            </div>
        </div>

        <div class="section" id="backend">
            <h2>⚒️ Back End ⚒️</h2>
            <div class="tech-icons">
                <img src="https://skillicons.dev/icons?i=c,cpp,cs,java,nodejs,express,nest,spring,dotnet" alt="Backend Technologies" />
            </div>
        </div>

        <div class="section" id="mobile">
            <h2>⚒️ Mobile App ⚒️</h2>
            <div class="tech-icons">
                <img src="https://skillicons.dev/icons?i=react,flutter,kotlin,swift" alt="Mobile Technologies" />
            </div>
        </div>

        <div class="section" id="games">
            <h2>⚒️ Games ⚒️</h2>
            <div class="tech-icons">
                <img src="https://skillicons.dev/icons?i=unity" alt="Game Development" />
            </div>
        </div>

        <div class="section" id="iot">
            <h2>⚒️ IoT ⚒️</h2>
            <div class="tech-icons">
                <img src="https://skillicons.dev/icons?i=arduino" alt="IoT" />
            </div>
        </div>

        <div class="section" id="database">
            <h2>⚒️ Database & Queue ⚒️</h2>
            <div class="tech-icons">
                <img src="https://skillicons.dev/icons?i=mysql,sqlite,mongodb,redis,rabbitmq" alt="Databases" />
            </div>
            <div class="badge-container">
                <img src="https://img.shields.io/badge/SQLServer-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white" alt="SQL Server" />
            </div>
        </div>

        <div class="section" id="deployment">
            <h2>⚒️ Deployment Tools ⚒️</h2>
            <div class="tech-icons">
                <img src="https://skillicons.dev/icons?i=docker,kubernetes,jenkins,aws,azure" alt="Deployment Tools" />
            </div>
            <div class="badge-container">
                <img src="https://img.shields.io/badge/Railway-0B0D0E?style=for-the-badge&logo=railway&logoColor=white" alt="Railway" />
                <img src="https://img.shields.io/badge/Render-46E3B7?style=for-the-badge&logo=render&logoColor=black" alt="Render" />
                <img src="https://img.shields.io/badge/ngrok-1F1E37?style=for-the-badge&logo=ngrok&logoColor=FBB040" alt="ngrok" />
            </div>
        </div>

        <div class="section" id="stats">
            <h2>📊 GitHub Stats</h2>
            <div class="stats">
                <img class="stat-img" src="https://github-readme-stats.vercel.app/api?username=Alexdev257&show_icons=true&theme=radical&hide_border=true&border_radius=12&title_color=ffa500&icon_color=ff8c00&text_color=ffffff" alt="GitHub Stats" />
                <img class="stat-img" src="https://github-readme-stats.vercel.app/api/top-langs/?username=Alexdev257&layout=compact&hide_border=true&title_color=ffa500&text_color=ffffff&bg_color=20232a" alt="Top Languages" />
            </div>
        </div>

        <div class="section animation-footer">
            <h2>✨ Let's make this dynamic ✨</h2>
            <img class="code-gif" src="https://media.giphy.com/media/du3J3cXyzhj75IOgvA/giphy.gif" alt="Coding animation" />
            <br/>
            <img class="typing-svg" src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=22&pause=1000&color=FFA500&center=true&vCenter=true&width=435&lines=Welcome+to+Minhtamkim's+Profile!;Web+Developer+%7C+Tech+Enthusiast;Always+learning+new+things+%F0%9F%92%BB" alt="Typing SVG animation" />
        </div>

        <div class="section" id="connect">
            <h2>🌐 Let's Connect!</h2>
            <div class="social-links">
                <a href="https://github.com/Alexdev257" target="_blank">
                    <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub" />
                </a>
                <a href="https://www.facebook.com/bui.phuoc.thang.2024" target="_blank">
                    <img src="https://img.shields.io/badge/Facebook-1877F2?style=for-the-badge&logo=facebook&logoColor=white" alt="Facebook" />
                </a>
                <a href="https://www.instagram.com/thangws.25/" target="_blank">
                    <img src="https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white" alt="Instagram" />
                </a>
            </div>
        </div>
    </div>

    <script>
        // Three.js Scene Setup
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });
        
        renderer.setSize(window.innerWidth, window.innerHeight);
        document.getElementById('canvas-container').appendChild(renderer.domElement);

        // Adjust particle count based on screen size
        const isMobile = window.innerWidth < 768;
        const particlesCount = isMobile ? 1500 : 3000;

        // Create particles
        const particlesGeometry = new THREE.BufferGeometry();
        const posArray = new Float32Array(particlesCount * 3);

        for(let i = 0; i < particlesCount * 3; i++) {
            posArray[i] = (Math.random() - 0.5) * 100;
        }

        particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));

        const particlesMaterial = new THREE.PointsMaterial({
            size: isMobile ? 0.12 : 0.1,
            color: 0xffa500,
            transparent: true,
            opacity: 0.8,
            blending: THREE.AdditiveBlending
        });

        const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
        scene.add(particlesMesh);

        // Create geometric shapes (fewer on mobile)
        const geometries = [
            new THREE.TorusGeometry(3, 0.5, 16, 100),
            new THREE.OctahedronGeometry(2),
            new THREE.IcosahedronGeometry(2)
        ];

        const material = new THREE.MeshBasicMaterial({
            color: 0xffa500,
            wireframe: true,
            transparent: true,
            opacity: 0.3
        });

        const shapes = [];
        const shapeCount = isMobile ? 2 : 3;
        
        for(let i = 0; i < shapeCount; i++) {
            const mesh = new THREE.Mesh(geometries[i], material);
            mesh.position.set(
                (Math.random() - 0.5) * 20,
                (Math.random() - 0.5) * 20,
                (Math.random() - 0.5) * 20 - 10
            );
            shapes.push(mesh);
            scene.add(mesh);
        }

        camera.position.z = 30;

        // Mouse movement
        let mouseX = 0;
        let mouseY = 0;

        document.addEventListener('mousemove', (e) => {
            mouseX = (e.clientX / window.innerWidth) * 2 - 1;
            mouseY = -(e.clientY / window.innerHeight) * 2 + 1;
        });

        // Touch support for mobile
        document.addEventListener('touchmove', (e) => {
            if (e.touches.length > 0) {
                mouseX = (e.touches[0].clientX / window.innerWidth) * 2 - 1;
                mouseY = -(e.touches[0].clientY / window.innerHeight) * 2 + 1;
            }
        });

        // Animation loop
        function animate() {
            requestAnimationFrame(animate);

            // Rotate particles
            particlesMesh.rotation.x += 0.0003;
            particlesMesh.rotation.y += 0.0005;

            // Rotate shapes
            shapes.forEach((shape, i) => {
                shape.rotation.x += 0.005 * (i + 1);
                shape.rotation.y += 0.003 * (i + 1);
            });

            // Camera movement based on mouse (reduced on mobile)
            const dampening = isMobile ? 0.03 : 0.05;
            camera.position.x += (mouseX * 5 - camera.position.x) * dampening;
            camera.position.y += (mouseY * 5 - camera.position.y) * dampening;
            camera.lookAt(scene.position);

            renderer.render(scene, camera);
        }

        animate();

        // GSAP Animations for sections
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    gsap.to(entry.target, {
                        opacity: 1,
                        y: 0,
                        duration: 1,
                        ease: "power2.out"
                    });
                }
            });
        }, { threshold: 0.1 });

        document.querySelectorAll('.section').forEach(section => {
            observer.observe(section);
        });

        // Animate tech icons on hover with GSAP
        document.querySelectorAll('.tech-icons img, .badge-container img, .social-links img').forEach(icon => {
            icon.addEventListener('mouseenter', function() {
                gsap.to(this, {
                    y: -10,
                    scale: 1.1,
                    duration: 0.3,
                    ease: "back.out(1.7)"
                });
            });

            icon.addEventListener('mouseleave', function() {
                gsap.to(this, {
                    y: 0,
                    scale: 1,
                    duration: 0.3
                });
            });
        });

        // Window resize handler
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
    </script>
</body>
</html>
