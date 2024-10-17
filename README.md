# Projeto para Treino de JavaScript

### Pong Game

Tutorial realizado com base nas aulas do ([ASMR Programming](https://youtu.be/wQHVJjrwLhA)), vou mostrar como codificar um jogo de pong com javascript. O projeto para você jogar pingue-pongue com Javascript❗️

### Torne o jogo mais fácil

Para facilitar o jogo, podemos ajustar a velocidade da raquete do computador para torná-la menos responsiva ao movimento da bola. Você pode modificar a linha ```com.y += (ball.y - (com.y + com.height / 2)) * 0.1;``` na função ```update()``` para reduzir o fator ```0.1``` para um valor menor. Isso fará com que a raquete do computador se mova mais lentamente e tornará o jogo mais fácil de vencer. Aqui está um exemplo com um fator reduzido de ```0.05``` :


```javascript
// Atualize a lógica do jogo
function update() {
  // Verifique a pontuação e reinicie a bola, se necessário
  if (ball.x - ball.radius < 0) {
    com.score++;
    resetBall();
  } else if (ball.x + ball.radius > canvas.width) {
    user.score++;
    resetBall();
  }

  // Update ball position
  ball.x += ball.velocityX;
  ball.y += ball.velocityY;

  // Atualize a posição da raquete do computador com base na posição da bola (ajustada para velocidade mais lenta)
  com.y += (ball.y - (com.y + com.height / 2)) * 0.05;

  // Reflita a bola nas paredes superior e inferior
  if (ball.y - ball.radius < 0 || ball.y + ball.radius > canvas.height) {
    ball.velocityY = -ball.velocityY;
  }

  // Determine qual raquete está sendo atingida pela bola e controle a colisão
  let player = ball.x + ball.radius < canvas.width / 2 ? user : com;
  if (collision(ball, player)) {
    const collidePoint = ball.y - (player.y + player.height / 2);
    const collisionAngle = (Math.PI / 4) * (collidePoint / (player.height / 2));
    const direction = ball.x + ball.radius < canvas.width / 2 ? 1 : -1;
    ball.velocityX = direction * ball.speed * Math.cos(collisionAngle);
    ball.velocityY = ball.speed * Math.sin(collisionAngle);

    // Aumente a velocidade da bola e limite a velocidade máxima
    ball.speed += 0.2;
    if (ball.speed > maxBallSpeed) {
      ball.speed = maxBallSpeed;
    }
  }
}
```
##

# Screenshot
Aqui temos a captura de tela do projeto: :

![screenshot](screenshot.jpg)
