<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dashboard de Análise UX</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
    <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/feather-icons/dist/feather.min.js"></script>
    <script src="https://unpkg.com/feather-icons"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        .heatmap-cell {
            background: radial-gradient(circle at 50% 50%, rgba(239,68,68,0.3), rgba(244,244,245,0.05));
            border: 1px solid rgba(38,38,38,0.6);
        }
        .custom-scrollbar::-webkit-scrollbar {
            width: 4px;
            height: 4px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #262626;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #525252;
            border-radius: 2px;
        }
    </style>
</head>
<body class="bg-gradient-to-b from-neutral-950 to-neutral-900 min-h-screen text-neutral-100">
    <div class="p-6 space-y-6">
        <header class="sticky top-0 z-40 border-b border-neutral-800 bg-neutral-950/80 backdrop-blur p-4 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div class="h-9 w-9 rounded-2xl bg-red-600 grid place-items-center font-bold">A</div>
                <div>
                    <h1 class="text-xl font-semibold tracking-tight">Dashboard de Análise UX</h1>
                    <p class="text-xs text-neutral-400">Mensuração da experiência por jornada • Últimos 90 dias</p>
                </div>
            </div>
            <button id="exportBtn" class="inline-flex items-center gap-2 rounded-2xl bg-neutral-200/10 px-3 py-2 text-sm hover:bg-neutral-200/20">
                Exportar CSV
            </button>
        </header>

        <div class="grid md:grid-cols-4 gap-4">
            <!-- KPI Cards -->
            <div class="rounded-2xl border border-neutral-800 bg-neutral-900 p-4 bg-gradient-to-br from-neutral-900 to-neutral-800 shadow-lg">
                <div class="flex items-center justify-between">
                    <div class="flex items-center gap-2 text-neutral-300">
                        <div class="h-8 w-8 rounded-xl bg-neutral-800/50 grid place-items-center border border-neutral-700">
                            <i data-feather="trending-up" class="text-emerald-400"></i>
                        </div>
                        <div class="text-xs uppercase tracking-wide">NPS</div>
                    </div>
                    <div class="text-2xl font-semibold text-emerald-400">+41</div>
                </div>
                <div class="mt-1 text-xs text-neutral-400">Tendência 90d</div>
                <div class="text-xs text-neutral-500">Últimos 90 dias</div>
            </div>
            
            <div class="rounded-2xl border border-neutral-800 bg-neutral-900 p-4 bg-gradient-to-br from-neutral-900 to-neutral-800 shadow-lg">
                <div class="flex items-center justify-between">
                    <div class="flex items-center gap-2 text-neutral-300">
                        <div class="h-8 w-8 rounded-xl bg-neutral-800/50 grid place-items-center border border-neutral-700">
                            <i data-feather="smile" class="text-blue-400"></i>
                        </div>
                        <div class="text-xs uppercase tracking-wide">CSAT médio</div>
                    </div>
                    <div class="text-2xl font-semibold text-blue-400">76%</div>
                </div>
                <div class="mt-1 text-xs text-neutral-400">Etapas críticas</div>
                <div class="text-xs text-neutral-500">Últimos 90 dias</div>
            </div>
            
            <div class="rounded-2xl border border-neutral-800 bg-neutral-900 p-4 bg-gradient-to-br from-neutral-900 to-neutral-800 shadow-lg">
                <div class="flex items-center justify-between">
                    <div class="flex items-center gap-2 text-neutral-300">
                        <div class="h-8 w-8 rounded-xl bg-neutral-800/50 grid place-items-center border border-neutral-700">
                            <i data-feather="activity" class="text-amber-400"></i>
                        </div>
                        <div class="text-xs uppercase tracking-wide">CES médio</div>
                    </div>
                    <div class="text-2xl font-semibold text-amber-400">2.6</div>
                </div>
                <div class="mt-1 text-xs text-neutral-400">1 (baixo) — 5 (alto)</div>
                <div class="text-xs text-neutral-500">Últimos 90 dias</div>
            </div>
            
            <div class="rounded-2xl border border-neutral-800 bg-neutral-900 p-4 bg-gradient-to-br from-neutral-900 to-neutral-800 shadow-lg">
                <div class="flex items-center justify-between">
                    <div class="flex items-center gap-2 text-neutral-300">
                        <div class="h-8 w-8 rounded-xl bg-neutral-800/50 grid place-items-center border border-neutral-700">
                            <i data-feather="shopping-cart" class="text-purple-400"></i>
                        </div>
                        <div class="text-xs uppercase tracking-wide">Conversão</div>
                    </div>
                    <div class="text-2xl font-semibold text-purple-400">2.9%</div>
                </div>
                <div class="mt-1 text-xs text-neutral-400">Abandono carrinho 72%</div>
                <div class="text-xs text-neutral-500">Últimos 90 dias</div>
            </div>
        </div>

        <div class="grid lg:grid-cols-3 gap-4">
            <!-- NPS Trend Chart -->
            <div class="col-span-2 rounded-2xl border border-neutral-800 bg-neutral-900 p-4">
                <h2 class="text-sm font-semibold uppercase tracking-wide text-neutral-300">NPS — Tendência</h2>
                <div class="mt-4 h-64">
                    <canvas id="npsTrendChart"></canvas>
                </div>
            </div>

            <!-- CSAT Distribution Chart -->
            <div class="rounded-2xl border border-neutral-800 bg-neutral-900 p-4">
                <h2 class="text-sm font-semibold uppercase tracking-wide text-neutral-300">CSAT — Distribuição</h2>
                <div class="mt-4 h-64">
                    <canvas id="csatPieChart"></canvas>
                </div>
            </div>
        </div>

        <div class="grid lg:grid-cols-3 gap-4">
            <!-- Funnel Chart -->
            <div class="col-span-2 rounded-2xl border border-neutral-800 bg-neutral-900 p-4">
                <div class="flex justify-between">
                    <h2 class="text-sm font-semibold uppercase tracking-wide text-neutral-300">Funil de Conversão</h2>
                    <div class="text-xs text-neutral-400">Segmento: Todos os usuários</div>
                </div>
                <div class="mt-4 h-64">
                    <canvas id="funnelChart"></canvas>
                </div>
            </div>

            <!-- Heatmap -->
            <div class="rounded-2xl border border-neutral-800 bg-neutral-900 p-4">
                <h2 class="text-sm font-semibold uppercase tracking-wide text-neutral-300">Mapa de calor — Home</h2>
                <div class="grid grid-cols-10 gap-1 mt-4">
                    <!-- Generate 60 heatmap cells -->
                    <template id="heatmap-cell">
                        <div class="heatmap-cell aspect-square rounded"></div>
                    </template>
                </div>
                <p class="mt-3 text-xs text-neutral-400">*Simulação visual baseada em densidade de cliques para apresentação no case.</p>
            </div>
        </div>

        <div class="grid lg:grid-cols-3 gap-4">
            <!-- Feedback & Research -->
            <div class="col-span-2 rounded-2xl border border-neutral-800 bg-neutral-900 p-4">
                <h2 class="text-sm font-semibold uppercase tracking-wide text-neutral-300">Feedback & Pesquisa</h2>
                <ul class="mt-3 space-y-3 max-h-64 overflow-auto pr-1 custom-scrollbar">
                    <li class="rounded-xl border border-neutral-800 bg-neutral-800/40 p-3">
                        <div class="flex justify-between items-center">
                            <span class="text-xs uppercase tracking-wide text-neutral-400">Frete</span>
                            <span class="bg-rose-500/20 text-rose-300 px-2 py-1 text-xs rounded-full">negativo</span>
                        </div>
                        <p class="mt-1 text-sm text-neutral-200">"O valor do frete aparece muito tarde, desisti no carrinho."</p>
                    </li>
                    <li class="rounded-xl border border-neutral-800 bg-neutral-800/40 p-3">
                        <div class="flex justify-between items-center">
                            <span class="text-xs uppercase tracking-wide text-neutral-400">Confiança</span>
                            <span class="bg-sky-500/20 text-sky-300 px-2 py-1 text-xs rounded-full">neutro</span>
                        </div>
                        <p class="mt-1 text-sm text-neutral-200">"Fiquei em dúvida sobre prazos, precisei voltar à página do produto."</p>
                    </li>
                    <li class="rounded-xl border border-neutral-800 bg-neutral-800/40 p-3">
                        <div class="flex justify-between items-center">
                            <span class="text-xs uppercase tracking-wide text-neutral-400">Promoções</span>
                            <span class="bg-emerald-500/20 text-emerald-300 px-2 py-1 text-xs rounded-full">positivo</span>
                        </div>
                        <p class="mt-1 text-sm text-neutral-200">"Gostei dos cupons visíveis no produto, ajudou a decidir."</p>
                    </li>
                </ul>
            </div>

            <!-- Journey Metrics -->
            <div class="rounded-2xl border border-neutral-800 bg-neutral-900 p-4">
                <h2 class="text-sm font-semibold uppercase tracking-wide text-neutral-300">Jornada & Métricas Críticas</h2>
                <ol class="mt-3 space-y-3">
                    <li class="flex items-center justify-between rounded-xl bg-neutral-800/40 p-3">
                        <div class="flex items-center gap-2">
                            <div class="grid h-8 w-8 place-items-center rounded-xl bg-neutral-700/30 text-sm font-medium">1</div>
                            <div>
                                <div class="text-sm font-medium">Home</div>
                                <div class="text-xs text-neutral-400">CES 3.1 • CSAT 80%</div>
                            </div>
                        </div>
                        <div class="text-neutral-500">→</div>
                    </li>
                    <li class="flex items-center justify-between rounded-xl bg-neutral-800/40 p-3">
                        <div class="flex items-center gap-2">
                            <div class="grid h-8 w-8 place-items-center rounded-xl bg-neutral-700/30 text-sm font-medium">2</div>
                            <div>
                                <div class="text-sm font-medium">Busca</div>
                                <div class="text-xs text-neutral-400">CES 2.8 • CSAT 72%</div>
                            </div>
                        </div>
                        <div class="text-neutral-500">→</div>
                    </li>
                    <li class="flex items-center justify-between rounded-xl bg-neutral-800/40 p-3">
                        <div class="flex items-center gap-2">
                            <div class="grid h-8 w-8 place-items-center rounded-xl bg-neutral-700/30 text-sm font-medium">3</div>
                            <div>
                                <div class="text-sm font-medium">Listagem</div>
                                <div class="text-xs text-neutral-400">CES 2.6 • CSAT 74%</div>
                            </div>
                        </div>
                        <div class="text-neutral-500">→</div>
                    </li>
                    <li class="flex items-center justify-between rounded-xl bg-neutral-800/40 p-3">
                        <div class="flex items-center gap-2">
                            <div class="grid h-8 w-8 place-items-center rounded-xl bg-neutral-700/30 text-sm font-medium">4</div>
                            <div>
                                <div class="text-sm font-medium">Produto</div>
                                <div class="text-xs text-neutral-400">CES 2.4 • CSAT 79%</div>
                            </div>
                        </div>
                        <div class="text-neutral-500">→</div>
                    </li>
                </ol>
            </div>
        </div>

        <div class="grid lg:grid-cols-3 gap-4">
            <!-- Priorities & Impact -->
            <div class="col-span-2 rounded-2xl border border-neutral-800 bg-neutral-900 p-4">
                <h2 class="text-sm font-semibold uppercase tracking-wide text-neutral-300">Prioridades & Impacto</h2>
                <div class="grid grid-cols-3 gap-4 mt-4">
                    <div class="h-[200px]">
                        <canvas id="priorityPieChart"></canvas>
                    </div>
                    <ul class="grid grid-cols-2 gap-3 col-span-2">
                        <li class="rounded-xl border border-neutral-800 bg-neutral-800/40 p-3">
                            <div class="flex items-start justify-between gap-3">
                                <div>
                                    <div class="text-sm font-medium text-neutral-100">Antecipar custo de frete na PDP</div>
                                    <div class="text-xs text-neutral-400">Reduz fricção e abandono no carrinho</div>
                                </div>
                                <div class="text-right text-xs">
                                    <div class="font-medium">Impacto: <span class="text-emerald-300">Alto</span></div>
                                    <div class="font-medium">Esforço: <span class="text-amber-300">Médio</span></div>
                                </div>
                            </div>
                        </li>
                        <li class="rounded-xl border border-neutral-800 bg-neutral-800/40 p-3">
                            <div class="flex items-start justify-between gap-3">
                                <div>
                                    <div class="text-sm font-medium text-neutral-100">Tolerância a typos na busca</div>
                                    <div class="text-xs text-neutral-400">Aumenta descoberta e CTR</div>
                                </div>
                                <div class="text-right text-xs">
                                    <div class="font-medium">Impacto: <span class="text-emerald-300">Médio</span></div>
                                    <div class="font-medium">Esforço: <span class="text-amber-300">Médio</span></div>
                                </div>
                            </div>
                        </li>
                        <li class="rounded-xl border border-neutral-800 bg-neutral-800/40 p-3">
                            <div class="flex items-start justify-between gap-3">
                                <div>
                                    <div class="text-sm font-medium text-neutral-100">Melhorar filtros de busca</div>
                                    <div class="text-xs text-neutral-400">Aumenta precisão e satisfação</div>
                                </div>
                                <div class="text-right text-xs">
                                    <div class="font-medium">Impacto: <span class="text-emerald-300">Alto</span></div>
                                    <div class="font-medium">Esforço: <span class="text-amber-300">Alto</span></div>
                                </div>
                            </div>
                        </li>
                        <li class="rounded-xl border border-neutral-800 bg-neutral-800/40 p-3">
                            <div class="flex items-start justify-between gap-3">
                                <div>
                                    <div class="text-sm font-medium text-neutral-100">Otimizar carregamento de imagens</div>
                                    <div class="text-xs text-neutral-400">Melhora performance e experiência</div>
                                </div>
                                <div class="text-right text-xs">
                                    <div class="font-medium">Impacto: <span class="text-emerald-300">Médio</span></div>
                                    <div class="font-medium">Esforço: <span class="text-amber-300">Baixo</span></div>
                                </div>
                            </div>
                        </li>
                        <li class="rounded-xl border border-neutral-800 bg-neutral-800/40 p-3">
                            <div class="flex items-start justify-between gap-3">
                                <div>
                                    <div class="text-sm font-medium text-neutral-100">Adicionar avaliações de produtos</div>
                                    <div class="text-xs text-neutral-400">Aumenta confiança e conversão</div>
                                </div>
                                <div class="text-right text-xs">
                                    <div class="font-medium">Impacto: <span class="text-emerald-300">Alto</span></div>
                                    <div class="font-medium">Esforço: <span class="text-amber-300">Médio</span></div>
                                </div>
                            </div>
                        </li>
                        <li class="rounded-xl border border-neutral-800 bg-neutral-800/40 p-3">
                            <div class="flex items-start justify-between gap-3">
                                <div>
                                    <div class="text-sm font-medium text-neutral-100">Implementar chat ao vivo</div>
                                    <div class="text-xs text-neutral-400">Reduz dúvidas e aumenta conversão</div>
                                </div>
                                <div class="text-right text-xs">
                                    <div class="font-medium">Impacto: <span class="text-emerald-300">Alto</span></div>
                                    <div class="font-medium">Esforço: <span class="text-amber-300">Alto</span></div>
                                </div>
                            </div>
                        </li>
                        <li class="rounded-xl border border-neutral-800 bg-neutral-800/40 p-3">
                            <div class="flex items-start justify-between gap-3">
                                <div>
                                    <div class="text-sm font-medium text-neutral-100">Melhorar busca por voz</div>
                                    <div class="text-xs text-neutral-400">Aumenta acessibilidade e usabilidade</div>
                                </div>
                                <div class="text-right text-xs">
                                    <div class="font-medium">Impacto: <span class="text-emerald-300">Médio</span></div>
                                    <div class="font-medium">Esforço: <span class="text-amber-300">Médio</span></div>
                                </div>
                            </div>
                        </li>
                        <li class="rounded-xl border border-neutral-800 bg-neutral-800/40 p-3">
                            <div class="flex items-start justify-between gap-3">
                                <div>
                                    <div class="text-sm font-medium text-neutral-100">Adicionar modo escuro</div>
                                    <div class="text-xs text-neutral-400">Melhora experiência visual noturna</div>
                                </div>
                                <div class="text-right text-xs">
                                    <div class="font-medium">Impacto: <span class="text-emerald-300">Médio</span></div>
                                    <div class="font-medium">Esforço: <span class="text-amber-300">Baixo</span></div>
                                </div>
                            </div>
                        </li>
                        <li class="rounded-xl border border-neutral-800 bg-neutral-800/40 p-3">
                            <div class="flex items-start justify-between gap-3">
                                <div>
                                    <div class="text-sm font-medium text-neutral-100">Otimizar para mobile</div>
                                    <div class="text-xs text-neutral-400">Melhora experiência em dispositivos móveis</div>
                                </div>
                                <div class="text-right text-xs">
                                    <div class="font-medium">Impacto: <span class="text-emerald-300">Alto</span></div>
                                    <div class="font-medium">Esforço: <span class="text-amber-300">Alto</span></div>
                                </div>
                            </div>
                        </li>
                    </ul>
                </div>
            </div>
        </div>

        <!-- Additional space to fill the page -->
        <div class="h-24"></div>
    </div>

    <script>
        // Initialize AOS and Feather Icons
        AOS.init();
        feather.replace();

        // Generate heatmap cells
        const heatmapContainer = document.querySelector('.grid-cols-10');
        for (let i = 0; i < 60; i++) {
            const cell = document.createElement('div');
            cell.className = 'heatmap-cell aspect-square rounded';
            const opacity = (Math.random() * 0.5 + 0.1).toFixed(2);
            cell.style.background = `radial-gradient(circle at 50% 50%, rgba(239,68,68,${opacity}), rgba(244,244,245,0.05))`;
            cell.style.border = '1px solid rgba(38,38,38,0.6)';
            heatmapContainer.appendChild(cell);
        }

        // NPS Trend Chart
        const npsCtx = document.getElementById('npsTrendChart').getContext('2d');
        new Chart(npsCtx, {
            type: 'line',
            data: {
                labels: ['Jul', 'Ago', 'Set'],
                datasets: [{
                    label: 'NPS',
                    data: [35, 42, 41],
                    borderColor: '#22c55e',
                    backgroundColor: 'rgba(34, 197, 94, 0.1)',
                    borderWidth: 2,
                    tension: 0.1,
                    fill: true
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                scales: {
                    y: {
                        grid: {
                            color: '#262626'
                        },
                        ticks: {
                            color: '#666'
                        }
                    },
                    x: {
                        grid: {
                            color: '#262626'
                        },
                        ticks: {
                            color: '#666'
                        }
                    }
                },
                plugins: {
                    legend: {
                        display: false
                    }
                }
            }
        });

        // CSAT Pie Chart
        const csatCtx = document.getElementById('csatPieChart').getContext('2d');
        new Chart(csatCtx, {
            type: 'pie',
            data: {
                labels: ['Satisfeitos', 'Insatisfeitos'],
                datasets: [{
                    data: [76, 24],
                    backgroundColor: ['#22c55e', '#0ea5e9'],
                    borderWidth: 0
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        position: 'right',
                        labels: {
                            color: '#f5f5f5'
                        }
                    }
                }
            }
        });

        // Funnel Chart
        const funnelCtx = document.getElementById('funnelChart').getContext('2d');
        new Chart(funnelCtx, {
            type: 'bar',
            data: {
                labels: ['Home', 'Busca', 'Listagem', 'Produto', 'Carrinho', 'Checkout', 'Compra'],
                datasets: [{
                    label: 'Usuários',
                    data: [100000, 72000, 52000, 31000, 10200, 2900, 2900],
                    backgroundColor: '#3b82f6',
                    borderRadius: 6
                }]
            },
            options: {
                indexAxis: 'y',
                responsive: true,
                maintainAspectRatio: false,
                scales: {
                    x: {
                        grid: {
                            color: '#262626'
                        },
                        ticks: {
                            color: '#666'
                        }
                    },
                    y: {
                        grid: {
                            color: '#262626'
                        },
                        ticks: {
                            color: '#666'
                        }
                    }
                },
                plugins: {
                    legend: {
                        display: false
                    }
                }
            }
        });

        // Priority Pie Chart
        const priorityCtx = document.getElementById('priorityPieChart').getContext('2d');
        new Chart(priorityCtx, {
            type: 'pie',
            data: {
                labels: ['Alto', 'Médio', 'Baixo'],
                datasets: [{
                    data: [50, 30, 20],
                    backgroundColor: ['#22c55e', '#f59e0b', '#ef4444'],
                    borderWidth: 0
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        position: 'right',
                        labels: {
                            color: '#f5f5f5'
                        }
                    }
                }
            }
        });

        // Export CSV functionality
        document.getElementById('exportBtn').addEventListener('click', function() {
            const csvContent = [
                ['Métrica', 'Valor', 'Descrição'],
                ['NPS', '+41', 'Tendência 90d'],
                ['CSAT médio', '76%', 'Etapas críticas'],
                ['CES médio', '2.6', '1 (baixo) — 5 (alto)'],
                ['Conversão', '2.9%', 'Abandono carrinho 72%']
            ].map(e => e.join(',')).join('\n');

            const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement('a');
            link.href = url;
            link.setAttribute('download', 'dashboard-ux-americanas.csv');
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        });
    </script>
</body>
</html>
