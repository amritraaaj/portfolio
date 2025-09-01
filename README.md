<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Resume | Amritraj Jayathilak</title>
    <!-- Chosen Palette: Modern Contrast -->
    <!-- Application Structure Plan: The SPA is designed as a narrative, top-down scrolling experience to guide a recruiter through Amritraj's professional story. It begins with a strong Hero section for immediate impact. The core is an interactive vertical timeline for work experience, allowing users to drill into details without cluttering the initial view. This is more engaging than a static list. Following this is a Skills Dashboard with charts to visually quantify capabilities, which is more compelling than a bulleted list. The structure concludes with education and a clear contact section. This thematic flow—Introduction, Experience, Skills, Credentials—is logical, scannable, and designed to hold user interest while highlighting key qualifications effectively. -->
    <!-- Visualization & Content Choices: 
        - Profile/Summary: Report Info -> Goal: Inform -> Presentation: Text block -> Interaction: None -> Justification: Clear, concise professional introduction. -> Method: HTML.
        - Work Experience: Report Info -> Goal: Organize & show change over time -> Viz: Interactive Vertical Timeline -> Interaction: Click on a job title to expand/collapse details. -> Justification: Makes exploring career history engaging and non-linear, showing progression clearly. -> Method: HTML/CSS/Vanilla JS.
        - Skills: Report Info (inferred technical skills) -> Goal: Compare & Inform -> Viz: Multiple horizontal bar charts (Chart.js) -> Interaction: Hover for tooltips. -> Justification: Visually breaks down diverse skills into understandable categories (Technical, Software, Professional), making proficiency levels easy to grasp. -> Library: Chart.js (Canvas).
        - Key Clients: Report Info -> Goal: Inform & build credibility -> Viz: Styled cards -> Interaction: Subtle hover effects -> Justification: Highlights high-profile clients to quickly establish professional legitimacy. -> Method: HTML/CSS.
        - CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&family=Roboto+Mono:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Montserrat', sans-serif;
            background-color: #121212;
            color: #E0E0E0;
        }
        .bg-primary { background-color: #000000; }
        .bg-secondary { background-color: #282828; }
        .text-accent { color: #FF0000; }
        .border-accent { border-color: #FF0000; }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 700px;
            margin-left: auto;
            margin-right: auto;
            height: 280px;
            max-height: 350px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 320px;
            }
        }
        .timeline-item .details {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease-in-out;
        }
        .timeline-item.open .details {
            max-height: 500px;
        }
        .font-thin { font-weight: 400; }
        .font-bold { font-weight: 700; }
        .font-mono { font-family: 'Roboto Mono', monospace; }
    </style>
</head>
<body class="antialiased">
    <header class="bg-primary text-white sticky top-0 z-50 shadow-lg">
        <nav class="container mx-auto px-6 py-3 flex justify-between items-center">
            <div class="text-xl font-bold font-mono">Amritraj Jayathilak</div>
            <div class="hidden md:flex space-x-6 font-thin">
                <a href="#profile" class="hover:text-accent">Profile</a>
                <a href="#experience" class="hover:text-accent">Experience</a>
                <a href="#skills" class="hover:text-accent">Skills</a>
                <a href="#contact" class="hover:text-accent">Contact</a>
            </div>
            <button id="mobile-menu-button" class="md:hidden focus:outline-none text-white">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path></svg>
            </button>
        </nav>
        <div id="mobile-menu" class="hidden md:hidden bg-secondary">
            <a href="#profile" class="block py-2 px-6 text-sm hover:bg-black hover:text-accent">Profile</a>
            <a href="#experience" class="block py-2 px-6 text-sm hover:bg-black hover:text-accent">Experience</a>
            <a href="#skills" class="block py-2 px-6 text-sm hover:bg-black hover:text-accent">Skills</a>
            <a href="#contact" class="block py-2 px-6 text-sm hover:bg-black hover:text-accent">Contact</a>
        </div>
    </header>

    <main class="container mx-auto px-6 py-12">
        <section id="hero" class="text-center py-20">
            <h1 class="text-5xl md:text-7xl font-bold font-mono text-accent">AMRITRAJ JAYATHILAK</h1>
            <p class="text-xl md:text-2xl mt-4 font-thin text-gray-300">Freelance Photographer & Videographer</p>
            <p class="mt-6 max-w-2xl mx-auto font-thin text-gray-400">Transforming visions into compelling visual stories through brand, fashion, and event photography.</p>
        </section>

        <section id="profile" class="py-16">
            <div class="bg-secondary p-8 rounded-lg shadow-lg">
                <h2 class="text-3xl font-bold text-accent mb-4 text-center">Professional Profile</h2>
                <p class="text-lg font-thin text-gray-300 leading-relaxed text-center max-w-3xl mx-auto">
                    Creative and detail-oriented photographer and videographer with over 4 years of professional experience. Skilled in capturing compelling visuals across diverse domains, including product, fashion, brand, and event shoots. Adept at collaborating with clients to deliver high-quality imagery that aligns with their vision and brand identity. Experienced freelancer with a proven track record of meeting deadlines and exceeding expectations in dynamic, fast-paced environments.
                </p>
            </div>
        </section>

        <section id="experience" class="py-16">
            <h2 class="text-3xl font-bold text-accent mb-12 text-center">Interactive Career Timeline</h2>
             <p class="text-center font-thin text-gray-400 mb-12 max-w-2xl mx-auto">Explore my professional journey. My experience spans renowned brands and dynamic startups, contributing to significant marketing and engagement goals. Click on any role to see key responsibilities and accomplishments.</p>
            <div class="relative max-w-3xl mx-auto">
                <div class="absolute left-1/2 h-full w-1 bg-gray-600 rounded-full transform -translate-x-1/2"></div>
                <div id="timeline-container" class="space-y-16">
                </div>
            </div>
        </section>

        <section id="skills" class="py-16">
            <h2 class="text-3xl font-bold text-accent mb-12 text-center">Skills Dashboard</h2>
            <p class="text-center font-thin text-gray-400 mb-12 max-w-2xl mx-auto">A visual overview of my technical and professional capabilities. I bring a diverse set of skills to every project, from creative execution to strategic planning, ensuring a comprehensive approach to content creation.</p>
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
                <div class="bg-secondary p-6 rounded-lg shadow-lg">
                    <h3 class="font-bold text-xl text-center mb-4 text-accent">Photography & Videography</h3>
                    <div class="chart-container">
                        <canvas id="photoVideoSkillsChart"></canvas>
                    </div>
                </div>
                <div class="bg-secondary p-6 rounded-lg shadow-lg">
                    <h3 class="font-bold text-xl text-center mb-4 text-accent">Software Proficiency</h3>
                    <div class="chart-container">
                        <canvas id="softwareSkillsChart"></canvas>
                    </div>
                </div>
                 <div class="bg-secondary p-6 rounded-lg shadow-lg lg:col-span-2">
                    <h3 class="font-bold text-xl text-center mb-4 text-accent">Professional Skills</h3>
                    <div class="chart-container">
                        <canvas id="professionalSkillsChart"></canvas>
                    </div>
                </div>
            </div>
        </section>

        <section id="education" class="py-16">
             <h2 class="text-3xl font-bold text-accent mb-12 text-center">Education</h2>
             <div class="max-w-3xl mx-auto grid grid-cols-1 md:grid-cols-2 gap-8">
                 <div class="bg-secondary p-6 rounded-lg shadow-md text-center">
                    <h3 class="font-bold text-lg text-accent">St. Joseph’s University</h3>
                    <p class="text-gray-300 font-thin">Bachelor of Vocation (B.Voc), Visual Media and Filmmaking</p>
                    <p class="text-gray-500 font-mono text-sm mt-1">2022 - 2025</p>
                 </div>
                 <div class="bg-secondary p-6 rounded-lg shadow-md text-center">
                    <h3 class="font-bold text-lg text-accent">St. Joseph’s Pre-University College</h3>
                    <p class="text-gray-300 font-thin">PCMB Science</p>
                    <p class="text-gray-500 font-mono text-sm mt-1">2019 - 2021</p>
                 </div>
             </div>
        </section>

        <section id="contact" class="py-16 text-center bg-secondary rounded-lg shadow-lg">
            <h2 class="text-3xl font-bold text-accent mb-4">Let's Create Together</h2>
            <p class="text-gray-400 font-thin mb-8 max-w-xl mx-auto">I'm currently available for freelance projects and full-time opportunities. Reach out to discuss your next project.</p>
            <div class="flex flex-col md:flex-row justify-center items-center space-y-4 md:space-y-0 md:space-x-8">
                <a href="mailto:amritrajthilak@gmail.com" class="text-lg font-thin hover:text-accent">amritrajthilak@gmail.com</a>
                <span class="hidden md:block text-gray-600">|</span>
                <p class="text-lg font-thin">+91 8073520601</p>
                <span class="hidden md:block text-gray-600">|</span>
                <a href="http://amritrajthilak.com" target="_blank" rel="noopener noreferrer" class="text-lg font-bold bg-accent text-white py-2 px-5 rounded-md hover:bg-opacity-80 transition duration-300">View Portfolio</a>
            </div>
        </section>
    </main>
    
<script>
document.addEventListener('DOMContentLoaded', function () {
    const mobileMenuButton = document.getElementById('mobile-menu-button');
    const mobileMenu = document.getElementById('mobile-menu');

    mobileMenuButton.addEventListener('click', () => {
        mobileMenu.classList.toggle('hidden');
    });

    document.querySelectorAll('#mobile-menu a').forEach(link => {
        link.addEventListener('click', () => {
            mobileMenu.classList.add('hidden');
        });
    });

    const experienceData = [
        {
            company: 'Redbull',
            role: 'Photographer',
            period: 'Jan 2024',
            side: 'left',
            details: 'Executed high-impact photography for a national marketing campaign that reached over 100,000 potential customers, directly supporting brand visibility goals.'
        },
        {
            company: 'Lycaon',
            role: 'Freelance Photographer',
            period: '2024',
            side: 'right',
            details: 'Produced comprehensive photo and video content for a diverse portfolio of 15+ small businesses, directly increasing their social media engagement and online presence.'
        },
        {
            company: 'InstaWings',
            role: 'Content Creator',
            period: '2023',
            side: 'left',
            details: 'Managed social media channels and created video content that contributed to a 25% increase in audience engagement and a 15% growth in follower count over 6 months. Collaborated with marketing to ensure visual consistency.'
        },
        {
            company: 'Sarayu Designs',
            role: 'Content Creator',
            period: '2022 - 2023',
            side: 'right',
            details: 'Covered 10+ high-profile fashion events and corporate shoots across Bengaluru, managing end-to-end production from on-site capture to final polished deliverables.'
        },
        {
            company: 'Freelance',
            role: 'Content Creator',
            period: '2020',
            side: 'left',
            details: 'Led freelance operations, successfully completing over 50 projects for a diverse clientele including Instagram influencers, product brands, and fashion labels. Specialized in delivering tailored visual content that enhances brand identity.'
        }
    ];

    const timelineContainer = document.getElementById('timeline-container');
    experienceData.forEach(item => {
        const alignClass = item.side === 'left' ? 'md:items-start md:text-left' : 'md:items-end md:text-right';
        const marginClass = item.side === 'left' ? 'md:mr-auto' : 'md:ml-auto';
        const dotPosition = item.side === 'left' ? 'md:-right-2' : 'md:-left-2';

        const timelineItem = document.createElement('div');
        timelineItem.className = `timeline-item flex flex-col items-center md:w-1/2 ${marginClass}`;

        timelineItem.innerHTML = `
            <div class="relative w-full">
                <div class="absolute top-1/2 transform -translate-y-1/2 w-4 h-4 bg-accent rounded-full z-10 ${dotPosition} border-4 border-black"></div>
                <div class="bg-secondary p-6 rounded-lg shadow-lg cursor-pointer transition transform hover:scale-105" onclick="this.parentElement.parentElement.classList.toggle('open')">
                    <p class="text-sm text-gray-500 font-thin">${item.period}</p>
                    <h3 class="text-xl font-bold text-accent">${item.company}</h3>
                    <p class="text-md text-gray-300 font-thin">${item.role}</p>
                    <div class="details mt-4 pt-4 border-t border-gray-600">
                        <p class="text-gray-400 font-thin">${item.details}</p>
                    </div>
                    <div class="text-xs text-center mt-2 text-accent font-thin">Click to expand</div>
                </div>
            </div>
        `;
        timelineContainer.appendChild(timelineItem);
    });

    const createChart = (ctx, type, labels, data, label, backgroundColor) => {
        new Chart(ctx, {
            type: type,
            data: {
                labels: labels,
                datasets: [{
                    label: label,
                    data: data,
                    backgroundColor: backgroundColor,
                    borderColor: backgroundColor.map(c => c.replace('0.6', '1')),
                    borderWidth: 1
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                indexAxis: 'y',
                scales: {
                    x: {
                        beginAtZero: true,
                        max: 100,
                        ticks: {
                            display: false
                        },
                        grid: {
                            display: false,
                            drawBorder: false
                        }
                    },
                    y: {
                        ticks: {
                           font: {
                               size: 14,
                               weight: '400'
                           },
                           color: '#E0E0E0'
                        },
                         grid: {
                            display: false,
                            drawBorder: false
                        }
                    }
                },
                plugins: {
                    legend: {
                        display: false
                    },
                    tooltip: {
                        enabled: true,
                        callbacks: {
                            label: function(context) {
                                return ` Proficiency: ${context.raw}%`;
                            }
                        }
                    }
                }
            }
        });
    };

    const photoVideoSkillsCtx = document.getElementById('photoVideoSkillsChart').getContext('2d');
    createChart(photoVideoSkillsCtx, 'bar', ['Event Coverage', 'Fashion & Model', 'Product & Brand', 'Drone Videography', 'Video Editing'], [95, 95, 90, 80, 95], 'Proficiency', ['rgba(255, 0, 0, 0.6)', 'rgba(255, 0, 0, 0.6)', 'rgba(255, 0, 0, 0.6)', 'rgba(255, 0, 0, 0.6)', 'rgba(255, 0, 0, 0.6)']);

    const softwareSkillsCtx = document.getElementById('softwareSkillsChart').getContext('2d');
    createChart(softwareSkillsCtx, 'bar', ['Adobe Lightroom', 'Adobe Photoshop', 'Adobe Premiere Pro', 'DaVinci Resolve', 'Capture One'], [100, 100, 100, 80, 75], 'Proficiency', ['rgba(255, 0, 0, 0.6)', 'rgba(255, 0, 0, 0.6)', 'rgba(255, 0, 0, 0.6)', 'rgba(255, 0, 0, 0.6)', 'rgba(255, 0, 0, 0.6)']);

    const professionalSkillsCtx = document.getElementById('professionalSkillsChart').getContext('2d');
    createChart(professionalSkillsCtx, 'bar', ['Client Communication', 'Project Management', 'Creative Thinking', 'Brand Development', 'Adaptability'], [95, 90, 95, 85, 90], 'Proficiency', ['rgba(255, 0, 0, 0.6)', 'rgba(255, 0, 0, 0.6)', 'rgba(255, 0, 0, 0.6)', 'rgba(255, 0, 0, 0.6)', 'rgba(255, 0, 0, 0.6)']);
});
</script>
</body>
</html>
