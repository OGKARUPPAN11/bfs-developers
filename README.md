<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>BFS Developers | Futuristic Dev Portal</title>
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;600;700&display=swap" rel="stylesheet" />
  <style>
    :root {
      --bg: #090d16;
      --card-bg: rgba(16, 24, 40, 0.75);
      --accent: #00f2fe;
      --accent-glow: #4facfe;
      --text: #e2e8f0;
      --muted: #94a3b8;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Space Grotesk', sans-serif;
    }

    body {
      background: radial-gradient(circle at 50% 0%, #151d3b, var(--bg));
      color: var(--text);
      min-height: 100vh;
      overflow-x: hidden;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 40px 20px;
    }

    header {
      text-align: center;
      margin-bottom: 40px;
    }

    .badge {
      display: inline-block;
      padding: 6px 16px;
      font-size: 0.85rem;
      color: var(--accent);
      background: rgba(0, 242, 254, 0.1);
      border: 1px solid rgba(0, 242, 254, 0.3);
      border-radius: 999px;
      margin-bottom: 16px;
      letter-spacing: 1.5px;
      text-transform: uppercase;
    }

    h1 {
      font-size: clamp(2rem, 5vw, 3.5rem);
      font-weight: 700;
      background: linear-gradient(135deg, #fff 30%, var(--accent) 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      margin-bottom: 12px;
    }

    p.subtitle {
      color: var(--muted);
      font-size: 1.1rem;
      max-width: 550px;
      margin: 0 auto;
    }

    .glass-card {
      background: var(--card-bg);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border: 1px solid rgba(255, 255, 255, 0.1);
      border-radius: 20px;
      padding: 36px;
      width: 100%;
      max-width: 650px;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4), 0 0 30px rgba(0, 242, 254, 0.1);
    }

    .form-group {
      margin-bottom: 22px;
    }

    label {
      display: block;
      font-size: 0.9rem;
      font-weight: 600;
      margin-bottom: 8px;
      color: #cbd5e1;
    }

    input, select, textarea {
      width: 100%;
      background: rgba(255, 255, 255, 0.04);
      border: 1px solid rgba(255, 255, 255, 0.15);
      border-radius: 10px;
      padding: 14px 16px;
      color: #fff;
      font-size: 1rem;
      outline: none;
      transition: all 0.3s ease;
    }

    input:focus, select:focus, textarea:focus {
      border-color: var(--accent);
      box-shadow: 0 0 12px rgba(0, 242, 254, 0.3);
      background: rgba(255, 255, 255, 0.08);
    }

    select option {
      background: #0d1527;
      color: #fff;
    }

    textarea {
      resize: vertical;
      min-height: 100px;
    }

    .btn-submit {
      width: 100%;
      padding: 16px;
      font-size: 1.1rem;
      font-weight: 700;
      color: #050a14;
      background: linear-gradient(135deg, var(--accent), var(--accent-glow));
      border: none;
      border-radius: 10px;
      cursor: pointer;
      box-shadow: 0 4px 20px rgba(0, 242, 254, 0.4);
      transition: transform 0.2s, box-shadow 0.2s;
    }

    .btn-submit:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 28px rgba(0, 242, 254, 0.6);
    }

    #successMsg {
      display: none;
      margin-top: 20px;
      padding: 16px;
      border-radius: 10px;
      background: rgba(16, 185, 129, 0.15);
      border: 1px solid rgba(16, 185, 129, 0.4);
      color: #6ee7b7;
      text-align: center;
      font-weight: 600;
    }
  </style>
</head>
<body>

  <header>
    <div class="badge">Next-Gen Tech Hub</div>
    <h1>BFS DEVELOPERS</h1>
    <p class="subtitle">Join our developer ecosystem. Share your technical stack and build the future together.</p>
  </header>

  <div class="glass-card">
    <form id="devForm">
      <div class="form-group">
        <label for="fullName">Full Name</label>
        <input type="text" id="fullName" placeholder="e.g. Logesh Kanna" required />
      </div>

      <div class="form-group">
        <label for="email">Email Address</label>
        <input type="email" id="email" placeholder="e.g. dev@example.com" required />
      </div>

      <div class="form-group">
        <label for="primaryRole">Primary Role / Domain</label>
        <select id="primaryRole" required>
          <option value="" disabled selected>Select your domain</option>
          <option value="Game Developer">Game Developer (Roblox / Unity / Unreal)</option>
          <option value="Full-Stack Developer">Full-Stack Web Developer</option>
          <option value="Python / AI Specialist">Python / AI Specialist</option>
          <option value="UI/UX Designer">UI/UX & Creative Designer</option>
        </select>
      </div>

      <div class="form-group">
        <label for="techStack">Primary Skills & Tech Stack</label>
        <input type="text" id="techStack" placeholder="e.g. Luau, Python, React, HTML/CSS" required />
      </div>

      <div class="form-group">
        <label for="portfolio">Portfolio / GitHub / Profile Link</label>
        <input type="url" id="portfolio" placeholder="https://github.com/your-username" />
      </div>

      <div class="form-group">
        <label for="notes">Brief Bio or Project Vision</label>
        <textarea id="notes" placeholder="Tell us about the cool stuff you are building..."></textarea>
      </div>

      <button type="submit" class="btn-submit">Submit Profile</button>
    </form>

    <div id="successMsg">✨ Application submitted successfully! Welcome to BFS Developers.</div>
  </div>

  <script>
    document.getElementById('devForm').addEventListener('submit', function(e) {
      e.preventDefault();
      
      const data = {
        name: document.getElementById('fullName').value,
        email: document.getElementById('email').value,
        role: document.getElementById('primaryRole').value,
        stack: document.getElementById('techStack').value,
        portfolio: document.getElementById('portfolio').value,
        notes: document.getElementById('notes').value,
        timestamp: new Date().toISOString()
      };

      console.log('BFS Developer Registration:', data);

      document.getElementById('devForm').reset();
      const msg = document.getElementById('successMsg');
      msg.style.display = 'block';

      setTimeout(() => {
        msg.style.display = 'none';
      }, 5000);
    });
  </script>
</body>
</html>
