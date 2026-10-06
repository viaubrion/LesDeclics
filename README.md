# LesDeclics
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tirage de Sticker</title>
  <style>
    body {
      font-family: system-ui, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
      background-color: #f3f4f6;
    }
    .card {
      background: white;
      padding: 2rem;
      border-radius: 1rem;
      box-shadow: 0 10px 25px rgba(0,0,0,0.1);
      text-align: center;
      max-width: 320px;
      width: 90%;
    }
    .sticker-box {
      margin: 1.5rem 0;
      min-height: 200px;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    img {
      max-width: 100%;
      height: auto;
      border-radius: 0.5rem;
    }
    button {
      background: #4f46e5;
      color: white;
      border: none;
      padding: 0.75rem 1.5rem;
      font-size: 1rem;
      border-radius: 0.5rem;
      cursor: pointer;
    }
    button:hover { background: #4338ca; }
  </style>
</head>
<body>

  <div class="card">
    <h2 id="titre">Obtiens ton sticker !</h2>
    <div class="sticker-box">
      <img id="sticker-display" src="" alt="Sticker" style="display: none;">
    </div>
    <button onclick="tirerSticker()">Lancer le tirage</button>
  </div>

  <script>
    // Remplace les URLs par les liens réels de tes stickers
    const stickers = [
      "https://picsum.photos/id/1025/300/300",
      "https://picsum.photos/id/1062/300/300",
      "https://picsum.photos/id/1069/300/300",
      "https://picsum.photos/id/1074/300/300"
    ];

    function tirerSticker() {
      const index = Math.floor(Math.random() * stickers.length);
      const img = document.getElementById('sticker-display');
      img.src = stickers[index];
      img.style.display = 'block';
      document.getElementById('titre').innerText = "🎉 Sticker obtenu !";
    }
  </script>

</body>
</html>
