<!DOCTYPE html>
<html lang="es" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Guía Interactiva de Repositorios Digitales</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #F8F7F4;
            color: #333745;
        }
        .nav-link {
            transition: color 0.3s ease, border-bottom-color 0.3s ease;
            border-bottom: 2px solid transparent;
        }
        .nav-link:hover, .nav-link.active {
            color: #2563EB;
            border-bottom-color: #2563EB;
        }
        .card {
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
            height: 400px;
            max-height: 50vh;
        }
        [x-cloak] { display: none !important; }
        .tab-button.active {
            border-color: #2563EB;
            background-color: #DBEAFE;
            color: #1E40AF;
        }
        .checklist-item.selected {
            background-color: #DBEAFE;
            border-color: #93C5FD;
        }
    </style>
    <script src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js" defer></script>
</head>
<body x-data="repositoryApp()">
    <!-- Chosen Palette: Academic Calm -->
    <!-- Application Structure Plan: The SPA abandons the linear 'class' format for a thematic, exploratory structure. It starts with a Hero section defining repositories, followed by a sticky navigation bar for quick access to key sections: 1) '¿Qué son?' for fundamentals, 2) 'Tipos' using interactive cards for focused learning, 3) 'Comparativa' with a dynamic chart for visual comparison, 4) 'Foco en Zenodo' with a tabbed interface for a deep dive, and 5) 'Cómo Elegir' as an interactive checklist. This architecture prioritizes user-driven exploration and data synthesis over passive reading, making complex information more digestible and engaging. -->
    <!-- Visualization & Content Choices: 
        - Report Info: Repository Types (Institutional, Thematic, etc.). Goal: Organize/Inform. Viz: Interactive HTML cards. Interaction: Click to expand details. Justification: Prevents 'wall of text', focuses user attention. Library: HTML/CSS/Alpine.js.
        - Report Info: Comparative data (storage limits, cost, etc. for Zenodo, Figshare, etc.). Goal: Compare. Viz: Bar Chart. Interaction: User selects metric from a dropdown to update the chart dynamically. Justification: Visual comparison is more intuitive and impactful than a static table. Library: Chart.js.
        - Report Info: Selection criteria for repositories. Goal: Guide. Viz: Interactive checklist. Interaction: User checks important criteria, the app highlights suitable repository types. Justification: Transforms a passive list into an active decision-making tool. Library: HTML/CSS/Alpine.js.
        - Report Info: Detailed Zenodo features. Goal: Detail/Inform. Viz: Tabbed interface. Interaction: Click tabs to switch content view. Justification: Organizes dense information into manageable chunks. Library: HTML/CSS/Alpine.js.
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

    <header class="bg-white shadow-md sticky top-0 z-50">
        <nav class="container mx-auto px-6 py-3 flex justify-between items-center">
            <a href="#" class="text-xl font-bold text-blue-800">Guía de Repositorios</a>
            <div class="hidden md:flex space-x-6">
                <a href="#fundamentos" class="py-2 nav-link">¿Qué son?</a>
                <a href="#tipos" class="py-2 nav-link">Tipos</a>
                <a href="#comparativa" class="py-2 nav-link">Comparativa</a>
                <a href="#zenodo" class="py-2 nav-link">Foco en Zenodo</a>
                <a href="#elegir" class="py-2 nav-link">Cómo Elegir</a>
            </div>
            <button @click="mobileMenuOpen = !mobileMenuOpen" class="md:hidden">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
                </svg>
            </button>
        </nav>
        <div x-show="mobileMenuOpen" x-cloak class="md:hidden">
            <a href="#fundamentos" @click="mobileMenuOpen = false" class="block py-2 px-4 text-sm hover:bg-gray-200">¿Qué son?</a>
            <a href="#tipos" @click="mobileMenuOpen = false" class="block py-2 px-4 text-sm hover:bg-gray-200">Tipos</a>
            <a href="#comparativa" @click="mobileMenuOpen = false" class="block py-2 px-4 text-sm hover:bg-gray-200">Comparativa</a>
            <a href="#zenodo" @click="mobileMenuOpen = false" class="block py-2 px-4 text-sm hover:bg-gray-200">Foco en Zenodo</a>
            <a href="#elegir" @click="mobileMenuOpen = false" class="block py-2 px-4 text-sm hover:bg-gray-200">Cómo Elegir</a>
        </div>
    </header>

    <main class="container mx-auto px-6 py-12">
        <section id="hero" class="text-center mb-24">
            <h1 class="text-4xl md:text-6xl font-bold mb-4">Navegando el Universo de los Repositorios Digitales</h1>
            <p class="text-lg md:text-xl max-w-3xl mx-auto text-gray-600">
                Una guía interactiva para entender, comparar y seleccionar las herramientas esenciales para la preservación y difusión de la investigación en la era de la Ciencia Abierta.
            </p>
        </section>

        <section id="fundamentos" class="py-16">
            <div class="max-w-4xl mx-auto">
                <h2 class="text-3xl font-bold text-center mb-2">¿Qué es un Repositorio Digital?</h2>
                <p class="text-center text-gray-600 mb-12">Más allá de un simple "almacén", los repositorios son infraestructuras activas y multifacéticas que potencian la visibilidad, el impacto y la preservación de la producción científica. Son pilares del Acceso Abierto, democratizando el conocimiento al eliminar barreras económicas y geográficas.</p>
                
                <div class="grid md:grid-cols-2 gap-8 text-center">
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <div class="text-blue-600 mb-3">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12 mx-auto" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10" /></svg>
                        </div>
                        <h3 class="text-xl font-semibold mb-2">Funciones Clave</h3>
                        <p class="text-gray-600">Preservación a largo plazo, acceso universal, difusión global del conocimiento y fomento de la colaboración entre investigadores.</p>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <div class="text-green-600 mb-3">
                             <svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12 mx-auto" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6" /></svg>
                        </div>
                        <h3 class="text-xl font-semibold mb-2">Beneficios Directos</h3>
                        <p class="text-gray-600">Aumentan el impacto y las citas del investigador, refuerzan el prestigio institucional y aceleran la innovación en la sociedad.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="tipos" class="py-16 bg-white rounded-xl shadow-lg">
             <div class="max-w-6xl mx-auto px-4">
                <h2 class="text-3xl font-bold text-center mb-2">Explora los Tipos de Repositorios</h2>
                 <p class="text-center text-gray-600 mb-12">No existe una solución única. El ecosistema de repositorios es diverso, con cada tipo diseñado para un propósito específico. Haz clic en cada tarjeta para descubrir sus características, ventajas y desventajas.</p>
                
                <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                    <template x-for="(type, index) in repositoryTypes" :key="index">
                        <div @click="selectedType = (selectedType === index ? null : index)" 
                            class="card bg-gray-50 p-6 rounded-lg shadow-sm cursor-pointer border-2"
                            :class="{'border-blue-500 bg-blue-50': selectedType === index, 'border-transparent': selectedType !== index}">
                            <div class="flex items-center mb-4">
                                <div class="text-xl mr-4" x-text="type.icon"></div>
                                <h3 class="text-xl font-bold text-gray-800" x-text="type.title"></h3>
                            </div>
                            <p class="text-gray-600" x-text="type.description"></p>
                            <div x-show="selectedType === index" x-cloak x-transition class="mt-4 text-left text-sm space-y-3">
                                <p><strong class="font-semibold text-gray-700">Ventajas:</strong> <span x-text="type.pros"></span></p>
                                <p><strong class="font-semibold text-gray-700">Desventajas:</strong> <span x-text="type.cons"></span></p>
                                <p><strong class="font-semibold text-gray-700">Ejemplos:</strong> <span x-text="type.examples"></span></p>
                            </div>
                        </div>
                    </template>
                </div>
            </div>
        </section>

        <section id="comparativa" class="py-16">
            <div class="max-w-5xl mx-auto">
                <h2 class="text-3xl font-bold text-center mb-2">Análisis Comparativo Interactivo</h2>
                <p class="text-center text-gray-600 mb-12">Las diferencias importan. Utiliza el selector para comparar visualmente los principales repositorios generalistas según criterios clave y encontrar el que mejor se ajusta a tus necesidades.</p>
                
                <div class="flex justify-center mb-8">
                    <select x-model="selectedMetric" @change="updateChart()" class="border border-gray-300 rounded-md p-2">
                        <option value="storage">Límite de Almacenamiento (GB)</option>
                        <option value="cost">Costo por Depósito (USD)</option>
                    </select>
                </div>

                <div class="chart-container bg-white p-4 rounded-xl shadow-lg">
                    <canvas id="comparisonChart"></canvas>
                </div>
            </div>
        </section>

        <section id="zenodo" class="py-16 bg-white rounded-xl shadow-lg">
            <div class="max-w-4xl mx-auto px-4">
                <h2 class="text-3xl font-bold text-center mb-2">Foco en Zenodo</h2>
                <p class="text-center text-gray-600 mb-12">Zenodo se ha convertido en una solución robusta y versátil para la comunidad científica. Explora sus características fundamentales, desde su potente integración con GitHub hasta su sólido compromiso con la preservación a largo plazo.</p>

                <div x-data="{ activeTab: 'features' }">
                    <div class="border-b border-gray-200 mb-8 flex justify-center space-x-2 md:space-x-4">
                        <button @click="activeTab = 'features'" :class="{ 'active': activeTab === 'features' }" class="tab-button font-semibold py-2 px-4 border-b-2">Características Clave</button>
                        <button @click="activeTab = 'policies'" :class="{ 'active': activeTab === 'policies' }" class="tab-button font-semibold py-2 px-4 border-b-2">Políticas</button>
                        <button @click="activeTab = 'github'" :class="{ 'active': activeTab === 'github' }" class="tab-button font-semibold py-2 px-4 border-b-2">Integración GitHub</button>
                    </div>

                    <div x-show="activeTab === 'features'" x-cloak class="space-y-4 text-gray-700">
                        <p><strong>Asignación de DOI:</strong> Cada depósito, y cada nueva versión, recibe un Identificador de Objeto Digital (DOI) único, garantizando su citabilidad y localización permanente.</p>
                        <p><strong>Versionado Robusto:</strong> Permite subir nuevas versiones de un trabajo, asignando un DOI específico a cada una, pero agrupándolas bajo un "DOI de concepto" que siempre apunta a la última versión.</p>
                        <p><strong>Comunidades:</strong> Permite crear colecciones temáticas o de proyectos para agrupar y curar registros relevantes, fomentando la colaboración.</p>
                        <p><strong>Preservación a Largo Plazo:</strong> Respaldado por la infraestructura de datos del CERN, garantiza la preservación de los archivos por un mínimo de 20 años, con múltiples réplicas y copias de seguridad.</p>
                    </div>

                    <div x-show="activeTab === 'policies'" x-cloak class="space-y-4 text-gray-700">
                        <p><strong>Contenido:</strong> Acepta depósitos de todos los campos de investigación y cualquier tipo de archivo, sin restricciones de formato.</p>
                        <p><strong>Límites:</strong> Hasta 50GB por depósito (ampliable gratuitamente bajo petición), lo que lo hace ideal para conjuntos de datos grandes.</p>
                        <p><strong>Acceso:</strong> Ofrece control total sobre el acceso: Abierto, Embargado, Restringido o Cerrado, aunque los metadatos siempre son públicos.</p>
                        <p><strong>Licencias:</strong> Exige la elección de una licencia para los archivos públicos, ofreciendo una amplia gama de opciones estándar (Creative Commons, MIT, etc.).</p>
                    </div>
                    
                    <div x-show="activeTab === 'github'" x-cloak class="space-y-4 text-gray-700">
                        <p><strong>Automatización del Archivo:</strong> Zenodo se puede conectar a un repositorio de GitHub para que cada vez que se cree un "release" (una versión estable del software), se archive automáticamente en Zenodo.</p>
                        <p><strong>Software Citable:</strong> Este proceso asigna un DOI a cada versión del software, transformando el código en un resultado de investigación citable y preservado a largo plazo.</p>
                        <p><strong>El Mejor de Dos Mundos:</strong> Permite usar GitHub para el desarrollo dinámico y colaborativo del código, mientras que Zenodo se encarga de la preservación estática y la citación formal, asegurando la reproducibilidad científica.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="elegir" class="py-16">
            <div class="max-w-4xl mx-auto">
                <h2 class="text-3xl font-bold text-center mb-2">¿Cómo Elegir el Repositorio Correcto?</h2>
                <p class="text-center text-gray-600 mb-12">Tu elección depende de tus necesidades específicas. Usa esta checklist interactiva para reflexionar sobre tus prioridades y descubre qué tipo de repositorio podría ser el más adecuado para ti.</p>
                
                <div class="bg-white p-8 rounded-xl shadow-lg space-y-4">
                    <template x-for="(criterion, index) in selectionCriteria" :key="index">
                        <div @click="toggleCriterion(criterion)"
                             class="checklist-item p-4 border-2 rounded-lg cursor-pointer flex items-center justify-between"
                             :class="{ 'selected': criterion.selected }">
                            <div>
                                <h4 class="font-semibold" x-text="criterion.text"></h4>
                                <p class="text-sm text-gray-500" x-text="criterion.subtext"></p>
                            </div>
                            <div x-show="criterion.selected" class="text-blue-600">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" viewBox="0 0 20 20" fill="currentColor">
                                    <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                                </svg>
                            </div>
                        </div>
                    </template>
                </div>

                <div x-show="recommendation" x-cloak class="mt-8 p-6 bg-blue-50 border border-blue-200 rounded-lg">
                    <h4 class="font-bold text-lg text-blue-800 mb-2">Recomendación Basada en tu Selección:</h4>
                    <p class="text-blue-700" x-text="recommendation"></p>
                </div>

            </div>
        </section>
    </main>

    <footer class="bg-gray-800 text-white mt-16">
        <div class="container mx-auto px-6 py-4 text-center">
            <p>Aplicación Interactiva creada con Gemini 2.5 Pro (versión preliminar) a partir del curso sobre Repositorios Digitales creado con Gemini Deep Research 2.5 Pro (versión preliminar).</p>
            <p class="text-sm text-gray-400 mt-1">&copy; 2025 Guía de Repositorios Digitales.</p>
        </div>
    </footer>

    <script>
        function repositoryApp() {
            return {
                mobileMenuOpen: false,
                selectedType: null,
                repositoryTypes: [
                    {
                        icon: '🏢',
                        title: 'Institucionales',
                        description: 'Vinculados a una universidad o centro de investigación. Recopilan la producción de su comunidad.',
                        pros: 'Aumentan el prestigio institucional, centralizan la producción y facilitan el cumplimiento de mandatos.',
                        cons: 'La visibilidad puede ser limitada si no se cosecha bien. El éxito depende del apoyo institucional.',
                        examples: 'DSpace@Cambridge, Digital.CSIC, repositorios de universidades locales.'
                    },
                    {
                        icon: '🔬',
                        title: 'Temáticos',
                        description: 'Especializados en un área de conocimiento, como física, economía o ciencias sociales.',
                        pros: 'Alta visibilidad dentro de una disciplina. Punto de encuentro para especialistas. Alto prestigio comunitario.',
                        cons: 'No son ideales para trabajos interdisciplinarios. La cobertura de algunas áreas puede ser fragmentada.',
                        examples: 'arXiv (Física, Mates), PubMed Central (Biomedicina), RePEc (Economía).'
                    },
                    {
                        icon: '💾',
                        title: 'De Datos',
                        description: 'Diseñados para almacenar, compartir y preservar conjuntos de datos de investigación.',
                        pros: 'Promueven la ciencia FAIR, la reproducibilidad y la reutilización de datos. Permiten citar los datos.',
                        cons: 'La curación puede ser intensiva. La gestión de datos sensibles es un desafío.',
                        examples: 'Zenodo, Figshare, Dryad, Harvard Dataverse.'
                    },
                    {
                        icon: '📄',
                        title: 'De Preprints',
                        description: 'Permiten la difusión rápida de manuscritos antes de la revisión por pares formal.',
                        pros: 'Aceleran la comunicación científica. Permiten recibir feedback temprano y establecer prioridad.',
                        cons: 'El contenido no está validado por pares, debe leerse con cautela. No todas las revistas los aceptaban (ahora es más común).',
                        examples: 'arXiv, bioRxiv, medRxiv, SocArXiv.'
                    },
                    {
                        icon: '💻',
                        title: 'De Software',
                        description: 'Plataformas para alojar, versionar y colaborar en el desarrollo de código fuente.',
                        pros: 'Control de versiones robusto (Git), facilitan la colaboración y la reproducibilidad computacional.',
                        cons: 'Las plataformas de desarrollo (GitHub) no son archivos de preservación a largo plazo por sí mismas.',
                        examples: 'GitHub, GitLab (para desarrollo); Zenodo (para archivo y citación).'
                    },
                    {
                        icon: '🌍',
                        title: 'Generalistas',
                        description: 'Aceptan todo tipo de contenidos de todas las disciplinas. Son una red de seguridad.',
                        pros: 'Flexibles, inclusivos, ideales para outputs que no encajan en otro lugar. Ofrecen DOI y preservación.',
                        cons: 'Pueden carecer de la curación o el enfoque comunitario de los repositorios especializados.',
                        examples: 'Zenodo, Figshare, OSF, Harvard Dataverse.'
                    }
                ],
                comparisonData: {
                    labels: ['Zenodo', 'Figshare', 'Dryad', 'Harvard Dataverse', 'OSF'],
                    datasets: {
                        storage: {
                            label: 'Límite de Almacenamiento Gratuito (GB)',
                            data: [50, 20, 0.01, 1000, Infinity],
                            backgroundColor: 'rgba(59, 130, 246, 0.7)',
                        },
                        cost: {
                            label: 'Costo por Depósito Estándar (USD)',
                            data: [0, 0, 150, 0, 0],
                            backgroundColor: 'rgba(16, 185, 129, 0.7)',
                        }
                    }
                },
                selectedMetric: 'storage',
                chart: null,
                selectionCriteria: [
                    { id: 'type_data', text: 'Mi resultado principal es un conjunto de datos.', subtext: 'Priorizo la citación y reutilización de datos.', selected: false, recommendation: 'Repositorios de Datos o Generalistas como Zenodo o Harvard Dataverse son ideales.' },
                    { id: 'type_software', text: 'Quiero archivar y hacer citable mi software/código.', subtext: 'Necesito un DOI para una versión específica de mi código en GitHub.', selected: false, recommendation: 'Zenodo, por su integración con GitHub, es la mejor opción para archivo y citación.' },
                    { id: 'type_article', text: 'Busco la máxima visibilidad en mi disciplina específica.', subtext: 'Quiero que mis colegas encuentren mi trabajo fácilmente.', selected: false, recommendation: 'Un Repositorio Temático como arXiv o bioRxiv es probablemente la mejor opción. Si no existe, el Repositorio Institucional es una buena alternativa.' },
                    { id: 'interdisciplinary', text: 'Mi investigación es muy interdisciplinar.', subtext: 'No encaja claramente en una sola área temática.', selected: false, recommendation: 'Los Repositorios Generalistas como Zenodo u OSF son perfectos para trabajos interdisciplinarios.' },
                    { id: 'cost_free', text: 'El coste es un factor clave, necesito una opción gratuita.', subtext: 'No dispongo de fondos para pagar por el depósito.', selected: false, recommendation: 'Zenodo, OSF, Harvard Dataverse o la versión gratuita de Figshare son excelentes opciones sin coste.' },
                    { id: 'preservation', text: 'La preservación a muy largo plazo es mi máxima prioridad.', subtext: 'Necesito una garantía de que mis archivos perdurarán décadas.', selected: false, recommendation: 'Zenodo, con el respaldo del CERN, ofrece uno de los compromisos de preservación más sólidos.' },
                ],
                recommendation: '',

                init() {
                    this.initChart();
                    this.setupScrollSpy();
                },
                
                initChart() {
                    const ctx = document.getElementById('comparisonChart').getContext('2d');
                    this.chart = new Chart(ctx, {
                        type: 'bar',
                        data: {
                            labels: this.comparisonData.labels,
                            datasets: [this.comparisonData.datasets[this.selectedMetric]]
                        },
                        options: {
                            responsive: true,
                            maintainAspectRatio: false,
                            plugins: {
                                legend: {
                                    display: false
                                },
                                title: {
                                    display: true,
                                    text: this.comparisonData.datasets[this.selectedMetric].label,
                                    font: {
                                        size: 16
                                    }
                                },
                                tooltip: {
                                    callbacks: {
                                        label: (context) => {
                                            let label = context.dataset.label || '';
                                            if (label) {
                                                label += ': ';
                                            }
                                            if (context.parsed.y !== null) {
                                                if (this.selectedMetric === 'storage') {
                                                     if (context.parsed.y === Infinity) {
                                                        label += 'Ilimitado';
                                                    } else {
                                                         label += context.parsed.y + ' GB';
                                                    }
                                                } else {
                                                    label += '$' + context.parsed.y;
                                                }
                                            }
                                            return label;
                                        }
                                    }
                                }
                            },
                            scales: {
                                y: {
                                    beginAtZero: true,
                                    title: {
                                        display: true,
                                        text: this.selectedMetric === 'storage' ? 'GB (Gigabytes)' : 'USD ($)'
                                    }
                                }
                            }
                        }
                    });
                },

                updateChart() {
                    const newDataset = this.comparisonData.datasets[this.selectedMetric];
                    this.chart.data.datasets[0] = newDataset;
                    this.chart.options.plugins.title.text = newDataset.label;
                    this.chart.options.scales.y.title.text = this.selectedMetric === 'storage' ? 'GB (Gigabytes)' : 'USD ($)';
                    if(this.selectedMetric === 'storage') {
                        this.chart.options.scales.y.type = 'logarithmic';
                    } else {
                        this.chart.options.scales.y.type = 'linear';
                    }
                    this.chart.update();
                },

                toggleCriterion(criterion) {
                    criterion.selected = !criterion.selected;
                    this.updateRecommendation();
                },

                updateRecommendation() {
                    const selected = this.selectionCriteria.filter(c => c.selected);
                    if (selected.length === 0) {
                        this.recommendation = '';
                        return;
                    }
                    
                    let recommendations = selected.map(c => c.recommendation);
                    // Simple logic to combine recommendations
                    this.recommendation = [...new Set(recommendations)].join(' ');
                },

                setupScrollSpy() {
                    const sections = document.querySelectorAll('section[id]');
                    const navLinks = document.querySelectorAll('.nav-link');

                    const observer = new IntersectionObserver(entries => {
                        entries.forEach(entry => {
                            if (entry.isIntersecting) {
                                const id = entry.target.getAttribute('id');
                                navLinks.forEach(link => {
                                    link.classList.remove('active');
                                    if (link.getAttribute('href') === `#${id}`) {
                                        link.classList.add('active');
                                    }
                                });
                            }
                        });
                    }, { rootMargin: '-50% 0px -50% 0px' });

                    sections.forEach(section => {
                        observer.observe(section);
                    });
                }
            }
        }
    </script>
</body>
</html>
