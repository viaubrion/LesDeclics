# LesDeclics
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ton Sticker Aléatoire</title>
  <style>
    body { text-align: center; font-family: sans-serif; background: #f4f4f9; padding: 40px 20px; }
    h1 { color: #333; }
    img { max-width: 280px; height: auto; margin-top: 20px; filter: drop-shadow(0 6px 12px rgba(0,0,0,0.15)); }
  </style>
</head>
<body>
  <h1>Félicitations ! 🎉</h1>
  <p>Voici ton sticker :</p>
  <img id="sticker-img" src="" alt="Sticker aléatoire">

  <script>
    // Liste des fichiers d'images
    const stickers = [
      'sticker1.png',
      'sticker2.png',
      'sticker3.png',
      'sticker4.png'
    ];

    // Tirage au sort au chargement de la page
    const tirage = stickers[Math.floor(Math.random() * stickers.length)];
    document.getElementById('sticker-img').src = tirage;
  </script>
</body>
</html>
