# LesDeclics
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ton Sticker Aléatoire</title>
  <style>
    body { font-family: system-ui, sans-serif; text-align: center; padding: 2rem; background: #f4f4f9; }
    .card { background: white; padding: 2rem; border-radius: 16px; box-shadow: 0 4px 12px rgba(0,0,0,0.1); display: inline-block; }
    img { max-width: 250px; height: auto; border-radius: 8px; margin-top: 1rem; }
  </style>
</head>
<body>
  <div class="card">
    <h1>🎉 Voici ton sticker !</h1>
    <img id="sticker" src="" alt="Sticker aléatoire">
  </div>

  <script>
    // Liste des liens de tes stickers
    const stickers = [
      "https://mon-site.com/stickers/sticker1.png",
      "https://mon-site.com/stickers/sticker2.png",
      "https://mon-site.com/stickers/sticker3.png"
    ];

    // Sélection aléatoire
    const randomIndex = Math.floor(Math.random() * stickers.length);
    document.getElementById("sticker").src = stickers[randomIndex];
  </script>
</body>
</html>
