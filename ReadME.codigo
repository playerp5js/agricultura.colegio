function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
}
let gardenerX;
let gardenerY;
let plants = [];
let tools = ["watering-can", "shovel", "pruner"];
let currentTool = 0;
let sunSize = 50;
let sunGrowing = true;

function setup() {
  createCanvas(800, 600);
  gardenerX = width / 2;
  gardenerY = height - 100;

  // Criar algumas plantas aleatórias
  for (let i = 0; i < 5; i++) {
    plants.push({
      x: random(100, width - 100),
      y: height - 50,
      height: random(30, 80),
      color: color(random(50, 150), random(150, 200), random(50, 100)),
      growth: random(0.2, 0.7),
    });
  }
}

function draw() {
  background(135, 206, 235); // céu azul

  // Desenhar sol
  drawSun();

  // Desenhar grama
  fill(34, 139, 34);
  noStroke();
  rect(0, height - 50, width, 50);

  // Desenhar plantas
  drawPlants();

  // Desenhar jardineiro
  drawGardener();

  // Animar ferramenta
  animateTool();

  // Crescer plantas lentamente
  growPlants();
}

function drawSun() {
  fill(255, 255, 0);
  noStroke();
  ellipse(width - 100, 100, sunSize);

  // Animação do sol pulsando
  if (sunGrowing) {
    sunSize += 0.2;
    if (sunSize > 60) sunGrowing = false;
  } else {
    sunSize -= 0.2;
    if (sunSize < 50) sunGrowing = true;
  }

  // Raios de sol
  for (let i = 0; i < 12; i++) {
    push();
    translate(width - 100, 100);
    rotate((i * TWO_PI) / 12);
    fill(255, 255, 0, 150);
    rect(0, -5, sunSize / 2, 10);
    pop();
  }
}

function drawPlants() {
  for (let plant of plants) {
    // Caule
    stroke(0, 100, 0);
    strokeWeight(2);
    line(plant.x, plant.y, plant.x, plant.y - plant.height);

    // Folhas/topo
    noStroke();
    fill(plant.color);
    ellipse(
      plant.x,
      plant.y - plant.height,
      30 * plant.growth,
      40 * plant.growth
    );
  }
}

function drawGardener() {
  // Chapéu
  fill(139, 69, 19); // marrom
  arc(gardenerX, gardenerY - 50, 60, 40, PI, TWO_PI);

  // Cabeça
  fill(255, 218, 185); // tom de pele
  ellipse(gardenerX, gardenerY - 60, 40, 40);

  // Corpo
  fill(70, 130, 180); // azul
  rect(gardenerX - 20, gardenerY - 40, 40, 50);

  // Pernas
  fill(0); // preto
  rect(gardenerX - 20, gardenerY + 10, 15, 30);
  rect(gardenerX + 5, gardenerY + 10, 15, 30);

  // Braços
  fill(255, 218, 185); // tom de pele
  // Braço esquerdo (segurando ferramenta)
  let armAngle = sin(frameCount * 0.1) * 0.5;
  push();
  translate(gardenerX - 20, gardenerY - 30);
  rotate(armAngle);
  rect(0, 0, 10, 30);
  pop();

  // Braço direito
  rect(gardenerX + 10, gardenerY - 30, 10, 30);
}

function animateTool() {
  let toolX = gardenerX - 30 + sin(frameCount * 0.1) * 5;
  let toolY = gardenerY - 30 + cos(frameCount * 0.1) * 5;

  // Alternar ferramentas periodicamente
  if (frameCount % 180 === 0) {
    currentTool = (currentTool + 1) % tools.length;
  }

  // Desenhar ferramenta atual
  if (tools[currentTool] === "watering-can") {
    fill(100, 100, 100);
    rect(toolX, toolY, 15, 20);
    fill(0, 100, 255, 100);
    // Água saindo
    for (let i = 0; i < 3; i++) {
      ellipse(toolX + 20, toolY + 10 + i * 5, 5, 10);
    }
  } else if (tools[currentTool] === "shovel") {
    fill(100, 100, 100);
    rect(toolX, toolY, 5, 25); // cabo
    fill(150, 150, 150);
    triangle(
      toolX + 5,
      toolY + 15,
      toolX + 15,
      toolY + 25,
      toolX + 5,
      toolY + 25
    ); // pá
  } else if (tools[currentTool] === "pruner") {
    fill(100, 100, 100);
    rect(toolX, toolY, 20, 5); // tesoura
    line(toolX + 10, toolY, toolX + 10, toolY + 10);
  }
}

function growPlants() {
  if (frameCount % 60 === 0) {
    // A cada segundo
    for (let plant of plants) {
      if (plant.growth < 1) {
        plant.growth += 0.02;
        plant.height += 1;
      }
    }
  }
}

function mouseMoved() {
  // Mover jardineiro com o mouse
  gardenerX = constrain(mouseX, 100, width - 100);
}
