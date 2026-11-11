<!DOCTYPE html>
<html lang="fr" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Karis — Le temps, en harmonie avec le vivant</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        karis: {
                            dark: '#0f0718',
                            card: '#1a102f',
                            cardHover: '#241542',
                            gold: '#d4af37',
                            goldLight: '#f3e5ab',
                            violet: '#7c3aed',
                            purpleAccent: '#9333ea',
                            textMuted: '#9ca3af'
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'system-ui', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0f0718;
            color: #f3f4f6;
        }
        .glass-panel {
            background: rgba(26, 16, 47, 0.7);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(212, 175, 55, 0.15);
        }
        .glass-gold {
            background: linear-gradient(135deg, rgba(212, 175, 55, 0.1), rgba(124, 58, 237, 0.1));
            backdrop-filter: blur(12px);
            border: 1px solid rgba(212, 175, 55, 0.3);
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #0f0718;
        }
        ::-webkit-scrollbar-thumb {
            background: #4c1d95;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #7c3aed;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between selection:bg-karis-gold selection:text-karis-dark">

    <!-- TOP HEADER -->
    <header class="glass-panel sticky top-0 z-50 px-4 py-3 border-b border-karis-gold/20 flex items-center justify-between">
        <div class="flex items-center space-x-3 cursor-pointer" onclick="switchTab('dashboard')">
            <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-karis-violet to-karis-gold flex items-center justify-center shadow-lg shadow-karis-violet/30">
                <i data-lucide="moon" class="w-5 h-5 text-karis-dark font-bold"></i>
            </div>
            <div>
                <h1 class="font-bold text-lg tracking-wide text-karis-goldLight">Karis</h1>
                <p class="text-xs text-karis-textMuted italic">Le temps, en harmonie avec le vivant</p>
            </div>
        </div>

        <div class="flex items-center space-x-2">
            <!-- Admin Button -->
            <button onclick="switchTab('admin')" class="px-3 py-1.5 rounded-lg text-xs font-medium bg-karis-violet/20 text-karis-gold border border-karis-gold/30 hover:bg-karis-violet/40 transition flex items-center space-x-1.5">
                <i data-lucide="shield" class="w-3.5 h-3.5"></i>
                <span class="hidden sm:inline">Admin</span>
            </button>
            <!-- User Status Badge -->
            <div id="userStatusBadge" class="px-3 py-1 rounded-full text-xs font-semibold bg-amber-500/10 text-karis-gold border border-karis-gold/30">
                Cercle Libre
            </div>
        </div>
    </header>

    <!-- MAIN CONTAINER -->
    <main class="flex-1 max-w-4xl w-full mx-auto px-4 py-6 mb-20">

        <!-- TAB 1: DASHBOARD (ROUE DES CYCLES & CHECK-IN) -->
        <section id="tab-dashboard" class="space-y-6">
            <!-- Welcome Banner -->
            <div class="glass-gold rounded-2xl p-6 relative overflow-hidden shadow-xl">
                <div class="absolute -right-10 -bottom-10 w-40 h-40 bg-karis-gold/10 rounded-full blur-2xl"></div>
                <div class="relative z-10">
                    <span class="text-xs uppercase tracking-widest text-karis-gold font-semibold">Cycle lunaire actuel</span>
                    <h2 class="text-2xl font-bold mt-1 text-karis-goldLight">Pleine Lune d'Ancrage</h2>
                    <p class="text-sm text-karis-textMuted mt-2">Votre énergie est en phase de culmination. Idéal pour finaliser vos projets créatifs et récolter les fruits de votre semaine.</p>
                </div>
            </div>

            <!-- Daily Check-in -->
            <div class="glass-panel rounded-2xl p-5 shadow-lg space-y-4">
                <div class="flex items-center justify-between">
                    <h3 class="font-semibold text-base text-karis-goldLight flex items-center space-x-2">
                        <i data-lucide="sun" class="w-4 h-4 text-karis-gold"></i>
                        <span>Check-in Énergétique du Matin</span>
                    </h3>
                    <span class="text-xs text-karis-textMuted" id="checkinStatus">Non effectué</span>
                </div>
                <p class="text-xs text-karis-textMuted">Comment ressentez-vous votre sève aujourd'hui ? L'application adaptera votre planning en douceur.</p>
                
                <div class="grid grid-cols-2 sm:grid-cols-4 gap-3 pt-2">
                    <button onclick="setEnergy('Feu (Créatif & Action)', 'bg-amber-500/20 text-amber-300 border-amber-500/40')" class="energy-btn p-3 rounded-xl border border-karis-gold/20 bg-karis-card hover:bg-karis-cardHover transition text-left flex flex-col justify-between space-y-2">
                        <i data-lucide="flame" class="w-5 h-5 text-amber-400"></i>
                        <div>
                            <div class="text-xs font-semibold">Feu</div>
                            <div class="text-[10px] text-karis-textMuted">Action & Élan</div>
                        </div>
                    </button>
                    <button onclick="setEnergy('Eau (Introspection)', 'bg-blue-500/20 text-blue-300 border-blue-500/40')" class="energy-btn p-3 rounded-xl border border-karis-gold/20 bg-karis-card hover:bg-karis-cardHover transition text-left flex flex-col justify-between space-y-2">
                        <i data-lucide="droplet" class="w-5 h-5 text-blue-400"></i>
                        <div>
                            <div class="text-xs font-semibold">Eau</div>
                            <div class="text-[10px] text-karis-textMuted">Réflexion & Repos</div>
                        </div>
                    </button>
                    <button onclick="setEnergy('Terre (Ancrage & Structure)', 'bg-emerald-500/20 text-emerald-300 border-emerald-500/40')" class="energy-btn p-3 rounded-xl border border-karis-gold/20 bg-karis-card hover:bg-karis-cardHover transition text-left flex flex-col justify-between space-y-2">
                        <i data-lucide="mountain" class="w-5 h-5 text-emerald-400"></i>
                        <div>
                            <div class="text-xs font-semibold">Terre</div>
                            <div class="text-[10px] text-karis-textMuted">Organisation</div>
                        </div>
                    </button>
                    <button onclick="setEnergy('Vent (Légèreté & Pause)', 'bg-purple-500/20 text-purple-300 border-purple-500/40')" class="energy-btn p-3 rounded-xl border border-karis-gold/20 bg-karis-card hover:bg-karis-cardHover transition text-left flex flex-col justify-between space-y-2">
                        <i data-lucide="wind" class="w-5 h-5 text-purple-400"></i>
                        <div>
                            <div class="text-xs font-semibold">Vent</div>
                            <div class="text-[10px] text-karis-textMuted">Souffle & Pausa</div>
                        </div>
                    </button>
                </div>
            </div>

            <!-- Circular Wheel / Productivity View -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <!-- Circular Calendar Mockup -->
                <div class="glass-panel rounded-2xl p-5 shadow-lg flex flex-col items-center justify-center text-center space-y-4">
                    <div class="relative w-40 h-40 rounded-full border-2 border-dashed border-karis-gold/40 flex items-center justify-center animate-[spin_60s_linear_infinite]">
                        <div class="absolute top-2 w-3 h-3 bg-karis-gold rounded-full"></div>
                        <div class="absolute bottom-2 w-3 h-3 bg-karis-violet rounded-full"></div>
                        <div class="absolute w-28 h-28 rounded-full border border-karis-violet/50"></div>
                    </div>
                    <div>
                        <h4 class="font-semibold text-sm text-karis-goldLight">Roue Orbitale des Saisons</h4>
                        <p class="text-xs text-karis-textMuted mt-1">Vos tâches s'alignent naturellement avec vos rythmes biologiques.</p>
                    </div>
                </div>

                <!-- Quick Actions / Features -->
                <div class="glass-panel rounded-2xl p-5 shadow-lg flex flex-col justify-between space-y-4">
                    <h4 class="font-semibold text-sm text-karis-goldLight flex items-center space-x-2">
                        <i data-lucide="sparkles" class="w-4 h-4 text-karis-gold"></i>
                        <span>Accès Rapide</span>
                    </h4>
                    <div class="space-y-2">
                        <button onclick="switchTab('ai')" class="w-full py-2.5 px-4 rounded-xl bg-karis-violet/20 hover:bg-karis-violet/30 border border-karis-violet/40 text-xs font-medium text-karis-goldLight flex items-center justify-between transition">
                            <span class="flex items-center space-x-2"><i data-lucide="bot" class="w-4 h-4 text-karis-gold"></i><span>Parler au Miroir Énergétique (IA)</span></span>
                            <i data-lucide="chevron-right" class="w-4 h-4"></i>
                        </button>
                        <button onclick="switchTab('sanctuary')" class="w-full py-2.5 px-4 rounded-xl bg-karis-card hover:bg-karis-cardHover border border-karis-gold/20 text-xs font-medium text-karis-textMuted flex items-center justify-between transition">
                            <span class="flex items-center space-x-2"><i data-lucide="heart" class="w-4 h-4 text-karis-violet"></i><span>Le Sanctuaire (Sons & Rituels)</span></span>
                            <i data-lucide="chevron-right" class="w-4 h-4"></i>
                        </button>
                        <button onclick="switchTab('pricing')" class="w-full py-2.5 px-4 rounded-xl bg-gradient-to-r from-karis-gold/20 to-karis-violet/20 hover:from-karis-gold/30 border border-karis-gold/40 text-xs font-medium text-karis-gold flex items-center justify-between transition">
                            <span class="flex items-center space-x-2"><i data-lucide="crown" class="w-4 h-4 text-karis-gold"></i><span>Passer au Cercle Complet (5000 FCFA)</span></span>
                            <i data-lucide="chevron-right" class="w-4 h-4"></i>
                        </button>
                    </div>
                </div>
            </div>
        </section>

        <!-- TAB 2: AI MIRROR (LE MIROIR ÉNERGÉTIQUE) -->
        <section id="tab-ai" class="space-y-4 hidden">
            <div class="glass-panel rounded-2xl p-5 shadow-lg flex flex-col h-[500px]">
                <div class="flex items-center justify-between pb-3 border-b border-karis-gold/20">
                    <div class="flex items-center space-x-3">
                        <div class="w-8 h-8 rounded-lg bg-karis-violet/30 flex items-center justify-center border border-karis-gold/30">
                            <i data-lucide="bot" class="w-4 h-4 text-karis-gold"></i>
                        </div>
                        <div>
                            <h3 class="font-semibold text-sm text-karis-goldLight">Le Miroir Énergétique</h3>
                            <p class="text-[10px] text-karis-textMuted">Votre guide intuitif de productivité douce</p>
                        </div>
                    </div>
                    <span class="px-2 py-0.5 rounded text-[10px] bg-emerald-500/20 text-emerald-300">En ligne</span>
                </div>

                <!-- Chat Feed -->
                <div id="chatContainer" class="flex-1 overflow-y-auto py-4 space-y-3 pr-2">
                    <div class="flex items-start space-x-2">
                        <div class="w-7 h-7 rounded-full bg-karis-violet/40 flex items-center justify-center text-xs text-karis-gold flex-shrink-0">AI</div>
                        <div class="glass-panel p-3 rounded-2xl rounded-tl-none text-xs text-karis-goldLight max-w-[80%] leading-relaxed">
                            Salutations, voyageur. Je suis ton Miroir Énergétique. Comment puis-je t'aider à alléger ou structurer ton parcours aujourd'hui ?
                        </div>
                    </div>
                </div>

                <!-- Chat Input -->
                <div class="pt-3 border-t border-karis-gold/20 flex space-x-2">
                    <input type="text" id="chatInput" placeholder="Ex: J'ai un projet de création à organiser..." class="flex-1 bg-karis-card border border-karis-gold/30 rounded-xl px-4 py-2.5 text-xs text-karis-goldLight focus:outline-none focus:border-karis-gold">
                    <button onclick="sendChatMessage()" class="bg-gradient-to-r from-karis-violet to-karis-gold text-karis-dark font-semibold px-4 py-2.5 rounded-xl text-xs hover:opacity-90 transition flex items-center justify-center">
                        <i data-lucide="send" class="w-4 h-4"></i>
                    </button>
                </div>
            </div>
        </section>

        <!-- TAB 3: SANCTUARY (BIEN-ÊTRE & RITUELS) -->
        <section id="tab-sanctuary" class="space-y-4 hidden">
            <div class="glass-gold rounded-2xl p-6 shadow-xl">
                <h3 class="text-xl font-bold text-karis-goldLight">Le Sanctuaire Intérieur</h3>
                <p class="text-xs text-karis-textMuted mt-1">Prenez 3 minutes pour souffler, méditer et réaligner votre boussole interne.</p>
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <div class="glass-panel rounded-2xl p-5 space-y-3">
                    <div class="w-10 h-10 rounded-xl bg-violet-500/20 flex items-center justify-center text-karis-gold">
                        <i data-lucide="wind" class="w-5 h-5"></i>
                    </div>
                    <h4 class="font-semibold text-sm text-karis-goldLight">Respiration Karis (4-7-8)</h4>
                    <p class="text-xs text-karis-textMuted">Un exercice guidé pour apaiser le système nerveux et retrouver l'ancrage.</p>
                    <button onclick="alert('Lancement de la session de respiration guidée de 3 minutes.')" class="w-full py-2 rounded-xl bg-karis-violet/20 hover:bg-karis-violet/30 border border-karis-gold/30 text-xs text-karis-gold font-medium transition">Commencer la session</button>
                </div>

                <div class="glass-panel rounded-2xl p-5 space-y-3">
                    <div class="w-10 h-10 rounded-xl bg-amber-500/20 flex items-center justify-center text-karis-gold">
                        <i data-lucide="volume-2" class="w-5 h-5"></i>
                    </div>
                    <h4 class="font-semibold text-sm text-karis-goldLight">Sons & Fréquences de la Nature</h4>
                    <p class="text-xs text-karis-textMuted">Pluie tropicale, feu de bois et bruits de vagues pour stimuler la concentration.</p>
                    <button onclick="alert('Lecture des paysages sonores en cours...')" class="w-full py-2 rounded-xl bg-karis-violet/20 hover:bg-karis-violet/30 border border-karis-gold/30 text-xs text-karis-gold font-medium transition">Écouter les sons</button>
                </div>
            </div>
        </section>

        <!-- TAB 4: PRICING (ABONNEMENT ORANGE MONEY) -->
        <section id="tab-pricing" class="space-y-6 hidden">
            <div class="text-center space-y-2">
                <h3 class="text-2xl font-bold text-karis-goldLight">Choisissez votre Cercle</h3>
                <p class="text-xs text-karis-textMuted">Soutenez le projet et débloquez l'intégralité de la puissance cyclique et de l'IA.</p>
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <!-- Free Tier -->
                <div class="glass-panel rounded-2xl p-6 flex flex-col justify-between space-y-4">
                    <div class="space-y-3">
                        <span class="text-xs uppercase tracking-widest text-karis-textMuted font-semibold">Découverte</span>
                        <h4 class="text-xl font-bold text-karis-goldLight">Cercle Libre</h4>
                        <div class="text-2xl font-bold text-karis-gold">0 FCFA <span class="text-xs text-karis-textMuted font-normal">/ gratuit</span></div>
                        <ul class="text-xs text-karis-textMuted space-y-2 pt-2">
                            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-3.5 h-3.5 text-karis-gold"></i><span>Calendrier lunaire de base</span></li>
                            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-3.5 h-3.5 text-karis-gold"></i><span>Check-in énergétique matinal</span></li>
                            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-3.5 h-3.5 text-karis-gold"></i><span>Accès limité au Sanctuaire</span></li>
                        </ul>
                    </div>
                    <button class="w-full py-2.5 rounded-xl bg-karis-card border border-karis-gold/20 text-xs font-semibold text-karis-textMuted cursor-default">Actuel</button>
                </div>

                <!-- Premium Tier -->
                <div class="glass-gold rounded-2xl p-6 flex flex-col justify-between space-y-4 relative overflow-hidden shadow-xl border-karis-gold/50">
                    <div class="absolute top-0 right-0 bg-gradient-to-l from-karis-gold to-karis-violet text-karis-dark text-[10px] font-bold px-3 py-1 rounded-bl-xl">POPULAIRE</div>
                    <div class="space-y-3">
                        <span class="text-xs uppercase tracking-widest text-karis-gold font-semibold">Illimité</span>
                        <h4 class="text-xl font-bold text-karis-goldLight">Cercle Complet</h4>
                        <div class="text-2xl font-bold text-karis-gold">5 000 FCFA <span class="text-xs text-karis-textMuted font-normal">/ mois</span></div>
                        <ul class="text-xs text-karis-goldLight space-y-2 pt-2">
                            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-3.5 h-3.5 text-karis-gold"></i><span>IA Miroir Énergétique Illimitée</span></li>
                            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-3.5 h-3.5 text-karis-gold"></i><span>Planification cyclique avancée des projets</span></li>
                            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-3.5 h-3.5 text-karis-gold"></i><span>Accès complet au Sanctuaire & Sons</span></li>
                        </ul>
                    </div>
                    <button onclick="openPaymentModal()" class="w-full py-2.5 rounded-xl bg-gradient-to-r from-karis-gold to-karis-violet text-karis-dark font-bold text-xs hover:opacity-90 transition shadow-lg shadow-karis-gold/20">S'abonner via Orange Money</button>
                </div>
            </div>
        </section>

        <!-- TAB 5: ADMIN DASHBOARD (GESTION PROPRIÉTAIRE) -->
        <section id="tab-admin" class="space-y-6 hidden">
            <div class="glass-gold rounded-2xl p-6 flex items-center justify-between shadow-xl">
                <div>
                    <span class="text-xs uppercase tracking-widest text-karis-gold font-semibold">Espace Propriétaire</span>
                    <h3 class="text-xl font-bold text-karis-goldLight">Tableau de Bord Administrateur</h3>
                    <p class="text-xs text-karis-textMuted mt-1">Gérez vos abonnés et validez les paiements Orange Money reçus sur le <strong>+226 04 91 10 65</strong>.</p>
                </div>
                <button onclick="addNewSubscriber()" class="px-4 py-2 bg-karis-gold text-karis-dark font-bold text-xs rounded-xl shadow hover:bg-karis-goldLight transition flex items-center space-x-1.5">
                    <i data-lucide="user-plus" class="w-4 h-4"></i>
                    <span>Ajouter un Abonné</span>
                </button>
            </div>

            <!-- Stats Grid -->
            <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                <div class="glass-panel rounded-xl p-4">
                    <div class="text-xs text-karis-textMuted">Total Abonnés</div>
                    <div class="text-2xl font-bold text-karis-goldLight mt-1" id="adminTotalUsers">12</div>
                </div>
                <div class="glass-panel rounded-xl p-4">
                    <div class="text-xs text-karis-textMuted">Chiffre d'Affaires Estimé</div>
                    <div class="text-2xl font-bold text-karis-gold mt-1" id="adminRevenue">60 000 FCFA</div>
                </div>
                <div class="glass-panel rounded-xl p-4">
                    <div class="text-xs text-karis-textMuted">Paiements en attente</div>
                    <div class="text-2xl font-bold text-amber-400 mt-1" id="adminPending">2</div>
                </div>
            </div>

            <!-- Subscribers Table -->
            <div class="glass-panel rounded-2xl p-5 shadow-lg space-y-4">
                <h4 class="font-semibold text-sm text-karis-goldLight">Liste des Utilisateurs & Statuts</h4>
                <div class="overflow-x-auto">
                    <table class="w-full text-left text-xs">
                        <thead>
                            <tr class="border-b border-karis-gold/20 text-karis-textMuted">
                                <th class="pb-3">Nom / Téléphone</th>
                                <th class="pb-3">Formule</th>
                                <th class="pb-3">Statut</th>
                                <th class="pb-3 text-right">Actions</th>
                            </tr>
                        </thead>
                        <tbody id="subscriberTableBody" class="divide-y divide-karis-gold/10">
                            <tr>
                                <td class="py-3 font-medium text-karis-goldLight">+226 70 12 34 56</td>
                                <td class="py-3">Cercle Complet (Mensuel)</td>
                                <td class="py-3"><span class="px-2 py-0.5 rounded text-[10px] bg-emerald-500/20 text-emerald-300">Actif</span></td>
                                <td class="py-3 text-right">
                                    <button onclick="toggleUserStatus(this)" class="text-xs text-karis-gold hover:underline">Suspendre</button>
                                </td>
                            </tr>
                            <tr>
                                <td class="py-3 font-medium text-karis-goldLight">+226 05 88 99 00</td>
                                <td class="py-3">Cercle Complet (Annuel)</td>
                                <td class="py-3"><span class="px-2 py-0.5 rounded text-[10px] bg-amber-500/20 text-amber-300">En attente OM</span></td>
                                <td class="py-3 text-right">
                                    <button onclick="approveUser(this)" class="text-xs text-emerald-400 font-bold hover:underline mr-2">Valider</button>
                                    <button onclick="toggleUserStatus(this)" class="text-xs text-red-400 hover:underline">Rejeter</button>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </section>

    </main>

    <!-- BOTTOM NAVIGATION BAR -->
    <nav class="glass-panel fixed bottom-0 left-0 right-0 z-40 border-t border-karis-gold/20 px-4 py-2">
        <div class="max-w-md mx-auto flex items-center justify-around">
            <button onclick="switchTab('dashboard')" class="nav-btn flex flex-col items-center space-y-1 text-karis-gold" data-target="dashboard">
                <i data-lucide="compass" class="w-5 h-5"></i>
                <span class="text-[10px]">Accueil</span>
            </button>
            <button onclick="switchTab('ai')" class="nav-btn flex flex-col items-center space-y-1 text-karis-textMuted hover:text-karis-gold transition" data-target="ai">
                <i data-lucide="bot" class="w-5 h-5"></i>
                <span class="text-[10px]">Miroir IA</span>
            </button>
            <button onclick="switchTab('sanctuary')" class="nav-btn flex flex-col items-center space-y-1 text-karis-textMuted hover:text-karis-gold transition" data-target="sanctuary">
                <i data-lucide="heart" class="w-5 h-5"></i>
                <span class="text-[10px]">Sanctuaire</span>
            </button>
            <button onclick="switchTab('pricing')" class="nav-btn flex flex-col items-center space-y-1 text-karis-textMuted hover:text-karis-gold transition" data-target="pricing">
                <i data-lucide="crown" class="w-5 h-5"></i>
                <span class="text-[10px]">Abonnement</span>
            </button>
        </div>
    </nav>

    <!-- PAYMENT MODAL -->
    <div id="paymentModal" class="fixed inset-0 z-50 bg-black/80 backdrop-blur-sm flex items-center justify-center p-4 hidden">
        <div class="glass-panel rounded-2xl p-6 max-w-sm w-full space-y-4 border border-karis-gold/40 relative">
            <button onclick="closePaymentModal()" class="absolute top-4 right-4 text-karis-textMuted hover:text-karis-gold">
                <i data-lucide="x" class="w-5 h-5"></i>
            </button>
            <h3 class="font-bold text-base text-karis-goldLight flex items-center space-x-2">
                <i data-lucide="smartphone" class="w-5 h-5 text-karis-gold"></i>
                <span>Paiement Orange Money</span>
            </h3>
            <p class="text-xs text-karis-textMuted">Pour activer votre accès <strong>Cercle Complet (5 000 FCFA)</strong>, effectuez un transfert Orange Money vers le numéro du propriétaire :</p>
            
            <div class="p-3 rounded-xl bg-karis-card border border-karis-gold/30 text-center">
                <div class="text-[10px] uppercase text-karis-textMuted">Numéro Marchand / Personnel</div>
                <div class="text-lg font-bold text-karis-gold mt-1 tracking-wider">+226 04 91 10 65</div>
            </div>

            <p class="text-[11px] text-karis-textMuted">Une fois le transfert effectué, cliquez sur le bouton ci-dessous pour envoyer la confirmation sur WhatsApp.</p>

            <a href="https://wa.me/22604911065?text=Bonjour,%20voici%20ma%20preuve%20de%20paiement%20Orange%20Money%20de%205000%20FCFA%20pour%20l'abonnement%20Karis." target="_blank" class="w-full py-3 rounded-xl bg-emerald-600 hover:bg-emerald-500 text-white font-semibold text-xs flex items-center justify-center space-x-2 transition shadow-lg">
                <i data-lucide="message-circle" class="w-4 h-4"></i>
                <span>Envoyer la preuve sur WhatsApp</span>
            </a>
        </div>
    </div>

    <!-- JAVASCRIPT LOGIC -->
    <script>
        // Initialize Lucide icons
        lucide.createIcons();

        // Navigation Switcher
        function switchTab(tabId) {
            const tabs = ['dashboard', 'ai', 'sanctuary', 'pricing', 'admin'];
            tabs.forEach(t => {
                const el = document.getElementById(`tab-${t}`);
                if (el) el.classList.add('hidden');
            });

            const activeEl = document.getElementById(`tab-${tabId}`);
            if (activeEl) activeEl.classList.remove('hidden');

            // Update bottom nav styles
            document.querySelectorAll('.nav-btn').forEach(btn => {
                if (btn.getAttribute('data-target') === tabId) {
                    btn.classList.remove('text-karis-textMuted');
                    btn.classList.add('text-karis-gold');
                } else {
                    btn.classList.remove('text-karis-gold');
                    btn.classList.add('text-karis-textMuted');
                }
            });

            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // Energy Check-in Handler
        function setEnergy(name, styleClass) {
            const status = document.getElementById('checkinStatus');
            status.textContent = `Vibrance du jour : ${name}`;
            status.className = "text-xs font-semibold px-2 py-0.5 rounded " + styleClass;
            
            // Subtle feedback
            alert(`Votre check-in "${name}" a été enregistré. Le Miroir Énergétique ajustera votre journée en conséquence.`);
        }

        // Chat Simulation
        function sendChatMessage() {
            const input = document.getElementById('chatInput');
            const container = document.getElementById('chatContainer');
            const text = input.value.trim();
            if(!text) return;

            // User bubble
            container.innerHTML += `
                <div class="flex items-start justify-end space-x-2">
                    <div class="glass-panel p-3 rounded-2xl rounded-tr-none text-xs text-karis-goldLight max-w-[80%] leading-relaxed bg-karis-violet/20 border-karis-violet/40">
                        ${text}
                    </div>
                    <div class="w-7 h-7 rounded-full bg-karis-gold/30 flex items-center justify-center text-xs text-karis-gold flex-shrink-0">Vous</div>
                </div>
            `;
            input.value = '';
            container.scrollTop = container.scrollHeight;

            // AI Response simulation
            setTimeout(() => {
                let aiReply = "J'ai bien capté ton intention. Veux-tu que nous répartissions cette tâche selon ton niveau d'énergie actuel, ou préfères-tu une pause d'ancrage d'abord ?";
                if(text.toLowerCase().includes('projet') || text.toLowerCase().includes('création')) {
                    aiReply = "C'est un magnifique élan de Feu ! Je te suggère de diviser ce projet en 3 étapes : l'intention ce matin, la structure cet après-midi, et le repos ce soir.";
                }
                container.innerHTML += `
                    <div class="flex items-start space-x-2">
                        <div class="w-7 h-7 rounded-full bg-karis-violet/40 flex items-center justify-center text-xs text-karis-gold flex-shrink-0">AI</div>
                        <div class="glass-panel p-3 rounded-2xl rounded-tl-none text-xs text-karis-goldLight max-w-[80%] leading-relaxed">
                            ${aiReply}
                        </div>
                    </div>
                `;
                container.scrollTop = container.scrollHeight;
            }, 800);
        }

        // Payment Modal Handlers
        function openPaymentModal() {
            document.getElementById('paymentModal').classList.remove('hidden');
        }
        function closePaymentModal() {
            document.getElementById('paymentModal').classList.add('hidden');
        }

        // Admin Actions
        function approveUser(btn) {
            const row = btn.closest('tr');
            const badge = row.querySelector('span');
            badge.textContent = "Actif";
            badge.className = "px-2 py-0.5 rounded text-[10px] bg-emerald-500/20 text-emerald-300";
            btn.remove();
            alert("Paiement validé avec succès ! Le compte est passé au Cercle Complet.");
        }

        function toggleUserStatus(btn) {
            const row = btn.closest('tr');
            const badge = row.querySelector('span');
            if(badge.textContent === "Actif") {
                badge.textContent = "Suspendu";
                badge.className = "px-2 py-0.5 rounded text-[10px] bg-red-500/20 text-red-300";
                btn.textContent = "Activer";
            } else {
                badge.textContent = "Actif";
                badge.className = "px-2 py-0.5 rounded text-[10px] bg-emerald-500/20 text-emerald-300";
                btn.textContent = "Suspendre";
            }
        }

        function addNewSubscriber() {
            const phone = prompt("Entrez le numéro de téléphone du nouvel abonné (ex: +226 ...) :");
            if(!phone) return;
            const tbody = document.getElementById('subscriberTableBody');
            tbody.innerHTML += `
                <tr>
                    <td class="py-3 font-medium text-karis-goldLight">${phone}</td>
                    <td class="py-3">Cercle Complet (Mensuel)</td>
                    <td class="py-3"><span class="px-2 py-0.5 rounded text-[10px] bg-emerald-500/20 text-emerald-300">Actif</span></td>
                    <td class="py-3 text-right">
                        <button onclick="toggleUserStatus(this)" class="text-xs text-karis-gold hover:underline">Suspendre</button>
                    </td>
                </tr>
            `;
            alert("Abonné ajouté avec succès !");
        }
    </script>
</body>
</html>
