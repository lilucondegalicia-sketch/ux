<!-- Chosen Palette: "Research Harmony" - Base: Stone-50 (Warm Neutral). Accents: Teal (Discovery), Indigo (Definition), Rose (Evaluation), Amber (Launch). Text: Stone-800. -->

<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>La Brújula UX: Guía de Investigación</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 800px;
            margin: 0 auto;
            height: 500px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        @media (max-width: 640px) {
            .chart-container { height: 350px; }
        }
        
        /* Axis Labels Styling */
        .axis-label {
            position: absolute;
            font-size: 0.75rem;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.05em;
            color: #78716c;
            background: rgba(255, 255, 255, 0.9);
            padding: 4px 8px;
            border-radius: 4px;
            border: 1px solid #e7e5e4;
            box-shadow: 0 1px 2px rgba(0,0,0,0.05);
            pointer-events: none;
            z-index: 10;
            text-align: center;
            max-width: 120px;
        }
        .axis-top { top: 10px; left: 50%; transform: translateX(-50%); color: #4f46e5; border-color: #c7d2fe; }
        .axis-bottom { bottom: 10px; left: 50%; transform: translateX(-50%); color: #0d9488; border-color: #99f6e4; }
        .axis-left { left: 10px; top: 50%; transform: translateY(-50%); color: #be185d; border-color: #fbcfe8; }
        .axis-right { right: 10px; top: 50%; transform: translateY(-50%); color: #059669; border-color: #a7f3d0; }

        .axis-desc {
            display: block;
            font-size: 0.6rem;
            font-weight: 400;
            text-transform: none;
            margin-top: 2px;
            color: #57534e;
        }

        /* Wizard Specific Styles */
        .wizard-option { cursor: pointer; transition: all 0.2s; }
        .wizard-option:hover { border-color: #0d9488; background-color: #f0fdfa; }
        .wizard-selected { border-color: #0d9488; background-color: #ccfbf1; ring: 2px solid #0d9488; }
        
        /* Helper Box Animation */
        .fade-in { animation: fadeIn 0.5s ease-in-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(5px); } to { opacity: 1; transform: translateY(0); } }

        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
    </style>
</head>
<body class="bg-stone-50 text-stone-800 antialiased selection:bg-teal-100 selection:text-teal-900">

    <!-- Navigation -->
    <nav class="bg-white border-b border-stone-200 sticky top-0 z-50 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16">
                <div class="flex items-center">
                    <div class="flex-shrink-0 flex items-center gap-2 cursor-pointer" onclick="window.scrollTo(0,0)">
                        <span class="text-2xl">🧭</span>
                        <span class="font-bold text-xl tracking-tight text-stone-900">Brújula UX</span>
                    </div>
                </div>
                <div class="hidden md:ml-6 md:flex md:space-x-8">
                    <button onclick="scrollToSection('mindset')" class="border-transparent text-stone-500 hover:text-stone-700 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium">Mindset</button>
                    <button onclick="scrollToSection('wizard')" class="border-transparent text-teal-600 font-bold hover:text-teal-800 inline-flex items-center px-1 pt-1 border-b-2 border-teal-500 text-sm">✨ Asistente</button>
                    <button onclick="scrollToSection('radar')" class="border-transparent text-stone-500 hover:text-stone-700 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium">El Radar</button>
                    <button onclick="scrollToSection('maturity')" class="border-transparent text-stone-500 hover:text-stone-700 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium">Madurez</button>
                    <button onclick="scrollToSection('tools')" class="border-transparent text-stone-500 hover:text-stone-700 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium">Herramientas</button>
                </div>
                 <!-- Mobile Menu Button -->
                 <div class="flex items-center md:hidden">
                    <button onclick="document.getElementById('mobile-menu').classList.toggle('hidden')" class="text-stone-500 hover:text-stone-700 p-2">
                        <span class="text-2xl">☰</span>
                    </button>
                </div>
            </div>
        </div>
        <!-- Mobile Menu -->
        <div id="mobile-menu" class="hidden md:hidden bg-white border-t border-stone-200">
            <div class="pt-2 pb-4 space-y-1">
                <button onclick="scrollToSection('wizard'); document.getElementById('mobile-menu').classList.add('hidden')" class="block w-full text-left pl-3 pr-4 py-2 border-l-4 border-teal-500 text-teal-700 bg-teal-50 font-bold">✨ Asistente</button>
                <button onclick="scrollToSection('radar'); document.getElementById('mobile-menu').classList.add('hidden')" class="block w-full text-left pl-3 pr-4 py-2 border-l-4 border-transparent text-stone-600 hover:bg-stone-50">El Radar</button>
                <button onclick="scrollToSection('maturity'); document.getElementById('mobile-menu').classList.add('hidden')" class="block w-full text-left pl-3 pr-4 py-2 border-l-4 border-transparent text-stone-600 hover:bg-stone-50">Madurez</button>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <header id="mindset" class="bg-white pt-10 pb-16 lg:pt-20 lg:pb-24 relative overflow-hidden">
        <div class="absolute inset-0 opacity-10 pointer-events-none bg-[radial-gradient(#0d9488_1px,transparent_1px)] [background-size:16px_16px]"></div>
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center relative z-10">
            <div class="inline-flex items-center px-3 py-1 rounded-full bg-teal-50 text-teal-700 text-xs font-semibold uppercase tracking-wide mb-6">Guía para investigadores</div>
            <h1 class="text-4xl font-extrabold tracking-tight text-stone-900 sm:text-5xl md:text-6xl mb-6 leading-tight">
                Investigar no es un trámite.<br>
                <span class="text-transparent bg-clip-text bg-gradient-to-r from-teal-600 to-indigo-600">Es tu superpoder.</span>
            </h1>
            <p class="mt-4 max-w-2xl mx-auto text-xl text-stone-500 leading-relaxed">Antes de abrir Figma, necesitas entender el "por qué". Usa esta brújula para navegar entre métodos, validar ideas y diseñar con evidencia.</p>
            <div class="mt-8 flex justify-center gap-4">
                <button onclick="scrollToSection('wizard')" class="inline-flex items-center px-6 py-3 border border-transparent text-base font-medium rounded-full shadow-sm text-white bg-teal-600 hover:bg-teal-700 transition-all transform hover:-translate-y-1">✨ Usar el Asistente</button>
                <button onclick="scrollToSection('radar')" class="inline-flex items-center px-6 py-3 border border-stone-300 text-base font-medium rounded-full shadow-sm text-stone-700 bg-white hover:bg-stone-50 transition-all">Explorar Mapa</button>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 space-y-32">

        <!-- Detail Modal (Fixed max-height, Flexbox layout) -->
        <div id="detail-overlay" class="fixed inset-0 bg-stone-900/50 z-50 hidden backdrop-blur-sm transition-opacity" onclick="hideDetail()"></div>
        <div id="detail-modal" class="fixed top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[90%] md:w-full max-w-3xl max-h-[85vh] bg-white rounded-2xl shadow-2xl border border-stone-200 z-50 hidden flex flex-col transition-all duration-300 scale-95 opacity-0">
            <!-- Header -->
            <div class="px-8 py-6 border-b border-stone-100 flex items-start justify-between bg-stone-50/50 rounded-t-2xl flex-shrink-0">
                <div>
                    <span id="detail-tag" class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-bold uppercase tracking-wider bg-stone-100 text-stone-800 mb-3">Categoría</span>
                    <h3 id="detail-title" class="text-3xl font-extrabold text-stone-900">Título</h3>
                </div>
                <button onclick="hideDetail()" class="text-stone-400 hover:text-stone-600 hover:bg-stone-100 p-2 rounded-full transition-colors">
                    <span class="sr-only">Cerrar</span>
                    <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" /></svg>
                </button>
            </div>
            <!-- Content Body -->
            <div class="px-8 py-6 overflow-y-auto flex-1 no-scrollbar">
                <div class="grid md:grid-cols-3 gap-8">
                    <div class="md:col-span-2 space-y-6">
                        <div>
                            <h4 class="text-xs font-bold text-stone-400 uppercase tracking-widest mb-2">¿En qué consiste?</h4>
                            <p id="detail-desc" class="text-stone-700 text-lg leading-relaxed">...</p>
                        </div>
                        <div>
                            <h4 class="text-xs font-bold text-stone-400 uppercase tracking-widest mb-2">¿Cuándo te conviene usarlo?</h4>
                            <p id="detail-when" class="text-stone-600 leading-relaxed bg-amber-50 p-4 rounded-lg border border-amber-100 text-sm">...</p>
                        </div>
                    </div>
                    <div class="space-y-6">
                        <div class="bg-stone-50 rounded-xl p-5 border border-stone-100">
                            <h4 class="text-xs font-bold text-stone-400 uppercase tracking-widest mb-3">Herramientas Típicas</h4>
                            <ul id="detail-tools" class="space-y-2 text-sm text-stone-600 font-medium"></ul>
                        </div>
                        <div class="flex items-center justify-between bg-stone-50 rounded-xl p-5 border border-stone-100">
                            <h4 class="text-xs font-bold text-stone-400 uppercase tracking-widest">Esfuerzo Estimado</h4>
                            <span id="detail-effort" class="font-bold text-teal-600 bg-white px-3 py-1 rounded-md shadow-sm border border-stone-100">Bajo</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Wizard Section -->
        <section id="wizard" class="scroll-mt-24">
            <div class="max-w-5xl mx-auto">
                <div class="text-center mb-10">
                    <div class="inline-block p-3 rounded-2xl bg-teal-50 text-teal-600 mb-4 text-3xl">✨</div>
                    <h2 class="text-3xl font-bold text-stone-900 mb-4">Asistente de Navegación</h2>
                    <p class="text-stone-600 text-lg">Cuéntanos qué necesitas resolver hoy y te sugeriremos por dónde empezar.</p>
                </div>
                
                <div class="bg-white rounded-3xl shadow-xl border border-stone-200 overflow-hidden flex flex-col md:flex-row min-h-[500px]">
                    
                    <!-- Left: Questions Area -->
                    <div class="w-full md:w-2/3 p-8 md:p-12">
                        <div class="h-2 bg-stone-100 w-full mb-8 rounded-full"><div id="wizard-progress" class="h-full bg-teal-500 rounded-full transition-all duration-500" style="width: 33%"></div></div>
                        
                        <!-- Question 1 -->
                        <div id="q1" class="wizard-step fade-in">
                            <h3 class="text-2xl font-bold text-stone-900 mb-6">1. ¿Qué reto enfrentas ahora mismo?</h3>
                            <div class="grid grid-cols-1 gap-4">
                                <button onclick="selectWizardOption('q1', 'explore')" class="wizard-option p-4 rounded-xl border-2 border-stone-200 text-left hover:border-teal-400 group">
                                    <div class="flex items-center gap-4">
                                        <span class="text-3xl bg-teal-50 p-2 rounded-lg group-hover:bg-teal-100 transition-colors">🔍</span>
                                        <div>
                                            <span class="text-lg font-bold block text-stone-800">Descubrir y Entender</span>
                                            <span class="text-sm text-stone-500 block mt-1">"Aún estoy definiendo cuál es el problema real."</span>
                                        </div>
                                    </div>
                                </button>
                                <button onclick="selectWizardOption('q1', 'structure')" class="wizard-option p-4 rounded-xl border-2 border-stone-200 text-left hover:border-indigo-400 group">
                                    <div class="flex items-center gap-4">
                                        <span class="text-3xl bg-indigo-50 p-2 rounded-lg group-hover:bg-indigo-100 transition-colors">🏗️</span>
                                        <div>
                                            <span class="text-lg font-bold block text-stone-800">Organizar Información</span>
                                            <span class="text-sm text-stone-500 block mt-1">"Tengo mucho contenido y necesito ponerle orden."</span>
                                        </div>
                                    </div>
                                </button>
                                <button onclick="selectWizardOption('q1', 'validate')" class="wizard-option p-4 rounded-xl border-2 border-stone-200 text-left hover:border-rose-400 group">
                                    <div class="flex items-center gap-4">
                                        <span class="text-3xl bg-rose-50 p-2 rounded-lg group-hover:bg-rose-100 transition-colors">🧪</span>
                                        <div>
                                            <span class="text-lg font-bold block text-stone-800">Evaluar Soluciones</span>
                                            <span class="text-sm text-stone-500 block mt-1">"Ya tengo algo tangible (boceto o diseño) y quiero probarlo."</span>
                                        </div>
                                    </div>
                                </button>
                                <button onclick="selectWizardOption('q1', 'optimize')" class="wizard-option p-4 rounded-xl border-2 border-stone-200 text-left hover:border-amber-400 group">
                                    <div class="flex items-center gap-4">
                                        <span class="text-3xl bg-amber-50 p-2 rounded-lg group-hover:bg-amber-100 transition-colors">🚀</span>
                                        <div>
                                            <span class="text-lg font-bold block text-stone-800">Mejorar lo Existente</span>
                                            <span class="text-sm text-stone-500 block mt-1">"El producto ya está vivo. Quiero que crezca o rinda mejor."</span>
                                        </div>
                                    </div>
                                </button>
                            </div>
                        </div>

                        <!-- Question 2 -->
                        <div id="q2" class="wizard-step hidden fade-in">
                            <h3 id="q2-title" class="text-2xl font-bold text-stone-900 mb-6">...</h3>
                            <div id="q2-options" class="grid grid-cols-1 gap-4"></div>
                            <div class="mt-8">
                                <button onclick="resetWizard()" class="text-stone-400 hover:text-stone-600 text-sm font-medium flex items-center gap-2">
                                    <span>←</span> Volver al inicio
                                </button>
                            </div>
                        </div>

                        <!-- Results -->
                        <div id="wizard-results" class="wizard-step hidden fade-in">
                            <div class="mb-6">
                                <h3 class="text-2xl font-bold text-stone-900">Sugerencias para tu caso</h3>
                                <p class="text-stone-500">Estos métodos suelen funcionar bien para tu objetivo. Úsalos como punto de partida.</p>
                            </div>
                            <div id="recommended-methods" class="grid gap-4 text-left"></div>
                            <div class="mt-8">
                                <button onclick="resetWizard()" class="px-6 py-3 bg-stone-100 text-stone-600 rounded-full font-bold hover:bg-stone-200 transition-colors w-full">
                                    🔄 Probar con otro escenario
                                </button>
                            </div>
                        </div>
                    </div>

                    <!-- Right: Educational Guide Sidebar -->
                    <div class="w-full md:w-1/3 bg-stone-50 border-t md:border-t-0 md:border-l border-stone-200 p-8 flex flex-col">
                        <div class="mb-4 flex items-center gap-2 text-stone-400 text-xs font-bold uppercase tracking-widest">
                            <span class="text-lg">💡</span> Tip de Experto
                        </div>
                        
                        <!-- Dynamic Tip Content -->
                        <div id="wizard-tip-content" class="flex-1">
                            <h4 class="text-xl font-bold text-stone-800 mb-3">Empieza con el "Por Qué"</h4>
                            <p class="text-stone-600 leading-relaxed text-sm mb-4">
                                El error número uno es investigar sin una pregunta clara.
                            </p>
                            <p class="text-stone-600 leading-relaxed text-sm">
                                No elijas un método solo porque está de moda. Elígelo porque es la forma más sencilla de responder a tu duda actual.
                            </p>
                            <div class="mt-6 bg-white p-4 rounded-lg border border-stone-200 shadow-sm">
                                <strong class="block text-teal-600 text-xs uppercase mb-1">Recuerda</strong>
                                <p class="text-stone-700 text-sm italic">"Observar lo que la gente hace suele ser más fiable que escuchar lo que dicen."</p>
                            </div>
                        </div>
                    </div>

                </div>
            </div>
        </section>

        <!-- RADAR SECTION -->
        <section id="radar" class="scroll-mt-24 pt-12 border-t border-stone-200">
            <div class="lg:grid lg:grid-cols-12 lg:gap-12 items-center">
                <div class="lg:col-span-4 mb-10 lg:mb-0">
                    <div class="inline-block p-3 rounded-2xl bg-indigo-50 text-indigo-600 mb-4 text-3xl">🧭</div>
                    <h2 class="text-3xl font-bold text-stone-900 mb-4">1. El Radar de Métodos</h2>
                    <p class="text-stone-600 mb-6 text-lg leading-relaxed">
                        Ubícate en el mapa. ¿Buscas datos duros (Cuantitativo) o historias profundas (Cualitativo)? ¿Necesitas saber lo que dicen o lo que hacen?
                    </p>
                    <div class="bg-white p-6 rounded-2xl border border-stone-200 shadow-sm text-sm space-y-4">
                        <h3 class="font-bold text-stone-900 uppercase text-xs tracking-wider">Cómo leer el mapa</h3>
                        <div class="space-y-3">
                            <div class="flex gap-3">
                                <div class="w-8 h-8 rounded bg-indigo-50 flex items-center justify-center text-indigo-600 font-bold text-xs border border-indigo-100">↑</div>
                                <div><strong class="text-stone-900 text-xs uppercase block">Cuantitativo</strong><span class="text-stone-500 text-xs">El "Cuántos" y "Cuánto". Estadísticas.</span></div>
                            </div>
                            <div class="flex gap-3">
                                <div class="w-8 h-8 rounded bg-teal-50 flex items-center justify-center text-teal-600 font-bold text-xs border border-teal-100">↓</div>
                                <div><strong class="text-stone-900 text-xs uppercase block">Cualitativo</strong><span class="text-stone-500 text-xs">El "Por Qué" y "Cómo". Motivaciones.</span></div>
                            </div>
                            <div class="flex gap-3">
                                <div class="w-8 h-8 rounded bg-rose-50 flex items-center justify-center text-rose-600 font-bold text-xs border border-rose-100">←</div>
                                <div><strong class="text-stone-900 text-xs uppercase block">Actitudinal</strong><span class="text-stone-500 text-xs">Lo que la gente DICE. Opiniones.</span></div>
                            </div>
                            <div class="flex gap-3">
                                <div class="w-8 h-8 rounded bg-emerald-50 flex items-center justify-center text-emerald-600 font-bold text-xs border border-emerald-100">→</div>
                                <div><strong class="text-stone-900 text-xs uppercase block">Comportamiento</strong><span class="text-stone-500 text-xs">Lo que la gente HACE. Realidad.</span></div>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="lg:col-span-8 bg-white p-2 md:p-6 rounded-3xl shadow-lg border border-stone-200 relative">
                    <!-- RICH LABELS FOR CHART -->
                    <div class="chart-container">
                        <!-- Top Label -->
                        <div class="axis-label axis-top">
                            Cuantitativo
                            <span class="axis-desc">Estadísticas y Métricas</span>
                        </div>
                        <!-- Bottom Label -->
                        <div class="axis-label axis-bottom">
                            Cualitativo
                            <span class="axis-desc">Insights y 'Por Qués'</span>
                        </div>
                        <!-- Left Label -->
                        <div class="axis-label axis-left">
                            Actitudinal
                            <span class="axis-desc">Lo que dicen</span>
                        </div>
                        <!-- Right Label -->
                        <div class="axis-label axis-right">
                            Conductual
                            <span class="axis-desc">Lo que hacen</span>
                        </div>

                        <canvas id="radarChart"></canvas>
                    </div>
                    <p class="text-center text-xs text-stone-400 mt-2 font-medium uppercase tracking-widest">Haz clic en un punto para ver detalles</p>
                </div>
            </div>
        </section>

        <!-- MATURITY FRAMEWORK (NEW) -->
        <section id="maturity" class="scroll-mt-24 pt-12 border-t border-stone-200">
            <div class="text-center mb-12 max-w-3xl mx-auto">
                <div class="inline-block p-3 rounded-2xl bg-purple-50 text-purple-600 mb-4 text-3xl">🚀</div>
                <h2 class="text-3xl font-bold text-stone-900 mb-4">2. Marco de Madurez del Producto</h2>
                <p class="text-stone-600 text-lg">
                    No todos los métodos sirven en todas las etapas.
                </p>
            </div>

            <div class="grid md:grid-cols-3 gap-6">
                <!-- Stage 1 -->
                <div class="bg-white rounded-2xl border-2 border-stone-100 p-6 hover:border-teal-200 transition-colors group">
                    <div class="flex items-center gap-3 mb-4">
                        <span class="bg-teal-100 text-teal-700 font-bold px-3 py-1 rounded-full text-xs uppercase tracking-wide">Etapa Temprana</span>
                    </div>
                    <h3 class="text-xl font-bold text-stone-900 mb-2">Exploración y Concepto</h3>
                    <p class="text-stone-500 text-sm mb-6 min-h-[60px]">Aún no hay producto o hay muy pocos usuarios. El objetivo es validar si el problema existe.</p>
                    
                    <ul class="space-y-3">
                        <li class="flex items-start gap-2 cursor-pointer hover:bg-stone-50 p-2 rounded-lg" onclick="showDetail(methodsData.find(m => m.id === 'entrevistas'))">
                            <span class="text-teal-500 font-bold">•</span>
                            <div><strong class="text-stone-800 text-sm">Entrevistas</strong><p class="text-xs text-stone-400">Valida el problema.</p></div>
                        </li>
                        <li class="flex items-start gap-2 cursor-pointer hover:bg-stone-50 p-2 rounded-lg" onclick="showDetail(methodsData.find(m => m.id === 'mysteryshopper'))">
                            <span class="text-teal-500 font-bold">•</span>
                            <div><strong class="text-stone-800 text-sm">Mystery Shopper</strong><p class="text-xs text-stone-400">Analiza competencia/contexto.</p></div>
                        </li>
                        <li class="flex items-start gap-2 cursor-pointer hover:bg-stone-50 p-2 rounded-lg" onclick="showDetail(methodsData.find(m => m.id === 'netnografia'))">
                            <span class="text-teal-500 font-bold">•</span>
                            <div><strong class="text-stone-800 text-sm">Netnografía</strong><p class="text-xs text-stone-400">Entiende el lenguaje.</p></div>
                        </li>
                    </ul>
                </div>

                <!-- Stage 2 -->
                <div class="bg-white rounded-2xl border-2 border-stone-100 p-6 hover:border-indigo-200 transition-colors group">
                    <div class="flex items-center gap-3 mb-4">
                        <span class="bg-indigo-100 text-indigo-700 font-bold px-3 py-1 rounded-full text-xs uppercase tracking-wide">Etapa Intermedia</span>
                    </div>
                    <h3 class="text-xl font-bold text-stone-900 mb-2">Diseño y Validación</h3>
                    <p class="text-stone-500 text-sm mb-6 min-h-[60px]">Ya tienes prototipos o un MVP. Necesitas validar la usabilidad y estructura antes de escalar.</p>
                    
                    <ul class="space-y-3">
                        <li class="flex items-start gap-2 cursor-pointer hover:bg-stone-50 p-2 rounded-lg" onclick="showDetail(methodsData.find(m => m.id === 'heuristica'))">
                            <span class="text-indigo-500 font-bold">•</span>
                            <div><strong class="text-stone-800 text-sm">Eval. Heurística</strong><p class="text-xs text-stone-400">Limpieza rápida.</p></div>
                        </li>
                        <li class="flex items-start gap-2 cursor-pointer hover:bg-stone-50 p-2 rounded-lg" onclick="showDetail(methodsData.find(m => m.id === 'cardsorting'))">
                            <span class="text-indigo-500 font-bold">•</span>
                            <div><strong class="text-stone-800 text-sm">Card Sorting</strong><p class="text-xs text-stone-400">Organiza el menú.</p></div>
                        </li>
                        <li class="flex items-start gap-2 cursor-pointer hover:bg-stone-50 p-2 rounded-lg" onclick="showDetail(methodsData.find(m => m.id === 'usability_mod'))">
                            <span class="text-indigo-500 font-bold">•</span>
                            <div><strong class="text-stone-800 text-sm">Pruebas Moderadas</strong><p class="text-xs text-stone-400">Encuentra errores graves.</p></div>
                        </li>
                    </ul>
                </div>

                <!-- Stage 3 -->
                <div class="bg-white rounded-2xl border-2 border-stone-100 p-6 hover:border-amber-200 transition-colors group">
                    <div class="flex items-center gap-3 mb-4">
                        <span class="bg-amber-100 text-amber-700 font-bold px-3 py-1 rounded-full text-xs uppercase tracking-wide">Etapa Avanzada</span>
                    </div>
                    <h3 class="text-xl font-bold text-stone-900 mb-2">Optimización (Live)</h3>
                    <p class="text-stone-500 text-sm mb-6 min-h-[60px]">Producto en vivo con tráfico real. Buscas mejorar métricas de negocio (Conversión, Retención).</p>
                    
                    <ul class="space-y-3">
                        <li class="flex items-start gap-2 cursor-pointer hover:bg-stone-50 p-2 rounded-lg" onclick="showDetail(methodsData.find(m => m.id === 'eyetracking'))">
                            <span class="text-amber-500 font-bold">•</span>
                            <div><strong class="text-stone-800 text-sm">Eye Tracking</strong><p class="text-xs text-stone-400">Atención visual.</p></div>
                        </li>
                        <li class="flex items-start gap-2 cursor-pointer hover:bg-stone-50 p-2 rounded-lg" onclick="showDetail(methodsData.find(m => m.id === 'analytics'))">
                            <span class="text-amber-500 font-bold">•</span>
                            <div><strong class="text-stone-800 text-sm">Analítica Web</strong><p class="text-xs text-stone-400">Detecta fugas.</p></div>
                        </li>
                        <li class="flex items-start gap-2 cursor-pointer hover:bg-stone-50 p-2 rounded-lg" onclick="showDetail(methodsData.find(m => m.id === 'encuestas'))">
                            <span class="text-amber-500 font-bold">•</span>
                            <div><strong class="text-stone-800 text-sm">Encuestas (NPS)</strong><p class="text-xs text-stone-400">Mide satisfacción.</p></div>
                        </li>
                    </ul>
                </div>
            </div>
        </section>

        <!-- Tools Section -->
        <section id="tools" class="scroll-mt-24 pb-24 border-t border-stone-200 pt-24">
            <div class="text-center max-w-3xl mx-auto mb-16">
                <div class="inline-block p-3 rounded-2xl bg-stone-100 text-stone-600 mb-4 text-3xl">🧰</div>
                <h2 class="text-3xl font-bold text-stone-900 mb-4">Caja de Herramientas</h2>
                <p class="text-stone-500">Estas plataformas son solo referencias populares.</p>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                <div class="bg-white p-8 rounded-2xl border border-stone-200 shadow-sm hover:shadow-md hover:border-teal-300 transition-all">
                    <div class="flex items-center justify-between mb-6"><h3 class="font-bold text-xl text-stone-900">Maze / Useberry</h3><span class="text-2xl bg-teal-50 p-2 rounded-lg">⚡</span></div>
                    <p class="text-sm text-stone-600 mb-6">Plataformas ágiles para pruebas no moderadas. Muy útiles para validar prototipos rápidamente.</p>
                    <div class="text-xs text-stone-400 font-mono bg-stone-50 p-2 rounded">Para: Testing Rápido</div>
                </div>
                <div class="bg-white p-8 rounded-2xl border border-stone-200 shadow-sm hover:shadow-md hover:border-indigo-300 transition-all">
                    <div class="flex items-center justify-between mb-6"><h3 class="font-bold text-xl text-stone-900">Optimal Workshop</h3><span class="text-2xl bg-indigo-50 p-2 rounded-lg">🌳</span></div>
                    <p class="text-sm text-stone-600 mb-6">Especializadas en arquitectura de información (cómo organizas tu contenido).</p>
                    <div class="text-xs text-stone-400 font-mono bg-stone-50 p-2 rounded">Para: Estructura / Menús</div>
                </div>
                <div class="bg-white p-8 rounded-2xl border border-stone-200 shadow-sm hover:shadow-md hover:border-rose-300 transition-all">
                    <div class="flex items-center justify-between mb-6"><h3 class="font-bold text-xl text-stone-900">Hotjar / Analytics</h3><span class="text-2xl bg-rose-50 p-2 rounded-lg">🔥</span></div>
                    <p class="text-sm text-stone-600 mb-6">Te permiten ver la realidad (mapas de calor, grabaciones) cuando el producto ya está en vivo.</p>
                    <div class="text-xs text-stone-400 font-mono bg-stone-50 p-2 rounded">Para: Análisis Cuantitativo</div>
                </div>
            </div>
        </section>

    </main>

    <footer class="bg-stone-900 text-stone-400 py-16 mt-12 border-t border-stone-800">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
            <div class="mb-8"><span class="text-4xl">🧭</span></div>
            <p class="mb-6 text-stone-100 text-2xl font-bold max-w-2xl mx-auto leading-tight">"Un poco de investigación es infinitamente mejor que nada de investigación."</p>
        </div>
    </footer>

    <!-- JavaScript Logic -->
    <script>
        // --- Data Source ---
        const methodsData = [
            // Existing
            { id: 'netnografia', name: 'Netnografía', phase: 'descubrimiento', type: 'Qual', axisX: -8, axisY: -4, effort: 'Alto', desc: 'Bucear en foros y redes sociales para comprender dinámicas sociales y lenguaje natural.', when: 'Etapa Temprana: Para entender la cultura de tus usuarios.', tools: ['Redes Sociales', 'Foros'] },
            { id: 'entrevistas', name: 'Entrevistas 1-a-1', phase: 'descubrimiento', type: 'Qual', axisX: -9, axisY: -6, effort: 'Medio', desc: 'Conversaciones profundas para entender dolores y motivaciones reales.', when: 'Etapa Temprana: Para empatizar profundamente.', tools: ['Zoom', 'Grabadora'] },
            { id: 'shadowing', name: 'Shadowing', phase: 'descubrimiento', type: 'Qual', axisX: -7, axisY: 9, effort: 'Alto', desc: 'Observar al usuario en su entorno real (oficina, casa) sin intervenir.', when: 'Etapa Temprana: Para ver el contexto físico real.', tools: ['Cámara'] },
            { id: 'benchmark', name: 'Benchmark', phase: 'descubrimiento', type: 'Mix', axisX: 2, axisY: 5, effort: 'Bajo', desc: 'Análisis comparativo de la competencia para no reinventar la rueda.', when: 'Etapa Temprana: Para identificar estándares del sector.', tools: ['Navegador', 'Excel'] },
            { id: 'encuestas', name: 'Encuestas', phase: 'descubrimiento', type: 'Quant', axisX: 4, axisY: 3, effort: 'Bajo', desc: 'Recoger información estructurada de muchas personas (NPS, CSAT).', when: 'Etapa Avanzada: Para medir satisfacción a escala.', tools: ['Typeform'] },
            { id: 'cardsorting', name: 'Card Sorting', phase: 'definicion', type: 'Mix', axisX: -3, axisY: -2, effort: 'Medio', desc: 'Pide a los usuarios que agrupen temas. Revela cómo organizan la info en su mente.', when: 'Etapa Intermedia: Para diseñar menús intuitivos.', tools: ['Optimal Workshop'] },
            { id: 'treetesting', name: 'Tree Testing', phase: 'diseno', type: 'Quant', axisX: 6, axisY: 7, effort: 'Bajo', desc: 'Evalúa si encuentran algo en tu menú (sin diseño visual).', when: 'Etapa Intermedia: Para validar tu arquitectura de información.', tools: ['Optimal Workshop'] },
            { id: 'firstclick', name: 'First Click', phase: 'diseno', type: 'Quant', axisX: 7, axisY: 8, effort: 'Bajo', desc: 'Mide dónde hacen el primer clic los usuarios para completar una tarea.', when: 'Etapa Intermedia: Para validar si la navegación es clara.', tools: ['Maze'] },
            { id: 'usability_mod', name: 'Pruebas Moderadas', phase: 'diseno', type: 'Qual', axisX: -8, axisY: 8, effort: 'Alto', desc: 'Sesiones guiadas donde observas y preguntas. Ideales para entender "por qué" fallan.', when: 'Etapa Intermedia: Para flujos complejos o nuevos.', tools: ['Zoom'] },
            { id: 'usability_unmod', name: 'Pruebas No Moderadas', phase: 'diseno', type: 'Quant', axisX: 5, axisY: 8, effort: 'Medio', desc: 'Usuarios realizan tareas solos. Rápido y escalable.', when: 'Etapa Intermedia/Avanzada: Para validar usabilidad rápidamente.', tools: ['Maze'] },
            { id: '5second', name: '5-Second Test', phase: 'diseno', type: 'Quant', axisX: 6, axisY: -3, effort: 'Bajo', desc: 'Muestra un diseño 5 segundos y pregunta qué recuerdan.', when: 'Etapa Intermedia: Para evaluar la claridad de una Landing Page.', tools: ['UsabilityHub'] },
            { id: 'analytics', name: 'Analítica Web', phase: 'lanzamiento', type: 'Quant', axisX: 10, axisY: 10, effort: 'Medio', desc: 'Análisis de datos masivos de uso real (visitas, rebote, flujo).', when: 'Etapa Avanzada: Para optimización continua.', tools: ['GA4', 'Hotjar'] },
            { id: 'abtesting', name: 'A/B Testing', phase: 'lanzamiento', type: 'Quant', axisX: 9, axisY: 9, effort: 'Medio', desc: 'Comparar dos versiones con tráfico real para ver cuál vende más.', when: 'Etapa Avanzada: Para mejorar conversión (CRO).', tools: ['VWO'] },
            
            // New Added Methods
            { id: 'eyetracking', name: 'Eye Tracking', phase: 'lanzamiento', type: 'Quant', axisX: 9, axisY: 7, effort: 'Alto', desc: 'Registra dónde mira el usuario (fijaciones). Revela la jerarquía visual real.', when: 'Optimización: Para validar si ven los elementos clave.', tools: ['Tobii', 'Hotjar'] },
            { id: 'mysteryshopper', name: 'Mystery Shopper', phase: 'descubrimiento', type: 'Qual', axisX: 8, axisY: -6, effort: 'Medio', desc: 'Investigador actúa como cliente para evaluar la calidad del servicio.', when: 'Exploración: Para evaluar la experiencia omnicanal.', tools: ['Guion', 'Cámara oculta'] },
            { id: 'heuristica', name: 'Evaluación Heurística', phase: 'definicion', type: 'Qual', axisX: 1, axisY: 4, effort: 'Bajo', desc: 'Expertos revisan la interfaz contra principios de usabilidad (ej. Nielsen).', when: 'Validación: Limpieza rápida antes de testear con usuarios.', tools: ['Nielsen Heuristics'] }
        ];

        // --- Core Logic ---
        function scrollToSection(id) { document.getElementById(id).scrollIntoView({ behavior: 'smooth' }); }
        function showDetail(method) {
            const overlay = document.getElementById('detail-overlay');
            const modal = document.getElementById('detail-modal');
            document.getElementById('detail-title').innerText = method.name;
            document.getElementById('detail-desc').innerText = method.desc;
            document.getElementById('detail-when').innerText = method.when;
            document.getElementById('detail-effort').innerText = method.effort;
            const toolsList = document.getElementById('detail-tools');
            toolsList.innerHTML = '';
            method.tools.forEach(t => toolsList.innerHTML += `<li class="flex items-center gap-2"><span class="w-1.5 h-1.5 rounded-full bg-stone-300"></span>${t}</li>`);
            overlay.classList.remove('hidden'); modal.classList.remove('hidden');
            setTimeout(() => { overlay.classList.remove('opacity-0'); modal.classList.remove('opacity-0', 'scale-95'); modal.classList.add('opacity-100', 'scale-100'); }, 10);
        }
        function hideDetail() {
            const overlay = document.getElementById('detail-overlay');
            const modal = document.getElementById('detail-modal');
            overlay.classList.add('opacity-0'); modal.classList.remove('opacity-100', 'scale-100'); modal.classList.add('opacity-0', 'scale-95');
            setTimeout(() => { overlay.classList.add('hidden'); modal.classList.add('hidden'); }, 300);
        }

        // --- Wizard Logic ---
        let wizardState = { q1: null };
        const adviceDictionary = {
            'initial': {
                title: 'Empieza con el "Por Qué"',
                text: 'El error número uno es investigar sin una pregunta clara. No elijas un método porque está de moda; elígelo porque responde tu duda actual de la forma más sencilla.',
                quote: '"Observar lo que la gente hace es más fiable que escuchar lo que dicen que hacen."'
            },
            'explore': {
                title: 'Fase Generativa',
                text: 'En esta etapa <strong>no estamos validando nada</strong>. Estamos buscando inspiración y patrones. Si preguntas "¿Te gusta esto?", te mentirán para ser amables. Mejor pregunta: "¿Cómo solucionas este problema hoy?".',
                quote: '"Lo que la gente dice y lo que hace suelen ser cosas muy diferentes."'
            },
            'structure': {
                title: 'Arquitectura de Información',
                text: 'La estructura de tu sitio debe coincidir con cómo piensa el usuario, no con el organigrama de tu empresa. El <strong>Card Sorting</strong> te muestra sus mapas mentales.',
                quote: '"Si el usuario no puede encontrarlo, no existe."'
            },
            'validate': {
                title: 'Evaluación Formativa',
                text: 'No necesitas 100 usuarios. Con <strong>5 usuarios</strong> sueles descubrir el 85% de los problemas graves. Lo importante es iterar rápido, no hacer un estudio científico perfecto.',
                quote: '"El objetivo es mejorar el diseño, no probar que eres perfecto."'
            },
            'optimize': {
                title: 'Evaluación Sumativa',
                text: 'Aquí sí importan los números. El producto está vivo. Usa datos (Analytics, A/B) para saber <em>qué</em> pasa, y cualitativos (Encuestas) para entender <em>por qué</em>.',
                quote: '"Una mejora del 1% en conversión puede tener un gran impacto."'
            },
            'context': {
                title: 'El Contexto es Rey',
                text: 'La gente no usa tu app en el vacío. La usan mientras corren al autobús o sostienen un bebé. Métodos como el <strong>Shadowing</strong> te muestran esa realidad desordenada.',
                quote: '"Sal de la oficina y observa el mundo real."'
            },
            'talk': {
                title: 'El Arte de Preguntar',
                text: 'En las <strong>entrevistas</strong>, evita preguntar sobre el futuro ("¿Usarías esto?"). Pregunta sobre el pasado ("Cuéntame la última vez que..."). El comportamiento pasado predice el futuro.',
                quote: '"Escucha el 80% del tiempo, habla el 20%."'
            },
            'create_struct': {
                title: 'Card Sorting Abierto',
                text: 'Deja que los usuarios creen los nombres de las categorías. Descubrirás que su vocabulario es diferente al tuyo. Es vital para que los menús sean intuitivos.',
                quote: '"No corrijas al usuario. Si agrupan Tomates en Frutas, hay una razón."'
            },
            'validate_struct': {
                title: 'Tree Testing',
                text: 'Es la única forma de saber si tu menú funciona sin que el diseño visual interfiera. Si fallan aquí, ningún diseño bonito salvará la navegación.',
                quote: 'Métrica Clave: ¿Pudieron encontrarlo sin dar vueltas?'
            },
            'why_fail': {
                title: 'Pruebas Moderadas',
                text: 'Son costosas en tiempo pero oro puro en aprendizaje. El valor no es ver si completan la tarea, sino escucharles pensar en voz alta mientras intentan hacerlo.',
                quote: '"El facilitador debe ser invisible pero empático."'
            },
            'how_many': {
                title: 'Pruebas No Moderadas',
                text: 'Herramientas automáticas te permiten probar con 50 personas en una tarde. Son ideales para medir tiempos y tasas de éxito cuando ya confías en el diseño general.',
                quote: '"Testear cada semana es mejor que un gran test al final."'
            }
        };

        function updateTip(key) {
            const data = adviceDictionary[key] || adviceDictionary['initial'];
            const content = document.getElementById('wizard-tip-content');
            
            // Simple fade effect
            content.style.opacity = '0';
            setTimeout(() => {
                content.innerHTML = `
                    <h4 class="text-xl font-bold text-stone-800 mb-3">${data.title}</h4>
                    <p class="text-stone-600 leading-relaxed text-sm mb-4">${data.text}</p>
                    <div class="mt-6 bg-white p-4 rounded-lg border border-stone-200 shadow-sm">
                        <strong class="block text-teal-600 text-xs uppercase mb-1">Recuerda</strong>
                        <p class="text-stone-700 text-sm italic">${data.quote}</p>
                    </div>
                `;
                content.style.opacity = '1';
            }, 200);
        }

        function selectWizardOption(q, v) {
            wizardState[q] = v;
            document.querySelectorAll(`#${q} .wizard-option`).forEach(o => o.classList.remove('wizard-selected'));
            event.currentTarget.classList.add('wizard-selected');
            
            // Update Tip immediately
            updateTip(v);

            if(q === 'q1') { 
                document.getElementById('wizard-progress').style.width = '66%'; 
                showQ2(v); 
            } else if (q === 'q2') { 
                document.getElementById('wizard-progress').style.width = '100%'; 
                showResults(v); 
            }
        }

        function showQ2(val) {
            const q2 = document.getElementById('q2'); 
            document.getElementById('q1').classList.add('hidden'); 
            q2.classList.remove('hidden');
            
            const title = document.getElementById('q2-title'); 
            const opts = document.getElementById('q2-options');
            let html = '';

            if (val === 'explore') { 
                title.innerText = '¿Qué necesitas entender mejor?'; 
                html = `<button onclick="selectWizardOption('q2', 'context')" class="wizard-option p-4 rounded-xl border-2 border-stone-200 text-left hover:border-teal-400 group flex items-center gap-4"><span class="text-3xl">🌍</span><div><strong class="block text-stone-800">El Entorno (Contexto)</strong><span class="text-sm text-stone-500">Ver realidad física y entorno.</span></div></button>
                        <button onclick="selectWizardOption('q2', 'talk')" class="wizard-option p-4 rounded-xl border-2 border-stone-200 text-left hover:border-teal-400 group flex items-center gap-4"><span class="text-3xl">🗣️</span><div><strong class="block text-stone-800">La Persona (Mentalidad)</strong><span class="text-sm text-stone-500">Entender creencias y deseos.</span></div></button>`; 
            }
            else if (val === 'structure') { 
                title.innerText = '¿En qué punto estás?'; 
                html = `<button onclick="selectWizardOption('q2', 'create_struct')" class="wizard-option p-4 rounded-xl border-2 border-stone-200 text-left hover:border-indigo-400 group flex items-center gap-4"><span class="text-3xl">✨</span><div><strong class="block text-stone-800">Creando Estructura</strong><span class="text-sm text-stone-500">Necesito agrupar el caos.</span></div></button>
                        <button onclick="selectWizardOption('q2', 'validate_struct')" class="wizard-option p-4 rounded-xl border-2 border-stone-200 text-left hover:border-indigo-400 group flex items-center gap-4"><span class="text-3xl">✅</span><div><strong class="block text-stone-800">Probando Estructura</strong><span class="text-sm text-stone-500">Quiero ver si encuentran las cosas.</span></div></button>`; 
            }
            else if (val === 'validate') { 
                title.innerText = '¿Qué es más crítico ahora?'; 
                html = `<button onclick="selectWizardOption('q2', 'why_fail')" class="wizard-option p-4 rounded-xl border-2 border-stone-200 text-left hover:border-rose-400 group flex items-center gap-4"><span class="text-3xl">🤔</span><div><strong class="block text-stone-800">Entender el "Por Qué"</strong><span class="text-sm text-stone-500">Cualitativo / Profundidad.</span></div></button>
                        <button onclick="selectWizardOption('q2', 'how_many')" class="wizard-option p-4 rounded-xl border-2 border-stone-200 text-left hover:border-rose-400 group flex items-center gap-4"><span class="text-3xl">📊</span><div><strong class="block text-stone-800">Medir el "Cuántos"</strong><span class="text-sm text-stone-500">Cuantitativo / Rapidez.</span></div></button>`; 
            }
            else { 
                title.innerText = '¿Qué quieres optimizar?'; 
                html = `<button onclick="selectWizardOption('q2', 'behavior')" class="wizard-option p-4 rounded-xl border-2 border-stone-200 text-left hover:border-amber-400 group flex items-center gap-4"><span class="text-3xl">🖱️</span><div><strong class="block text-stone-800">Comportamiento de uso</strong><span class="text-sm text-stone-500">Dónde hacen clic, dónde se van.</span></div></button>
                        <button onclick="selectWizardOption('q2', 'conversion')" class="wizard-option p-4 rounded-xl border-2 border-stone-200 text-left hover:border-amber-400 group flex items-center gap-4"><span class="text-3xl">💰</span><div><strong class="block text-stone-800">Conversión / Ventas</strong><span class="text-sm text-stone-500">Comparar efectividad (A vs B).</span></div></button>`; 
            }
            opts.innerHTML = html;
        }

        function showResults(final) {
            document.getElementById('q2').classList.add('hidden'); 
            document.getElementById('wizard-results').classList.remove('hidden');
            const cont = document.getElementById('recommended-methods'); 
            cont.innerHTML = '';
            
            let ids = [];
            if (wizardState.q1 === 'explore') ids = final === 'context' ? ['shadowing', 'netnografia', 'mysteryshopper'] : ['entrevistas'];
            else if (wizardState.q1 === 'structure') ids = final === 'create_struct' ? ['cardsorting'] : ['treetesting'];
            else if (wizardState.q1 === 'validate') ids = final === 'why_fail' ? ['usability_mod', 'heuristica'] : ['usability_unmod', 'firstclick'];
            else ids = final === 'behavior' ? ['analytics', 'eyetracking'] : ['abtesting', 'encuestas'];
            
            ids.forEach(id => { 
                const m = methodsData.find(x => x.id === id); 
                if(m) cont.innerHTML += `
                    <div onclick="showDetail(methodsData.find(x=>x.id=='${m.id}'))" class="bg-white p-4 rounded-xl border border-stone-200 flex justify-between items-center cursor-pointer hover:shadow-md hover:border-teal-400 transition-all group">
                        <div class="flex items-center gap-4">
                            <span class="text-2xl bg-stone-50 p-2 rounded-lg group-hover:bg-teal-50">👉</span>
                            <div>
                                <strong class="text-stone-900 block text-lg">${m.name}</strong>
                                <span class="text-sm text-stone-500">${m.desc}</span>
                            </div>
                        </div>
                    </div>`; 
            });
        }

        function resetWizard() { 
            wizardState = {q1:null}; 
            document.getElementById('q1').classList.remove('hidden'); 
            document.getElementById('q2').classList.add('hidden'); 
            document.getElementById('wizard-results').classList.add('hidden'); 
            document.getElementById('wizard-progress').style.width = '33%'; 
            document.querySelectorAll('.wizard-option').forEach(o => o.classList.remove('wizard-selected')); 
            updateTip('initial');
        }

        // --- Charts ---
        const ctxRadar = document.getElementById('radarChart').getContext('2d');
        new Chart(ctxRadar, {
            type: 'scatter',
            data: { datasets: [{ label: 'Métodos', data: methodsData.map(m => ({ x: m.axisX, y: m.axisY, method: m })), backgroundColor: m => m.raw.method.type === 'Qual' ? 'rgba(20, 184, 166, 0.8)' : (m.raw.method.type === 'Quant' ? 'rgba(99, 102, 241, 0.8)' : 'rgba(168, 85, 247, 0.8)'), pointRadius: 8, pointHoverRadius: 12 }] },
            options: {
                responsive: true, maintainAspectRatio: false,
                scales: { x: { min: -11, max: 11, grid: { color: '#e7e5e4' }, ticks: { display: false } }, y: { min: -11, max: 11, grid: { color: '#e7e5e4' }, ticks: { display: false } } },
                plugins: { legend: { display: false }, tooltip: { callbacks: { label: c => c.raw.method.name }, backgroundColor: '#1c1917', padding: 12, cornerRadius: 8 } },
                onClick: (e, els) => { if(els.length) showDetail(methodsData[els[0].index]); }
            }
        });
    </script>
</body>
</html>
