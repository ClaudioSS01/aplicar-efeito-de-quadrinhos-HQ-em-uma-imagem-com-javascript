# aplicar-efeito-de-quadrinhos-HQ-em-uma-imagem-com-javascript
função para aplicar efeito de historias em quadrinhos em uma imagem usando javascript puro


function applyComicEffectToImage(imageId) {
  // Pega a imagem original
  const originalImage = document.getElementById(imageId);

  // Cria um novo elemento de canvas
  const canvas = document.createElement('canvas');
  canvas.width = originalImage.width;
  canvas.height = originalImage.height;
  const context = canvas.getContext('2d');

  // Desenha a imagem original no canvas
  context.drawImage(originalImage, 0, 0);

  // Aplica o efeito de quadrinhos
  const imageData = context.getImageData(0, 0, canvas.width, canvas.height);
  const pixels = imageData.data;
  for (let i = 0; i < pixels.length; i += 4) {
    const red = pixels[i];
    const green = pixels[i + 1];
    const blue = pixels[i + 2];
    const brightness = (red + green + blue) / 3;
    pixels[i] = brightness + 40;
    pixels[i + 1] = brightness + 40;
    pixels[i + 2] = brightness + 40;
  }
  context.putImageData(imageData, 0, 0);

  // Substitui a imagem original pelo canvas com o efeito
  originalImage.parentNode.replaceChild(canvas, originalImage);
}
