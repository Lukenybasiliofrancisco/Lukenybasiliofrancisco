 
html
<!DOCTYPE html>
<html>
<head>
  <title>Captura de Foto</title>
</head>
<body>
  <video id="video" width="640" height="480" autoplay></video>
  <button id="capture-btn">Capturar Foto</button>
  <canvas id="canvas" width="640" height="480"></canvas>
  <img id="photo" src="" alt="Foto Capturada">
  
  <script src="script.js"></script>
</body>
</html>
```

2. No arquivo JavaScript (script.js) vinculado à página HTML, é necessário adicionar o código para capturar a imagem e exibi-la no elemento `<img>`:
```javascript
// Acessar o elemento de vídeo
const video = document.getElementById('video');
const captureBtn = document.getElementById('capture-btn');
const canvas = document.getElementById('canvas');
const photo = document.getElementById('photo');

// Verificar se o navegador suporta a captura de vídeo
if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
  // Pedir permissão ao usuário para acessar a câmera
  navigator.mediaDevices.getUserMedia({ video: true })
    .then(function(stream) {
      // Exibir o vídeo na tag de vídeo
      video.srcObject = stream;
      video.play();
    })
    .catch(function(error) {
      console.error('Erro ao acessar a câmera:', error);
    });

    // Adicionar evento de clique para capturar a foto
    captureBtn.addEventListener('click', function() {
      // Desenhar a imagem do vídeo no canvas
      canvas.getContext('2d').drawImage(video, 0, 0, canvas.width, canvas.height);

      // Converter o canvas para uma URL de imagem base64
      const dataURL = canvas.toDataURL();

      // Definir a URL da imagem capturada no elemento <img>
      photo.src = dataURL;
    });
}
else {
  console.error('Seu navegador não suporta a captura de vídeo.');
}
```

 
