# 🚀 Hi there, I'm [WinCodex]!

Welcome to my GitHub profile! Feel free to explore my repositories and projects.

---

## 🎮 Interactive Contribution Game

Click on the calendar date below to fire a rocket and create a fire explosion! 

<div align="center">
  <canvas id="rocketCanvas" width="600" height="400" style="border: 2px solid #333; background: linear-gradient(180deg, #87CEEB 0%, #E0F6FF 100%); cursor: pointer; border-radius: 8px;"></canvas>
</div>

<script>
  const canvas = document.getElementById('rocketCanvas');
  const ctx = canvas.getContext('2d');

  // Game variables
  let rocket = {
    x: 50,
    y: canvas.height - 50,
    width: 20,
    height: 40,
    vx: 0,
    vy: 0,
    launched: false,
    angle: 0
  };

  let target = {
    x: canvas.width - 100,
    y: 100,
    width: 80,
    height: 80,
    hit: false
  };

  let particles = [];
  let fireParticles = [];

  class Particle {
    constructor(x, y, vx, vy, color) {
      this.x = x;
      this.y = y;
      this.vx = vx;
      this.vy = vy;
      this.color = color;
      this.life = 1;
      this.decay = Math.random() * 0.02 + 0.01;
    }

    update() {
      this.x += this.vx;
      this.y += this.vy;
      this.vy += 0.2; // gravity
      this.life -= this.decay;
    }

    draw() {
      ctx.save();
      ctx.globalAlpha = this.life;
      ctx.fillStyle = this.color;
      ctx.beginPath();
      ctx.arc(this.x, this.y, 3, 0, Math.PI * 2);
      ctx.fill();
      ctx.restore();
    }
  }

  class FireParticle {
    constructor(x, y) {
      this.x = x;
      this.y = y;
      this.vx = (Math.random() - 0.5) * 4;
      this.vy = Math.random() * -3 - 1;
      this.life = 1;
      this.decay = Math.random() * 0.03 + 0.02;
      this.size = Math.random() * 20 + 10;
    }

    update() {
      this.x += this.vx;
      this.y += this.vy;
      this.vy -= 0.1; // rise effect
      this.life -= this.decay;
      this.size *= 0.95;
    }

    draw() {
      ctx.save();
      ctx.globalAlpha = this.life;
      const gradient = ctx.createRadialGradient(this.x, this.y, 0, this.x, this.y, this.size);
      gradient.addColorStop(0, 'rgba(255, 200, 0, 1)');
      gradient.addColorStop(0.5, 'rgba(255, 100, 0, 0.5)');
      gradient.addColorStop(1, 'rgba(255, 0, 0, 0)');
      ctx.fillStyle = gradient;
      ctx.beginPath();
      ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
      ctx.fill();
      ctx.restore();
    }
  }

  function drawRocket() {
    ctx.save();
    ctx.translate(rocket.x, rocket.y);
    ctx.rotate(rocket.angle);

    // Rocket body
    ctx.fillStyle = '#FF4444';
    ctx.fillRect(-rocket.width / 2, 0, rocket.width, rocket.height);

    // Rocket window
    ctx.fillStyle = '#FFFF00';
    ctx.beginPath();
    ctx.arc(0, 10, 4, 0, Math.PI * 2);
    ctx.fill();

    // Rocket fins
    ctx.fillStyle = '#0066FF';
    ctx.beginPath();
    ctx.moveTo(-rocket.width / 2, rocket.height - 10);
    ctx.lineTo(-rocket.width, rocket.height);
    ctx.lineTo(-rocket.width / 2, rocket.height);
    ctx.fill();

    ctx.beginPath();
    ctx.moveTo(rocket.width / 2, rocket.height - 10);
    ctx.lineTo(rocket.width, rocket.height);
    ctx.lineTo(rocket.width / 2, rocket.height);
    ctx.fill();

    // Rocket flame (when launched)
    if (rocket.launched) {
      ctx.fillStyle = '#FF6600';
      ctx.beginPath();
      ctx.moveTo(-rocket.width / 2, rocket.height);
      ctx.lineTo(rocket.width / 2, rocket.height);
      ctx.lineTo(0, rocket.height + 15);
      ctx.fill();
    }

    ctx.restore();
  }

  function drawTarget() {
    ctx.save();
    ctx.fillStyle = target.hit ? '#888888' : '#FF6B6B';
    ctx.fillRect(target.x, target.y, target.width, target.height);

    ctx.fillStyle = '#FFFFFF';
    ctx.font = 'bold 20px Arial';
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';
    ctx.fillText('No Contrib', target.x + target.width / 2, target.y + target.height / 2);

    ctx.restore();
  }

  function drawUI() {
    ctx.fillStyle = '#000000';
    ctx.font = '14px Arial';
    ctx.fillText('Click to launch rocket! Angle: ' + Math.round(rocket.angle * 180 / Math.PI) + '°', 10, 20);
  }

  function update() {
    if (rocket.launched) {
      rocket.x += rocket.vx;
      rocket.y += rocket.vy;
      rocket.vy += 0.3; // gravity

      // Check collision with target
      if (
        rocket.x > target.x &&
        rocket.x < target.x + target.width &&
        rocket.y > target.y &&
        rocket.y < target.y + target.height &&
        !target.hit
      ) {
        target.hit = true;
        rocket.launched = false;

        // Create fire effect
        for (let i = 0; i < 30; i++) {
          fireParticles.push(new FireParticle(target.x + target.width / 2, target.y + target.height / 2));
        }

        // Reset after 2 seconds
        setTimeout(() => {
          target.hit = false;
          rocket.launched = false;
          rocket.x = 50;
          rocket.y = canvas.height - 50;
        }, 2000);
      }

      // Out of bounds reset
      if (rocket.y > canvas.height || rocket.x > canvas.width) {
        rocket.launched = false;
        rocket.x = 50;
        rocket.y = canvas.height - 50;
      }
    }

    // Update particles
    particles = particles.filter(p => p.life > 0);
    particles.forEach(p => p.update());

    fireParticles = fireParticles.filter(p => p.life > 0);
    firePar
