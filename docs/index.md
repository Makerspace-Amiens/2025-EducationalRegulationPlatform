<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Régulateur PID pour Drone</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.7.1/chart.min.js"></script>
</head>
<body class="bg-gray-100 text-gray-900">
    <header class="bg-blue-600 text-white p-4 text-center text-2xl font-bold">
        Régulateur PID pour Drone
    </header>
    <main class="container mx-auto p-6">
        <section class="bg-white p-6 rounded-lg shadow-md mb-6">
            <h2 class="text-xl font-semibold mb-2">Comprendre le Régulateur PID</h2>
            <p>Le régulateur PID permet d'ajuster dynamiquement la stabilité du drone en corrigeant les écarts avec une boucle de rétroaction.</p>
        </section>
        
        <section class="bg-white p-6 rounded-lg shadow-md mb-6">
            <h2 class="text-xl font-semibold mb-2">Graphique de Réponse PID</h2>
            <canvas id="pidChart"></canvas>
        </section>
    </main>
    
    <script>
        var ctx = document.getElementById('pidChart').getContext('2d');
        var pidChart = new Chart(ctx, {
            type: 'line',
            data: {
                labels: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
                datasets: [{
                    label: 'Réponse PID',
                    data: [0, 2, 4, 8, 10, 12, 14, 15, 15.5, 15.8, 16],
                    borderColor: 'blue',
                    fill: false
                }]
            },
            options: {
                responsive: true,
                scales: {
                    x: { title: { display: true, text: 'Temps (s)' } },
                    y: { title: { display: true, text: 'Valeur de consigne' } }
                }
            }
        });
    </script>
</body>
</html>
