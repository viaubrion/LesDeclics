<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jeu Tirage au Sort - Lots à Gagné</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body {
            background-color: #f4f7f6;
            color: #333;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }
        h1 {
            margin-bottom: 10px;
            color: #2c3e50;
        }
        p.subtitle {
            margin-bottom: 30px;
            color: #7f8c8d;
        }
        /* Grille des lots */
        .prizes-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            width: 100%;
            max-width: 900px;
            margin-bottom: 40px;
        }
        .prize-card {
            background: white;
            border-radius: 12px;
            padding: 20px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            transition: transform 0.2s ease, border-color 0.2s ease;
            border: 2px solid transparent;
        }
        .prize-card:hover {
            transform: translateY(-5px);
        }
        .prize-card.active {
            border-color: #e74c3c;
            animation: pulse 0.5s infinite alternate;
        }
        @keyframes pulse {
            from { transform: scale(1); }
            to { transform: scale(1.03); }
        }
        .prize-icon {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        .prize-name {
            font-size: 1.1rem;
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 8px;
        }
        .prize-probability {
            display: inline-block;
            background-color: #e8f8f5;
            color: #1abc9c;
            font-weight: bold;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.9rem;
        }
        /* Zone de Tirage */
        .draw-section {
            text-align: center;
        }
        .btn-draw {
            background: linear-gradient(135deg, #ff7675, #d63031);
            color: white;
            border: none;
            padding: 15px 40px;
            font-size: 1.2rem;
            font-weight: bold;
            border-radius: 30px;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(214, 48, 49, 0.4);
            transition: background 0.3s, transform 0.1s;
        }
        .btn-draw:hover {
            transform: scale(1.05);
        }
        .btn-draw:disabled {
            background: #b2bec3;
            cursor: not-allowed;
            box-shadow: none;
            transform: none;
        }
        /* Pop-up Résultat */
        .result-modal {
            margin-top: 25px;
            padding: 15px 25px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            display: none;
        }
        .result-modal.show {
            display: block;
            animation: fadeIn 0.4s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>
    <h1>🎉 Grande Loterie</h1>
    <p class="subtitle">Découvrez nos lots et tentez votre chance !</p>
    <!-- Affichage des lots -->
    <div class="prizes-grid" id="prizesContainer"></div>
    <!-- Bouton de lancement -->
    <div class="draw-section">
        <button id="drawBtn" class="btn-draw" onclick="playGame()">Tirer un lot !</button>
        <div id="resultModal" class="result-modal">
            <h2>Résultat :</h2>
            <p id="resultText" style="font-size: 1.2rem; margin-top: 8px; color: #2d3436;"></p>
        </div>
    </div>
    <script>
        // 1. DÉFINITION DES LOTS ET LEURS PROBABILITÉS (Total = 100%)
        const prizes = [
            { id: 1, name: "Consolation (Sticker)", probability: 50, icon: "🏷️" },
            { id: 2, name: "Bons d'achat 10€",      probability: 30, icon: "🎟️" },
            { id: 3, name: "Enceinte Bluetooth",    probability: 14, icon: "🔊" },
            { id: 4, name: "Console PS5",           probability: 5,  icon: "🎮" },
            { id: 5, name: "Voyage à Bali",         probability: 1,  icon: "✈️" }
        ];
        // 2. GENERATION DYNAMIQUE DU HTML POUR CHAQUE LOT
        const container = document.getElementById('prizesContainer');
        prizes.forEach(prize => {
            const card = document.createElement('div');
            card.className = 'prize-card';
            card.id = `prize-${prize.id}`;
            card.innerHTML = `
                <div class="prize-icon">${prize.icon}</div>
                <div class="prize-name">${prize.name}</div>
                <div class="prize-probability">${prize.probability}% de chance</div>
            `;
            container.appendChild(card);
        });
        // 3. ALGORITHME DE TIRAGE ALÉATOIRE PONDÉRÉ
        function getWeightedRandomPrize() {
            // Génère un nombre entre 0 et 100
            const random = Math.random() * 100;
            let cumulativeProbability = 0;
            for (const prize of prizes) {
                cumulativeProbability += prize.probability;
                if (random <= cumulativeProbability) {
                    return prize;
                }
            }
            return prizes[0]; // Sécurité
        }
        // 4. LOGIQUE D'ANIMATION ET DU BOUTON
        function playGame() {
            const btn = document.getElementById('drawBtn');
            const resultModal = document.getElementById('resultModal');
            const resultText = document.getElementById('resultText');
          
            // Désactiver le bouton pendant le tirage
            btn.disabled = true;
            resultModal.classList.remove('show');
            // Retirer la mise en valeur précédente
            document.querySelectorAll('.prize-card').forEach(card => card.classList.remove('active'));

            // Simulation d'un suspense (effet visuel pendant 2 secondes)
            let counter = 0;
            const interval = setInterval(() => {
                const randomCardIndex = Math.floor(Math.random() * prizes.length);
                document.querySelectorAll('.prize-card').forEach(c => c.classList.remove('active'));
                document.getElementById(`prize-${prizes[randomCardIndex].id}`).classList.add('active');
                
                counter += 100;
                if (counter >= 2000) { // Fin de l'animation après 2s
                    clearInterval(interval);
                    
                    // Résultat réel selon les probabilités
                    const winningPrize = getWeightedRandomPrize();
                    
                    // Mettre en surbrillance la carte gagnante
                    document.querySelectorAll('.prize-card').forEach(c => c.classList.remove('active'));
                    document.getElementById(`prize-${winningPrize.id}`).classList.add('active');

                    // Afficher le texte de victoire
                    resultText.innerHTML = `Bravo ! Vous avez gagné : <strong>${winningPrize.icon} ${winningPrize.name}</strong> !`;
                    resultModal.classList.add('show');
                    
                    // Réactiver le bouton
                    btn.disabled = false;
                }
            }, 100);
        }
    </script>
</body>
</html>
