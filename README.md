<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ciclo de Estudos</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #f0f4f8;
        }
        .gradient-bg {
            background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
        }
        .card {
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
        }
        .animate-pulse-slow {
            animation: pulse 3s cubic-bezier(0.4, 0, 0.6, 1) infinite;
        }
        @keyframes pulse {
            0%, 100% {
                opacity: 1;
            }
            50% {
                opacity: 0.7;
            }
        }
        .chart-bar {
            transition: height 1s ease;
        }
        .tab-active {
            border-bottom: 3px solid #6366f1;
            color: #6366f1;
            font-weight: 600;
        }
        .modal {
            transition: opacity 0.3s ease, transform 0.3s ease;
        }
        .modal-enter {
            opacity: 0;
            transform: translateY(-20px);
        }
        .modal-enter-active {
            opacity: 1;
            transform: translateY(0);
        }
        .modal-exit {
            opacity: 1;
            transform: translateY(0);
        }
        .modal-exit-active {
            opacity: 0;
            transform: translateY(-20px);
        }
        .toast {
            animation: slideIn 0.5s ease forwards, fadeOut 0.5s ease 2.5s forwards;
            transform: translateX(100%);
            opacity: 0;
        }
        @keyframes slideIn {
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }
        @keyframes fadeOut {
            to {
                opacity: 0;
                transform: translateY(-20px);
            }
        }
        .progress-ring-circle {
            transition: stroke-dashoffset 0.5s ease;
            transform: rotate(-90deg);
            transform-origin: 50% 50%;
        }
    </style>
</head>
<body>
    <div id="app" class="min-h-screen flex flex-col">
        <!-- Header -->
        <header class="gradient-bg text-white p-4 shadow-lg">
            <div class="container mx-auto flex justify-between items-center">
                <h1 class="text-2xl font-bold">Ciclo de Estudos</h1>
                <div class="flex items-center space-x-2">
                    <button id="settingsBtn" class="p-2 rounded-full hover:bg-white/20 transition">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                        </svg>
                    </button>
                    <button id="dataBtn" class="p-2 rounded-full hover:bg-white/20 transition">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 7v10c0 2.21 3.582 4 8 4s8-1.79 8-4V7M4 7c0 2.21 3.582 4 8 4s8-1.79 8-4M4 7c0-2.21 3.582-4 8-4s8 1.79 8 4m0 5c0 2.21-3.582 4-8 4s-8-1.79-8-4" />
                        </svg>
                    </button>
                </div>
            </div>
        </header>

        <!-- Main Content -->
        <main class="flex-grow container mx-auto p-4">
            <!-- Tabs -->
            <div class="flex border-b border-gray-200 mb-6">
                <button id="tabDashboard" class="px-4 py-2 tab-active">Dashboard</button>
                <button id="tabSubjects" class="px-4 py-2 text-gray-500">Matérias</button>
                <button id="tabStats" class="px-4 py-2 text-gray-500">Estatísticas</button>
            </div>

            <!-- Dashboard Tab -->
            <div id="dashboardContent" class="tab-content">
                <!-- Today's Summary -->
                <div class="mb-8">
                    <h2 class="text-xl font-semibold mb-4 text-gray-800">Resumo de Hoje</h2>
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                        <div class="bg-white rounded-lg shadow p-6 card">
                            <div class="flex items-center justify-between">
                                <div>
                                    <p class="text-sm text-gray-500">Tempo Estudado Hoje</p>
                                    <p id="todayTime" class="text-2xl font-bold text-indigo-600">0h 0min</p>
                                </div>
                                <div class="bg-indigo-100 p-3 rounded-full">
                                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-indigo-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                                    </svg>
                                </div>
                            </div>
                            <div class="mt-4">
                                <div class="w-full bg-gray-200 rounded-full h-2.5">
                                    <div id="todayProgress" class="bg-indigo-600 h-2.5 rounded-full" style="width: 0%"></div>
                                </div>
                                <p id="todayProgressText" class="text-xs text-gray-500 mt-1">0% da meta diária</p>
                            </div>
                        </div>

                        <div class="bg-white rounded-lg shadow p-6 card">
                            <div class="flex items-center justify-between">
                                <div>
                                    <p class="text-sm text-gray-500">Matérias Estudadas Hoje</p>
                                    <p id="todaySubjects" class="text-2xl font-bold text-purple-600">0</p>
                                </div>
                                <div class="bg-purple-100 p-3 rounded-full">
                                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-purple-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253" />
                                    </svg>
                                </div>
                            </div>
                        </div>

                        <div class="bg-white rounded-lg shadow p-6 card">
                            <div class="flex items-center justify-between">
                                <div>
                                    <p class="text-sm text-gray-500">Ciclo Atual</p>
                                    <p id="currentCycle" class="text-2xl font-bold text-blue-600">Dia 0</p>
                                </div>
                                <div class="bg-blue-100 p-3 rounded-full">
                                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
                                    </svg>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Quick Actions -->
                <div class="mb-8">
                    <h2 class="text-xl font-semibold mb-4 text-gray-800">Ações Rápidas</h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <button id="startStudyBtn" class="bg-indigo-600 hover:bg-indigo-700 text-white font-medium py-3 px-4 rounded-lg shadow transition flex items-center justify-center">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14.752 11.168l-3.197-2.132A1 1 0 0010 9.87v4.263a1 1 0 001.555.832l3.197-2.132a1 1 0 000-1.664z" />
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                            </svg>
                            Iniciar Sessão de Estudo
                        </button>
                        <button id="addSubjectBtn" class="bg-white border border-gray-300 hover:bg-gray-50 text-gray-700 font-medium py-3 px-4 rounded-lg shadow transition flex items-center justify-center">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2 text-indigo-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
                            </svg>
                            Adicionar Nova Matéria
                        </button>
                    </div>
                </div>

                <!-- Recent Activity -->
                <div>
                    <h2 class="text-xl font-semibold mb-4 text-gray-800">Atividade Recente</h2>
                    <div class="bg-white rounded-lg shadow overflow-hidden">
                        <div id="recentActivityList" class="divide-y divide-gray-200">
                            <div class="p-4 text-center text-gray-500">
                                Nenhuma atividade recente para mostrar.
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Subjects Tab -->
            <div id="subjectsContent" class="tab-content hidden">
                <div class="flex justify-between items-center mb-6">
                    <h2 class="text-xl font-semibold text-gray-800">Suas Matérias</h2>
                    <button id="addSubjectBtnTab" class="bg-indigo-600 hover:bg-indigo-700 text-white font-medium py-2 px-4 rounded-lg shadow transition flex items-center">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
                        </svg>
                        Nova Matéria
                    </button>
                </div>

                <div id="subjectsList" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
                    <div class="bg-white rounded-lg shadow p-6 text-center text-gray-500">
                        Nenhuma matéria cadastrada. Clique em "Nova Matéria" para começar.
                    </div>
                </div>
            </div>

            <!-- Stats Tab -->
            <div id="statsContent" class="tab-content hidden">
                <h2 class="text-xl font-semibold mb-6 text-gray-800">Estatísticas de Estudo</h2>
                
                <!-- Time Distribution -->
                <div class="bg-white rounded-lg shadow p-6 mb-6">
                    <h3 class="text-lg font-medium mb-4 text-gray-700">Distribuição de Tempo por Matéria</h3>
                    <div id="timeDistributionChart" class="h-64 flex items-end justify-around">
                        <!-- Chart bars will be added here -->
                    </div>
                </div>

                <!-- Weekly Progress -->
                <div class="bg-white rounded-lg shadow p-6 mb-6">
                    <h3 class="text-lg font-medium mb-4 text-gray-700">Progresso Semanal</h3>
                    <div id="weeklyProgressChart" class="h-64 flex items-end justify-around">
                        <!-- Chart bars will be added here -->
                    </div>
                </div>

                <!-- Overall Stats -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div class="bg-white rounded-lg shadow p-6 card">
                        <p class="text-sm text-gray-500">Tempo Total de Estudo</p>
                        <p id="totalStudyTime" class="text-2xl font-bold text-indigo-600">0h 0min</p>
                    </div>
                    <div class="bg-white rounded-lg shadow p-6 card">
                        <p class="text-sm text-gray-500">Média Diária</p>
                        <p id="dailyAverage" class="text-2xl font-bold text-purple-600">0h 0min</p>
                    </div>
                    <div class="bg-white rounded-lg shadow p-6 card">
                        <p class="text-sm text-gray-500">Dias Consecutivos</p>
                        <p id="consecutiveDays" class="text-2xl font-bold text-blue-600">0 dias</p>
                    </div>
                </div>
            </div>
        </main>

        <!-- Footer -->
        <footer class="bg-white border-t border-gray-200 py-4">
            <div class="container mx-auto px-4 text-center text-gray-500 text-sm">
                &copy; 2023 Ciclo de Estudos | Desenvolvido com ❤️
            </div>
        </footer>
    </div>

    <!-- Modals -->
    <!-- Add Subject Modal -->
    <div id="addSubjectModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg shadow-xl p-6 w-full max-w-md mx-4 modal modal-enter">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-lg font-semibold text-gray-800">Adicionar Nova Matéria</h3>
                <button class="closeModal text-gray-400 hover:text-gray-600">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>
            </div>
            <form id="addSubjectForm">
                <div class="mb-4">
                    <label for="subjectName" class="block text-sm font-medium text-gray-700 mb-1">Nome da Matéria</label>
                    <input type="text" id="subjectName" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" required>
                </div>
                <div class="mb-4">
                    <label for="subjectColor" class="block text-sm font-medium text-gray-700 mb-1">Cor</label>
                    <div class="flex space-x-2">
                        <div class="color-option cursor-pointer w-8 h-8 rounded-full bg-red-500" data-color="#ef4444"></div>
                        <div class="color-option cursor-pointer w-8 h-8 rounded-full bg-orange-500" data-color="#f97316"></div>
                        <div class="color-option cursor-pointer w-8 h-8 rounded-full bg-amber-500" data-color="#f59e0b"></div>
                        <div class="color-option cursor-pointer w-8 h-8 rounded-full bg-green-500" data-color="#22c55e"></div>
                        <div class="color-option cursor-pointer w-8 h-8 rounded-full bg-teal-500" data-color="#14b8a6"></div>
                        <div class="color-option cursor-pointer w-8 h-8 rounded-full bg-blue-500" data-color="#3b82f6"></div>
                        <div class="color-option cursor-pointer w-8 h-8 rounded-full bg-indigo-500" data-color="#6366f1"></div>
                        <div class="color-option cursor-pointer w-8 h-8 rounded-full bg-purple-500" data-color="#a855f7"></div>
                        <div class="color-option cursor-pointer w-8 h-8 rounded-full bg-pink-500" data-color="#ec4899"></div>
                    </div>
                    <input type="hidden" id="subjectColor" value="#6366f1" required>
                </div>
                <div class="mb-4">
                    <label for="subjectPriority" class="block text-sm font-medium text-gray-700 mb-1">Prioridade</label>
                    <select id="subjectPriority" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">
                        <option value="high">Alta</option>
                        <option value="medium" selected>Média</option>
                        <option value="low">Baixa</option>
                    </select>
                </div>
                <div class="mb-4">
                    <label for="subjectGoal" class="block text-sm font-medium text-gray-700 mb-1">Meta de Tempo Diário (minutos)</label>
                    <input type="number" id="subjectGoal" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" min="1" value="60" required>
                </div>
                <div class="flex justify-end space-x-2">
                    <button type="button" class="closeModal px-4 py-2 border border-gray-300 rounded-md text-gray-700 hover:bg-gray-50">Cancelar</button>
                    <button type="submit" class="px-4 py-2 bg-indigo-600 text-white rounded-md hover:bg-indigo-700">Adicionar</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Edit Subject Modal -->
    <div id="editSubjectModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg shadow-xl p-6 w-full max-w-md mx-4 modal modal-enter">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-lg font-semibold text-gray-800">Editar Matéria</h3>
                <button class="closeModal text-gray-400 hover:text-gray-600">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>
            </div>
            <form id="editSubjectForm">
                <input type="hidden" id="editSubjectId">
                <div class="mb-4">
                    <label for="editSubjectName" class="block text-sm font-medium text-gray-700 mb-1">Nome da Matéria</label>
                    <input type="text" id="editSubjectName" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" required>
                </div>
                <div class="mb-4">
                    <label for="editSubjectColor" class="block text-sm font-medium text-gray-700 mb-1">Cor</label>
                    <div class="flex space-x-2">
                        <div class="edit-color-option cursor-pointer w-8 h-8 rounded-full bg-red-500" data-color="#ef4444"></div>
                        <div class="edit-color-option cursor-pointer w-8 h-8 rounded-full bg-orange-500" data-color="#f97316"></div>
                        <div class="edit-color-option cursor-pointer w-8 h-8 rounded-full bg-amber-500" data-color="#f59e0b"></div>
                        <div class="edit-color-option cursor-pointer w-8 h-8 rounded-full bg-green-500" data-color="#22c55e"></div>
                        <div class="edit-color-option cursor-pointer w-8 h-8 rounded-full bg-teal-500" data-color="#14b8a6"></div>
                        <div class="edit-color-option cursor-pointer w-8 h-8 rounded-full bg-blue-500" data-color="#3b82f6"></div>
                        <div class="edit-color-option cursor-pointer w-8 h-8 rounded-full bg-indigo-500" data-color="#6366f1"></div>
                        <div class="edit-color-option cursor-pointer w-8 h-8 rounded-full bg-purple-500" data-color="#a855f7"></div>
                        <div class="edit-color-option cursor-pointer w-8 h-8 rounded-full bg-pink-500" data-color="#ec4899"></div>
                    </div>
                    <input type="hidden" id="editSubjectColor" required>
                </div>
                <div class="mb-4">
                    <label for="editSubjectPriority" class="block text-sm font-medium text-gray-700 mb-1">Prioridade</label>
                    <select id="editSubjectPriority" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">
                        <option value="high">Alta</option>
                        <option value="medium">Média</option>
                        <option value="low">Baixa</option>
                    </select>
                </div>
                <div class="mb-4">
                    <label for="editSubjectGoal" class="block text-sm font-medium text-gray-700 mb-1">Meta de Tempo Diário (minutos)</label>
                    <input type="number" id="editSubjectGoal" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" min="1" required>
                </div>
                <div class="flex justify-between">
                    <button type="button" id="deleteSubjectBtn" class="px-4 py-2 bg-red-600 text-white rounded-md hover:bg-red-700">Excluir</button>
                    <div class="flex space-x-2">
                        <button type="button" class="closeModal px-4 py-2 border border-gray-300 rounded-md text-gray-700 hover:bg-gray-50">Cancelar</button>
                        <button type="submit" class="px-4 py-2 bg-indigo-600 text-white rounded-md hover:bg-indigo-700">Salvar</button>
                    </div>
                </div>
            </form>
        </div>
    </div>

    <!-- Study Session Modal -->
    <div id="studySessionModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg shadow-xl p-6 w-full max-w-md mx-4 modal modal-enter">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-lg font-semibold text-gray-800">Iniciar Sessão de Estudo</h3>
                <button class="closeModal text-gray-400 hover:text-gray-600">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>
            </div>
            <form id="studySessionForm">
                <div class="mb-4">
                    <label for="sessionSubject" class="block text-sm font-medium text-gray-700 mb-1">Matéria</label>
                    <select id="sessionSubject" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" required>
                        <option value="" disabled selected>Selecione uma matéria</option>
                    </select>
                </div>
                <div class="mb-4">
                    <label for="sessionDuration" class="block text-sm font-medium text-gray-700 mb-1">Duração (minutos)</label>
                    <input type="number" id="sessionDuration" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" min="1" value="30" required>
                </div>
                <div class="mb-4">
                    <label for="sessionNotes" class="block text-sm font-medium text-gray-700 mb-1">Notas (opcional)</label>
                    <textarea id="sessionNotes" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" rows="3"></textarea>
                </div>
                <div class="flex justify-end space-x-2">
                    <button type="button" class="closeModal px-4 py-2 border border-gray-300 rounded-md text-gray-700 hover:bg-gray-50">Cancelar</button>
                    <button type="submit" class="px-4 py-2 bg-indigo-600 text-white rounded-md hover:bg-indigo-700">Iniciar</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Active Study Session Modal -->
    <div id="activeSessionModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg shadow-xl p-6 w-full max-w-md mx-4 modal modal-enter">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-lg font-semibold text-gray-800">Sessão de Estudo em Andamento</h3>
                <button id="minimizeSessionBtn" class="text-gray-400 hover:text-gray-600">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                    </svg>
                </button>
            </div>
            <div class="text-center mb-6">
                <p id="activeSubjectName" class="text-xl font-medium mb-2">Matéria</p>
                <div class="flex justify-center mb-4">
                    <svg class="w-32 h-32">
                        <circle class="text-gray-200" stroke-width="10" stroke="currentColor" fill="transparent" r="58" cx="64" cy="64"/>
                        <circle id="progressRing" class="progress-ring-circle text-indigo-600" stroke-width="10" stroke="currentColor" fill="transparent" r="58" cx="64" cy="64" stroke-dasharray="364.4" stroke-dashoffset="364.4"/>
                    </svg>
                    <div class="absolute mt-10">
                        <p id="timerDisplay" class="text-3xl font-bold">00:00</p>
                    </div>
                </div>
                <p id="sessionProgress" class="text-sm text-gray-500">0% concluído</p>
            </div>
            <div class="flex justify-between space-x-2">
                <button id="pauseResumeBtn" class="flex-1 px-4 py-2 bg-yellow-500 text-white rounded-md hover:bg-yellow-600">
                    <span id="pauseResumeText">Pausar</span>
                </button>
                <button id="finishSessionBtn" class="flex-1 px-4 py-2 bg-red-600 text-white rounded-md hover:bg-red-700">Finalizar</button>
            </div>
        </div>
    </div>

    <!-- Minimized Session Indicator -->
    <div id="minimizedSession" class="fixed bottom-4 right-4 bg-indigo-600 text-white rounded-lg shadow-lg p-4 hidden cursor-pointer">
        <div class="flex items-center">
            <div class="mr-3">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 animate-pulse-slow" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
            </div>
            <div>
                <p class="font-medium">Sessão em andamento</p>
                <p id="minimizedTimer" class="text-sm">00:00</p>
            </div>
        </div>
    </div>

    <!-- Settings Modal -->
    <div id="settingsModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg shadow-xl p-6 w-full max-w-md mx-4 modal modal-enter">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-lg font-semibold text-gray-800">Configurações</h3>
                <button class="closeModal text-gray-400 hover:text-gray-600">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>
            </div>
            <form id="settingsForm">
                <div class="mb-4">
                    <label for="dailyGoal" class="block text-sm font-medium text-gray-700 mb-1">Meta Diária (minutos)</label>
                    <input type="number" id="dailyGoal" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" min="1" value="120" required>
                </div>
                <div class="mb-4">
                    <label for="cycleLength" class="block text-sm font-medium text-gray-700 mb-1">Duração do Ciclo (dias)</label>
                    <input type="number" id="cycleLength" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" min="1" value="7" required>
                </div>
                <div class="mb-4">
                    <label class="block text-sm font-medium text-gray-700 mb-1">Notificações</label>
                    <div class="flex items-center">
                        <input type="checkbox" id="enableNotifications" class="h-4 w-4 text-indigo-600 focus:ring-indigo-500 border-gray-300 rounded">
                        <label for="enableNotifications" class="ml-2 block text-sm text-gray-700">Ativar notificações</label>
                    </div>
                </div>
                <div class="flex justify-end space-x-2">
                    <button type="button" class="closeModal px-4 py-2 border border-gray-300 rounded-md text-gray-700 hover:bg-gray-50">Cancelar</button>
                    <button type="submit" class="px-4 py-2 bg-indigo-600 text-white rounded-md hover:bg-indigo-700">Salvar</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Data Management Modal -->
    <div id="dataModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg shadow-xl p-6 w-full max-w-md mx-4 modal modal-enter">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-lg font-semibold text-gray-800">Gerenciar Dados</h3>
                <button class="closeModal text-gray-400 hover:text-gray-600">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>
            </div>
            <div class="mb-6">
                <p class="text-sm text-gray-600 mb-4">Exporte seus dados para fazer backup ou transferir para outro dispositivo.</p>
                <button id="exportDataBtn" class="w-full px-4 py-2 bg-indigo-600 text-white rounded-md hover:bg-indigo-700 mb-4 flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
                    </svg>
                    Exportar Dados
                </button>
                <p class="text-sm text-gray-600 mb-4">Importe dados previamente exportados.</p>
                <label for="importDataFile" class="w-full px-4 py-2 bg-white border border-gray-300 text-gray-700 rounded-md hover:bg-gray-50 cursor-pointer flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2 text-indigo-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-8l-4-4m0 0L8 8m4-4v12" />
                    </svg>
                    Importar Dados
                    <input type="file" id="importDataFile" accept=".json" class="hidden">
                </label>
            </div>
            <div class="border-t border-gray-200 pt-4">
                <p class="text-sm text-gray-600 mb-4">Cuidado! Esta ação não pode ser desfeita.</p>
                <button id="resetDataBtn" class="w-full px-4 py-2 bg-red-600 text-white rounded-md hover:bg-red-700 flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
                    </svg>
                    Resetar Todos os Dados
                </button>
            </div>
        </div>
    </div>

    <!-- Toast Notification -->
    <div id="toast" class="fixed top-4 right-4 bg-white rounded-lg shadow-lg p-4 z-50 hidden toast">
        <div class="flex items-center">
            <div id="toastIcon" class="mr-3 text-green-500">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                </svg>
            </div>
            <div>
                <p id="toastMessage" class="font-medium">Operação realizada com sucesso!</p>
            </div>
        </div>
    </div>

    <script>
        // Data structure
        let appData = {
            subjects: [],
            sessions: [],
            settings: {
                dailyGoal: 120, // minutes
                cycleLength: 7, // days
                enableNotifications: false,
                cycleStartDate: new Date().toISOString().split('T')[0]
            }
        };

        // Active session state
        let activeSession = null;
        let timer = null;
        let elapsedSeconds = 0;
        let isPaused = false;

        // DOM Elements
        const tabDashboard = document.getElementById('tabDashboard');
        const tabSubjects = document.getElementById('tabSubjects');
        const tabStats = document.getElementById('tabStats');
        const dashboardContent = document.getElementById('dashboardContent');
        const subjectsContent = document.getElementById('subjectsContent');
        const statsContent = document.getElementById('statsContent');
        
        const addSubjectBtn = document.getElementById('addSubjectBtn');
        const addSubjectBtnTab = document.getElementById('addSubjectBtnTab');
        const startStudyBtn = document.getElementById('startStudyBtn');
        const settingsBtn = document.getElementById('settingsBtn');
        const dataBtn = document.getElementById('dataBtn');
        
        const addSubjectModal = document.getElementById('addSubjectModal');
        const editSubjectModal = document.getElementById('editSubjectModal');
        const studySessionModal = document.getElementById('studySessionModal');
        const activeSessionModal = document.getElementById('activeSessionModal');
        const settingsModal = document.getElementById('settingsModal');
        const dataModal = document.getElementById('dataModal');
        const minimizedSession = document.getElementById('minimizedSession');
        
        const addSubjectForm = document.getElementById('addSubjectForm');
        const editSubjectForm = document.getElementById('editSubjectForm');
        const studySessionForm = document.getElementById('studySessionForm');
        const settingsForm = document.getElementById('settingsForm');
        
        const colorOptions = document.querySelectorAll('.color-option');
        const editColorOptions = document.querySelectorAll('.edit-color-option');
        const subjectsList = document.getElementById('subjectsList');
        const sessionSubject = document.getElementById('sessionSubject');
        const deleteSubjectBtn = document.getElementById('deleteSubjectBtn');
        
        const pauseResumeBtn = document.getElementById('pauseResumeBtn');
        const pauseResumeText = document.getElementById('pauseResumeText');
        const finishSessionBtn = document.getElementById('finishSessionBtn');
        const minimizeSessionBtn = document.getElementById('minimizeSessionBtn');
        
        const exportDataBtn = document.getElementById('exportDataBtn');
        const importDataFile = document.getElementById('importDataFile');
        const resetDataBtn = document.getElementById('resetDataBtn');
        
        const toast = document.getElementById('toast');
        const toastMessage = document.getElementById('toastMessage');
        const toastIcon = document.getElementById('toastIcon');

        // Initialize app
        document.addEventListener('DOMContentLoaded', () => {
            loadData();
            setupEventListeners();
            updateUI();
        });

        // Load data from localStorage
        function loadData() {
            const savedData = localStorage.getItem('studyCycleAppData');
            if (savedData) {
                try {
                    appData = JSON.parse(savedData);
                    // Ensure settings object has all required properties
                    if (!appData.settings) {
                        appData.settings = {
                            dailyGoal: 120,
                            cycleLength: 7,
                            enableNotifications: false,
                            cycleStartDate: new Date().toISOString().split('T')[0]
                        };
                    } else {
                        if (!appData.settings.cycleStartDate) {
                            appData.settings.cycleStartDate = new Date().toISOString().split('T')[0];
                        }
                    }
                } catch (e) {
                    console.error('Error loading data:', e);
                    showToast('Erro ao carregar dados', 'error');
                }
            }
        }

        // Save data to localStorage
        function saveData() {
            try {
                localStorage.setItem('studyCycleAppData', JSON.stringify(appData));
            } catch (e) {
                console.error('Error saving data:', e);
                showToast('Erro ao salvar dados', 'error');
            }
        }

        // Setup event listeners
        function setupEventListeners() {
            // Tab navigation
            tabDashboard.addEventListener('click', () => switchTab('dashboard'));
            tabSubjects.addEventListener('click', () => switchTab('subjects'));
            tabStats.addEventListener('click', () => switchTab('stats'));
            
            // Buttons
            addSubjectBtn.addEventListener('click', () => showModal(addSubjectModal));
            addSubjectBtnTab.addEventListener('click', () => showModal(addSubjectModal));
            startStudyBtn.addEventListener('click', () => {
                populateSubjectDropdown();
                showModal(studySessionModal);
            });
            settingsBtn.addEventListener('click', () => {
                document.getElementById('dailyGoal').value = appData.settings.dailyGoal;
                document.getElementById('cycleLength').value = appData.settings.cycleLength;
                document.getElementById('enableNotifications').checked = appData.settings.enableNotifications;
                showModal(settingsModal);
            });
            dataBtn.addEventListener('click', () => showModal(dataModal));
            
            // Close modals
            document.querySelectorAll('.closeModal').forEach(btn => {
                btn.addEventListener('click', () => {
                    document.querySelectorAll('.modal').forEach(modal => {
                        modal.parentElement.classList.add('hidden');
                    });
                });
            });
            
            // Color selection
            colorOptions.forEach(option => {
                option.addEventListener('click', () => {
                    document.getElementById('subjectColor').value = option.dataset.color;
                    colorOptions.forEach(opt => opt.style.border = '');
                    option.style.border = '3px solid #4b5563';
                });
            });
            
            editColorOptions.forEach(option => {
                option.addEventListener('click', () => {
                    document.getElementById('editSubjectColor').value = option.dataset.color;
                    editColorOptions.forEach(opt => opt.style.border = '');
                    option.style.border = '3px solid #4b5563';
                });
            });
            
            // Forms
            addSubjectForm.addEventListener('submit', handleAddSubject);
            editSubjectForm.addEventListener('submit', handleEditSubject);
            studySessionForm.addEventListener('submit', handleStartSession);
            settingsForm.addEventListener('submit', handleSaveSettings);
            
            // Session controls
            pauseResumeBtn.addEventListener('click', togglePauseResume);
            finishSessionBtn.addEventListener('click', finishSession);
            minimizeSessionBtn.addEventListener('click', minimizeSession);
            minimizedSession.addEventListener('click', maximizeSession);
            
            // Delete subject
            deleteSubjectBtn.addEventListener('click', handleDeleteSubject);
            
            // Data management
            exportDataBtn.addEventListener('click', exportData);
            importDataFile.addEventListener('change', importData);
            resetDataBtn.addEventListener('click', resetData);
        }

        // Switch between tabs
        function switchTab(tab) {
            // Remove active class from all tabs
            tabDashboard.classList.remove('tab-active');
            tabSubjects.classList.remove('tab-active');
            tabStats.classList.remove('tab-active');
            tabDashboard.classList.add('text-gray-500');
            tabSubjects.classList.add('text-gray-500');
            tabStats.classList.add('text-gray-500');
            
            // Hide all content
            dashboardContent.classList.add('hidden');
            subjectsContent.classList.add('hidden');
            statsContent.classList.add('hidden');
            
            // Show selected tab and content
            if (tab === 'dashboard') {
                tabDashboard.classList.add('tab-active');
                tabDashboard.classList.remove('text-gray-500');
                dashboardContent.classList.remove('hidden');
                updateDashboard();
            } else if (tab === 'subjects') {
                tabSubjects.classList.add('tab-active');
                tabSubjects.classList.remove('text-gray-500');
                subjectsContent.classList.remove('hidden');
                updateSubjectsList();
            } else if (tab === 'stats') {
                tabStats.classList.add('tab-active');
                tabStats.classList.remove('text-gray-500');
                statsContent.classList.remove('hidden');
                updateStats();
            }
        }

        // Show modal
        function showModal(modal) {
            modal.classList.remove('hidden');
            const modalContent = modal.querySelector('.modal');
            modalContent.classList.remove('modal-enter');
            // Force reflow
            void modalContent.offsetWidth;
            modalContent.classList.add('modal-enter-active');
        }

        // Handle adding a new subject
        function handleAddSubject(e) {
            e.preventDefault();
            
            const name = document.getElementById('subjectName').value;
            const color = document.getElementById('subjectColor').value;
            const priority = document.getElementById('subjectPriority').value;
            const goal = parseInt(document.getElementById('subjectGoal').value);
            
            const newSubject = {
                id: Date.now().toString(),
                name,
                color,
                priority,
                goal,
                totalTime: 0
            };
            
            appData.subjects.push(newSubject);
            saveData();
            
            addSubjectForm.reset();
            document.getElementById('subjectColor').value = '#6366f1';
            colorOptions.forEach(opt => opt.style.border = '');
            
            addSubjectModal.classList.add('hidden');
            
            updateSubjectsList();
            showToast('Matéria adicionada com sucesso!');
        }

        // Handle editing a subject
        function handleEditSubject(e) {
            e.preventDefault();
            
            const id = document.getElementById('editSubjectId').value;
            const name = document.getElementById('editSubjectName').value;
            const color = document.getElementById('editSubjectColor').value;
            const priority = document.getElementById('editSubjectPriority').value;
            const goal = parseInt(document.getElementById('editSubjectGoal').value);
            
            const subjectIndex = appData.subjects.findIndex(s => s.id === id);
            if (subjectIndex !== -1) {
                appData.subjects[subjectIndex] = {
                    ...appData.subjects[subjectIndex],
                    name,
                    color,
                    priority,
                    goal
                };
                
                saveData();
                editSubjectModal.classList.add('hidden');
                
                updateSubjectsList();
                updateDashboard();
                updateStats();
                showToast('Matéria atualizada com sucesso!');
            }
        }

        // Handle deleting a subject
        function handleDeleteSubject() {
            const id = document.getElementById('editSubjectId').value;
            
            if (confirm('Tem certeza que deseja excluir esta matéria? Todos os registros de estudo associados também serão excluídos.')) {
                appData.subjects = appData.subjects.filter(s => s.id !== id);
                appData.sessions = appData.sessions.filter(s => s.subjectId !== id);
                
                saveData();
                editSubjectModal.classList.add('hidden');
                
                updateSubjectsList();
                updateDashboard();
                updateStats();
                showToast('Matéria excluída com sucesso!');
            }
        }

        // Handle starting a study session
        function handleStartSession(e) {
            e.preventDefault();
            
            const subjectId = document.getElementById('sessionSubject').value;
            const duration = parseInt(document.getElementById('sessionDuration').value);
            const notes = document.getElementById('sessionNotes').value;
            
            const subject = appData.subjects.find(s => s.id === subjectId);
            if (!subject) {
                showToast('Selecione uma matéria válida', 'error');
                return;
            }
            
            activeSession = {
                subjectId,
                subjectName: subject.name,
                subjectColor: subject.color,
                plannedDuration: duration * 60, // Convert to seconds
                startTime: new Date(),
                notes,
                isPaused: false,
                pauseTime: 0
            };
            
            studySessionModal.classList.add('hidden');
            showModal(activeSessionModal);
            
            document.getElementById('activeSubjectName').textContent = subject.name;
            document.getElementById('activeSubjectName').style.color = subject.color;
            
            startTimer();
        }

        // Handle saving settings
        function handleSaveSettings(e) {
            e.preventDefault();
            
            const dailyGoal = parseInt(document.getElementById('dailyGoal').value);
            const cycleLength = parseInt(document.getElementById('cycleLength').value);
            const enableNotifications = document.getElementById('enableNotifications').checked;
            
            appData.settings.dailyGoal = dailyGoal;
            appData.settings.cycleLength = cycleLength;
            appData.settings.enableNotifications = enableNotifications;
            
            saveData();
            settingsModal.classList.add('hidden');
            
            updateDashboard();
            showToast('Configurações salvas com sucesso!');
        }

        // Start the timer for active session
        function startTimer() {
            elapsedSeconds = 0;
            updateTimerDisplay();
            
            timer = setInterval(() => {
                if (!isPaused) {
                    elapsedSeconds++;
                    updateTimerDisplay();
                    updateProgressRing();
                }
            }, 1000);
        }

        // Update timer display
        function updateTimerDisplay() {
            const minutes = Math.floor(elapsedSeconds / 60);
            const seconds = elapsedSeconds % 60;
            
            const display = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
            document.getElementById('timerDisplay').textContent = display;
            document.getElementById('minimizedTimer').textContent = display;
            
            // Update progress percentage
            const progress = Math.min(100, Math.round((elapsedSeconds / activeSession.plannedDuration) * 100));
            document.getElementById('sessionProgress').textContent = `${progress}% concluído`;
        }

        // Update progress ring
        function updateProgressRing() {
            const circle = document.getElementById('progressRing');
            const radius = circle.getAttribute('r');
            const circumference = 2 * Math.PI * radius;
            
            const progress = Math.min(1, elapsedSeconds / activeSession.plannedDuration);
            const offset = circumference * (1 - progress);
            
            circle.style.strokeDasharray = `${circumference} ${circumference}`;
            circle.style.strokeDashoffset = offset;
        }

        // Toggle pause/resume
        function togglePauseResume() {
            isPaused = !isPaused;
            
            if (isPaused) {
                pauseResumeText.textContent = 'Retomar';
                pauseResumeBtn.classList.remove('bg-yellow-500', 'hover:bg-yellow-600');
                pauseResumeBtn.classList.add('bg-green-500', 'hover:bg-green-600');
                activeSession.isPaused = true;
                activeSession.pauseTime = new Date();
            } else {
                pauseResumeText.textContent = 'Pausar';
                pauseResumeBtn.classList.remove('bg-green-500', 'hover:bg-green-600');
                pauseResumeBtn.classList.add('bg-yellow-500', 'hover:bg-yellow-600');
                activeSession.isPaused = false;
                activeSession.pauseTime = 0;
            }
        }

        // Finish session
        function finishSession() {
            clearInterval(timer);
            
            // Calculate actual duration
            const endTime = new Date();
            const durationMs = endTime - new Date(activeSession.startTime);
            const durationMinutes = Math.round(durationMs / 60000);
            
            // Create session record
            const session = {
                id: Date.now().toString(),
                subjectId: activeSession.subjectId,
                date: endTime.toISOString().split('T')[0],
                startTime: activeSession.startTime.toISOString(),
                endTime: endTime.toISOString(),
                duration: durationMinutes,
                notes: activeSession.notes
            };
            
            // Update subject total time
            const subjectIndex = appData.subjects.findIndex(s => s.id === activeSession.subjectId);
            if (subjectIndex !== -1) {
                appData.subjects[subjectIndex].totalTime += durationMinutes;
            }
            
            appData.sessions.push(session);
            saveData();
            
            activeSession = null;
            activeSessionModal.classList.add('hidden');
            minimizedSession.classList.add('hidden');
            
            updateDashboard();
            updateStats();
            showToast('Sessão de estudo finalizada!');
        }

        // Minimize session
        function minimizeSession() {
            activeSessionModal.classList.add('hidden');
            minimizedSession.classList.remove('hidden');
        }

        // Maximize session
        function maximizeSession() {
            minimizedSession.classList.add('hidden');
            showModal(activeSessionModal);
        }

        // Update dashboard
        function updateDashboard() {
            updateTodaySummary();
            updateRecentActivity();
            updateCurrentCycle();
        }

        // Update today's summary
        function updateTodaySummary() {
            const today = new Date().toISOString().split('T')[0];
            
            // Calculate today's study time
            const todaySessions = appData.sessions.filter(s => s.date === today);
            const todayMinutes = todaySessions.reduce((total, session) => total + session.duration, 0);
            const todayHours = Math.floor(todayMinutes / 60);
            const todayRemainingMinutes = todayMinutes % 60;
            
            document.getElementById('todayTime').textContent = `${todayHours}h ${todayRemainingMinutes}min`;
            
            // Calculate progress towards daily goal
            const progress = Math.min(100, Math.round((todayMinutes / appData.settings.dailyGoal) * 100));
            document.getElementById('todayProgress').style.width = `${progress}%`;
            document.getElementById('todayProgressText').textContent = `${progress}% da meta diária`;
            
            // Count unique subjects studied today
            const uniqueSubjectsToday = new Set(todaySessions.map(s => s.subjectId)).size;
            document.getElementById('todaySubjects').textContent = uniqueSubjectsToday;
        }

        // Update recent activity
        function updateRecentActivity() {
            const recentActivityList = document.getElementById('recentActivityList');
            
            // Get 5 most recent sessions
            const recentSessions = [...appData.sessions]
                .sort((a, b) => new Date(b.endTime) - new Date(a.endTime))
                .slice(0, 5);
            
            if (recentSessions.length === 0) {
                recentActivityList.innerHTML = `
                    <div class="p-4 text-center text-gray-500">
                        Nenhuma atividade recente para mostrar.
                    </div>
                `;
                return;
            }
            
            recentActivityList.innerHTML = '';
            
            recentSessions.forEach(session => {
                const subject = appData.subjects.find(s => s.id === session.subjectId);
                if (!subject) return;
                
                const date = new Date(session.date);
                const formattedDate = date.toLocaleDateString('pt-BR', {
                    day: '2-digit',
                    month: '2-digit',
                    year: 'numeric'
                });
                
                const item = document.createElement('div');
                item.className = 'p-4 flex items-center';
                item.innerHTML = `
                    <div class="w-2 h-2 rounded-full mr-3" style="background-color: ${subject.color}"></div>
                    <div class="flex-grow">
                        <p class="font-medium">${subject.name}</p>
                        <p class="text-sm text-gray-500">${formattedDate} • ${session.duration} minutos</p>
                    </div>
                `;
                
                recentActivityList.appendChild(item);
            });
        }

        // Update current cycle
        function updateCurrentCycle() {
            const cycleStartDate = new Date(appData.settings.cycleStartDate);
            const today = new Date();
            
            // Calculate days since cycle start
            const diffTime = Math.abs(today - cycleStartDate);
            const diffDays = Math.floor(diffTime / (1000 * 60 * 60 * 24));
            
            // Calculate current day in cycle
            const cycleDay = (diffDays % appData.settings.cycleLength) + 1;
            
            document.getElementById('currentCycle').textContent = `Dia ${cycleDay} de ${appData.settings.cycleLength}`;
        }

        // Update subjects list
        function updateSubjectsList() {
            if (appData.subjects.length === 0) {
                subjectsList.innerHTML = `
                    <div class="bg-white rounded-lg shadow p-6 text-center text-gray-500">
                        Nenhuma matéria cadastrada. Clique em "Nova Matéria" para começar.
                    </div>
                `;
                return;
            }
            
            subjectsList.innerHTML = '';
            
            // Sort subjects by priority
            const sortedSubjects = [...appData.subjects].sort((a, b) => {
                const priorityOrder = { high: 0, medium: 1, low: 2 };
                return priorityOrder[a.priority] - priorityOrder[b.priority];
            });
            
            sortedSubjects.forEach(subject => {
                const hours = Math.floor(subject.totalTime / 60);
                const minutes = subject.totalTime % 60;
                
                const priorityLabel = {
                    high: 'Alta',
                    medium: 'Média',
                    low: 'Baixa'
                }[subject.priority];
                
                const priorityClass = {
                    high: 'bg-red-100 text-red-800',
                    medium: 'bg-yellow-100 text-yellow-800',
                    low: 'bg-green-100 text-green-800'
                }[subject.priority];
                
                const card = document.createElement('div');
                card.className = 'bg-white rounded-lg shadow p-6 card';
                card.innerHTML = `
                    <div class="flex justify-between items-start mb-4">
                        <h3 class="text-lg font-semibold" style="color: ${subject.color}">${subject.name}</h3>
                        <span class="px-2 py-1 rounded-full text-xs font-medium ${priorityClass}">${priorityLabel}</span>
                    </div>
                    <div class="mb-4">
                        <p class="text-sm text-gray-500">Tempo total de estudo</p>
                        <p class="text-xl font-bold">${hours}h ${minutes}min</p>
                    </div>
                    <div class="mb-4">
                        <p class="text-sm text-gray-500">Meta diária</p>
                        <p class="text-md">${subject.goal} minutos</p>
                    </div>
                    <button class="edit-subject-btn w-full px-4 py-2 bg-gray-100 hover:bg-gray-200 text-gray-700 rounded-md transition" data-id="${subject.id}">
                        Editar
                    </button>
                `;
                
                subjectsList.appendChild(card);
            });
            
            // Add event listeners to edit buttons
            document.querySelectorAll('.edit-subject-btn').forEach(btn => {
                btn.addEventListener('click', () => {
                    const id = btn.dataset.id;
                    const subject = appData.subjects.find(s => s.id === id);
                    
                    if (subject) {
                        document.getElementById('editSubjectId').value = subject.id;
                        document.getElementById('editSubjectName').value = subject.name;
                        document.getElementById('editSubjectColor').value = subject.color;
                        document.getElementById('editSubjectPriority').value = subject.priority;
                        document.getElementById('editSubjectGoal').value = subject.goal;
                        
                        // Highlight selected color
                        editColorOptions.forEach(opt => {
                            opt.style.border = opt.dataset.color === subject.color ? '3px solid #4b5563' : '';
                        });
                        
                        showModal(editSubjectModal);
                    }
                });
            });
        }

        // Update stats
        function updateStats() {
            updateTimeDistributionChart();
            updateWeeklyProgressChart();
            updateOverallStats();
        }

        // Update time distribution chart
        function updateTimeDistributionChart() {
            const chart = document.getElementById('timeDistributionChart');
            chart.innerHTML = '';
            
            if (appData.subjects.length === 0) {
                chart.innerHTML = `
                    <div class="w-full text-center text-gray-500">
                        Nenhuma matéria cadastrada ainda.
                    </div>
                `;
                return;
            }
            
            // Sort subjects by total time (descending)
            const sortedSubjects = [...appData.subjects]
                .sort((a, b) => b.totalTime - a.totalTime)
                .slice(0, 7); // Show top 7 subjects
            
            // Find maximum time for scaling
            const maxTime = Math.max(...sortedSubjects.map(s => s.totalTime), 60);
            
            sortedSubjects.forEach(subject => {
                const height = Math.max(10, (subject.totalTime / maxTime) * 200);
                
                const barContainer = document.createElement('div');
                barContainer.className = 'flex flex-col items-center';
                barContainer.innerHTML = `
                    <div class="text-xs font-medium mb-1">${subject.totalTime}min</div>
                    <div class="chart-bar w-12 rounded-t-lg" style="height: ${height}px; background-color: ${subject.color}"></div>
                    <div class="text-xs mt-2 w-16 text-center truncate" title="${subject.name}">${subject.name}</div>
                `;
                
                chart.appendChild(barContainer);
            });
        }

        // Update weekly progress chart
        function updateWeeklyProgressChart() {
            const chart = document.getElementById('weeklyProgressChart');
            chart.innerHTML = '';
            
            // Get dates for the last 7 days
            const dates = [];
            const today = new Date();
            
            for (let i = 6; i >= 0; i--) {
                const date = new Date(today);
                date.setDate(today.getDate() - i);
                dates.push(date.toISOString().split('T')[0]);
            }
            
            // Calculate study time for each day
            const dailyTimes = dates.map(date => {
                const sessions = appData.sessions.filter(s => s.date === date);
                return sessions.reduce((total, session) => total + session.duration, 0);
            });
            
            // Find maximum time for scaling
            const maxTime = Math.max(...dailyTimes, appData.settings.dailyGoal);
            
            // Create chart bars
            dates.forEach((date, index) => {
                const dayName = new Date(date).toLocaleDateString('pt-BR', { weekday: 'short' }).slice(0, 3);
                const time = dailyTimes[index];
                const height = Math.max(10, (time / maxTime) * 200);
                const isToday = date === today.toISOString().split('T')[0];
                
                const barContainer = document.createElement('div');
                barContainer.className = 'flex flex-col items-center';
                barContainer.innerHTML = `
                    <div class="text-xs font-medium mb-1">${time}min</div>
                    <div class="chart-bar w-12 rounded-t-lg ${isToday ? 'bg-indigo-600' : 'bg-indigo-400'}" style="height: ${height}px;"></div>
                    <div class="text-xs mt-2 ${isToday ? 'font-bold' : ''}">${dayName}</div>
                `;
                
                chart.appendChild(barContainer);
            });
        }

        // Update overall stats
        function updateOverallStats() {
            // Calculate total study time
            const totalMinutes = appData.sessions.reduce((total, session) => total + session.duration, 0);
            const totalHours = Math.floor(totalMinutes / 60);
            const remainingMinutes = totalMinutes % 60;
            
            document.getElementById('totalStudyTime').textContent = `${totalHours}h ${remainingMinutes}min`;
            
            // Calculate daily average
            const uniqueDays = new Set(appData.sessions.map(s => s.date)).size;
            let avgMinutes = 0;
            
            if (uniqueDays > 0) {
                avgMinutes = Math.round(totalMinutes / uniqueDays);
            }
            
            const avgHours = Math.floor(avgMinutes / 60);
            const avgRemainingMinutes = avgMinutes % 60;
            
            document.getElementById('dailyAverage').textContent = `${avgHours}h ${avgRemainingMinutes}min`;
            
            // Calculate consecutive days
            let consecutiveDays = 0;
            const today = new Date().toISOString().split('T')[0];
            let currentDate = today;
            
            while (true) {
                const sessions = appData.sessions.filter(s => s.date === currentDate);
                if (sessions.length === 0) break;
                
                consecutiveDays++;
                
                // Move to previous day
                const prevDate = new Date(currentDate);
                prevDate.setDate(prevDate.getDate() - 1);
                currentDate = prevDate.toISOString().split('T')[0];
            }
            
            document.getElementById('consecutiveDays').textContent = `${consecutiveDays} dias`;
        }

        // Populate subject dropdown
        function populateSubjectDropdown() {
            const dropdown = document.getElementById('sessionSubject');
            dropdown.innerHTML = '<option value="" disabled selected>Selecione uma matéria</option>';
            
            appData.subjects.forEach(subject => {
                const option = document.createElement('option');
                option.value = subject.id;
                option.textContent = subject.name;
                dropdown.appendChild(option);
            });
        }

        // Show toast notification
        function showToast(message, type = 'success') {
            const toast = document.getElementById('toast');
            const toastMessage = document.getElementById('toastMessage');
            const toastIcon = document.getElementById('toastIcon');
            
            toastMessage.textContent = message;
            
            if (type === 'success') {
                toastIcon.className = 'mr-3 text-green-500';
                toastIcon.innerHTML = `
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                    </svg>
                `;
            } else {
                toastIcon.className = 'mr-3 text-red-500';
                toastIcon.innerHTML = `
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
                    </svg>```
