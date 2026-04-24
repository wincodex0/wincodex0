# 🚀 Hi there, I'm [Your Name]!

Welcome to my GitHub profile! Feel free to explore my repositories and projects.

---

## 🎮 Interactive Contribution Game

Click on the target to fire a rocket and create a fire explosion!

<div align="center">
  <iframe 
    srcdoc="
<!DOCTYPE html>
<html>
<head>
  <style>
    body { margin: 0; overflow: hidden; background: linear-gradient(180deg, #87CEEB 0%, #E0F6FF 100%); }
    canvas { display: block; }
  </style>
</head>
<body>
  <canvas id='rocketCanvas' width='600' height='400'></canvas>
  <script>
    const canvas = document.getElementById('rocketCanvas');
    const ctx = canvas.getContext('2d');

    let rocket = { x: 50, y: 350, width: 20, height: 40, vx: 0, vy: 0, launched: false, angle: 0 };
    let target = { x: 500, y: 100, width: 80, height: 80, hit: false };
    let fireParticles = [];

    class FireParticle {
      constructor(x, y) {
        this.x = x; this.y = y;
        this.vx = (Math.random() - 0.5) * 4;
        this.vy = Math.random() * -3 - 1;
        this.life = 1;
        this.decay = Math.random() * 0.03 + 0.02;
        this.size = Math.random() * 20 + 10;
      }
      update() {
        this.x += this.vx;
        this.y += this.vy;
        this.vy -= 0.1;
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
      ctx.fillStyle = '#FF4444';
      ctx.fillRect(-rocket.width / 2, 0, rocket.width, rocket.height);
      ctx.fillStyle = '#FFFF00';
      ctx.beginPath();
      ctx.arc(0, 10, 4, 0, Math.PI * 2);
      ctx.fill();
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
      ctx.fillStyle = target.hit ? '#888888' : '#FF6B6B';
      ctx.fillRect(target.x, target.y, target.width, target.height);
      ctx.fillStyle = '#FFFFFF';
      ctx.font = 'bold 16px Arial';
      ctx.textAlign = 'center';
      ctx.textBaseline = 'middle';
      ctx.fillText('No Contrib', target.x + target.width / 2, target.y + target.height / 2);
    }

    function update() {
      if (rocket.launched) {
        rocket.x += rocket.vx;
        rocket.y += rocket.vy;
        rocket.vy += 0.3;
        if (rocket.x > target.x && rocket.x < target.x + target.width &&
            rocket.y > target.y && rocket.y < target.y + target.height && !target.hit) {
          target.hit = true;
          rocket.launched = false;
          for (let i = 0; i < 30; i++) {
            fireParticles.push(new FireParticle(target.x + target.width / 2, target.y + target.height / 2));
          }
          setTimeout(() => { target.hit = false; }, 2000);
        }
        if (rocket.y > canvas.height || rocket.x > canvas.width) {
          rocket.launched = false;
          rocket.x = 50;
          rocket.y = 350;
        }
      }
      fireParticles = fireParticles.filter(p => p.life > 0);
      fireParticles.forEach(p => p.update());
    }

    function draw() {
      ctx.fillStyle = 'rgba(135, 206, 235, 0.1)';
      ctx.fillRect(0, 0, canvas.width, canvas.height);
      drawTarget();
      drawRocket();
      fireParticles.forEach(p => p.draw());
      requestAnimationFrame(draw);
      update();
    }

    canvas.addEventListener('click', (e) => {
      if (!rocket.launched) {
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const dx = mouseX - rocket.x;
        const dy = mouseY - rocket.y;
        rocket.angle = Math.atan2(dy, dx);
        const speed = 8;
        rocket.vx = Math.cos(rocket.angle) * speed;
        rocket.vy = Math.sin(rocket.angle) * speed;
        rocket.launched = true;
      }
    });

    draw();
  </script>
</body>
</html>
" 
    width="600" 
    height="400" 
    style="border: 2px solid #333; border-radius: 8px; background: #87CEEB;">
  </iframe>
</div>

**Click anywhere on the canvas to launch a rocket!** Hit the "No Contrib" target to see a fire explosion! 🎆

---

## 📊 About Me

- 💻 Passionate developer
- 🚀 Always learning and building
- 🎯 Love creating interactive experiences

## 🛠️ Tech Stack

- JavaScript
- HTML5 & CSS3
- Canvas API
- React/Vue/Angular (add your frameworks)

## 📫 Get in Touch

- **Email**: your.email@example.com
- **LinkedIn**: [Your LinkedIn Profile](https://linkedin.com)
- **Twitter**: [@YourHandle](https://twitter.com)

---

<div align="center">

### 🌟 My Stats

![GitHub stats](https://github-readme-stats.vercel.app/api?username=YOUR_USERNAME&show_icons=true&theme=radical)

[![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=YOUR_USERNAME&layout=compact&theme=radical)](https://github.com/anuraghazra/github-readme-stats)

</div>

---

*Thanks for visiting! 🚀*
