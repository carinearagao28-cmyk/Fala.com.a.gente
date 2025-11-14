<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Feira de TI Criativa - Dinâmico</title>
  <!-- Biblioteca do EmailJS -->
  <script src="https://cdn.emailjs.com/sdk/3.2.0/email.min.js"></script>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Fredoka+One&family=Comic+Neue&display=swap');

    * {
      margin: 0; padding: 0; box-sizing: border-box;
    }

    body {
      background-color: #007f00; /* verde */
      color: white;
      font-family: 'Comic Neue', cursive, sans-serif;
      min-height: 100vh;
      overflow-x: hidden;
      padding: 20px;
      position: relative;
    }

    header {
      font-family: 'Fredoka One', cursive;
      font-size: 3em;
      color: #e60000; /* vermelho */
      text-align: center;
      margin-bottom: 30px;
      text-shadow: 2px 2px 4px black;
      user-select: none;
    }

    /* Background shapes inspired by the image */
    .decorations {
      position: fixed;
      top: 0; left: 0;
      width: 100vw; height: 100vh;
      pointer-events: none;
      z-index: 0;
      overflow: hidden;
    }

    .shape {
      position: absolute;
      fill: none;
      stroke-width: 3px;
      stroke-linejoin: round;
      stroke-linecap: round;
      stroke: #e60000;
      animation: float 5s ease-in-out infinite alternate;
    }

    .scissors {
      top: 10%;
      left: 5%;
      width: 150px;
      animation-delay: 0s;
    }

    .ruler {
      bottom: 15%;
      right: 5%;
      width: 140px;
      animation-delay: 2s;
    }

    .paperclip {
      top: 40%;
      right: 20%;
      width: 60px;
      animation-delay: 4s;
    }

    @keyframes float {
      0% { transform: translateY(0) translateX(0); }
      100% { transform: translateY(10px) translateX(3px); }
    }

    main {
      position: relative;
      z-index: 2;
      max-width: 900px;
      margin: 0 auto;
    }

    section {
      background: white;
      border-radius: 20px;
      margin-bottom: 30px;
      padding: 25px;
      color: black;
      box-shadow: 0 10px 20px rgba(0,0,0,0.3);
      transition: transform 0.35s ease;
      cursor: default;
    }
    section:hover {
      transform: scale(1.05);
      box-shadow: 0 15px 30px rgba(0,0,0,0.5);
    }

    h2 {
      color: #007f00;
      font-family: 'Fredoka One', cursive;
      font-size: 2em;
      margin-bottom: 15px;
      text-align: center;
      user-select: none;
    }

    p {
      font-size: 1.1em;
      line-height: 1.6em;
      user-select: text;
    }

    /* Time / Integrantes Grid */
    .team {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
      gap: 20px;
      justify-items: center;
    }

    .team-member {
      text-align: center;
      cursor: pointer;
      transition: transform 0.3s ease;
    }
    .team-member:hover {
      transform: scale(1.1);
    }
    .team-member img {
      width: 140px;
      height: 140px;
      object-fit: cover;
      border-radius: 50%;
      border: 5px solid #e60000;
      box-shadow: 0 0 15px #007f00;
      display: block;
      margin: 0 auto 10px auto;
      user-select: none;
    }
    .team-member p {
      font-weight: bold;
      color: #007f00;
    }

    /* Estilo do formulário "Fala com a Gente" */
    #fala {
      background: #e60000;
      color: white;
      padding: 30px;
      border-radius: 20px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.6);
      position: relative;
      overflow: hidden;
    }

    #fala h2 {
      color: white;
      margin-bottom: 30px;
    }

    #contatoForm {
      display: flex;
      flex-direction: column;
      gap: 15px;
      max-width: 480px;
      margin: 0 auto 15px auto;
    }

    input, textarea {
      padding: 12px;
      border-radius: 12px;
      border: none;
      font-size: 1em;
      font-family: inherit;
      resize: vertical;
      box-shadow: inset 0 0 7px rgba(255,255,255,0.3);
    }
    input:focus, textarea:focus {
      outline: 2px solid #007f00;
      box-shadow: inset 0 0 10px #00ff00;
    }

    button {
      padding: 15px 20px;
      background: #007f00;
      color: white;
      font-size: 1.2em;
      font-weight: 700;
      cursor: pointer;
      border-radius: 15px;
      transition: background-color 0.3s ease;
      font-family: 'Fredoka One', cursive;
      user-select: none;
    }
    button:hover {
      background-color: #004900;
    }

    #resposta {
      text-align: center;
      font-weight: bold;
      margin-top: 15px;
      user-select: none;
    }

    /* QR code style */
    .qr-container {
      max-width: 300px;
      margin: 30px auto 0;
      background: white;
      border: 6px solid #007f00;
      border-radius: 25px;
      padding: 15px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.4);
      text-align: center;
      user-select: none;
    }

    .qr-container p {
      margin-top: 10px;
      font-weight: bold;
      color: white;
      text-shadow: 1px 1px 3px black;
      font-size: 1.5em;
      font-family: 'Fredoka One', cursive;
    }

    .qr-name {
      color: white;
      font-weight: bold;
      font-size: 1.3em;
      margin-bottom: 8px;
      user-select: text;
    }

    /* Rodapé */
    footer {
      margin-top: 40px;
      color: white;
      text-align: center;
      font-size: 0.95em;
      text-shadow: 1px 1px 2px black;
      user-select: none;
    }

    /* Responsividade */
    @media (max-width: 600px) {
      section {
        padding: 20px 15px;
      }
      .team-member img {
        width: 100px;
        height: 100px;
      }
      #contatoForm {
        max-width: 100%;
      }
      .qr-container {
        max-width: 80vw;
        padding: 10px;
      }
    }
  </style>
</head>

<body>

<header>Feira de TI Criativa</header>

<div class="decorations">
  <!-- Tesoura SVG -->
  <svg class="shape scissors" viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
    <circle cx="18" cy="18" r="12" stroke="#e60000"/>
    <line x1="32" y1="32" x2="62" y2="62" stroke="#e60000"/>
    <line x1="42" y1="22" x2="62" y2="42" stroke="#e60000"/>
  </svg>

  <!-- Régua triângulo -->
  <svg class="shape ruler" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
    <polygon points="0,100 100,100 0,0" stroke="#e60000" fill="none" />
    <line x1="10" y1="90" x2="10" y2="100" stroke="#e60000" />
    <line x1="20" y1="80" x2="20" y2="100" stroke="#e60000" />
    <line x1="30" y1="70" x2="30" y2="100" stroke="#e60000" />
    <line x1="40" y1="60" x2="40" y2="100" stroke="#e60000" />
    <line x1="50" y1="50" x2="50" y2="100" stroke="#e60000" />
  </svg>

  <!-- Paperclip SVG -->
  <svg class="shape paperclip" viewBox="0 0 24 64" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
    <path d="M6 2 L18 2L18 50 a6 6 0 1 1 -12 0L18 50" stroke="#e60000" />
  </svg>
</div>

<main>
  <section id="trabalho" aria-label="Nosso trabalho">
    <h2>Nosso Trabalho</h2>
    <p>Somos apaixonados por tecnologia! Criamos soluções modernas e acessíveis, valorizando a experiência do usuário e a criatividade. Nosso projeto envolve inovação, colaboração e muito entusiasmo.</p>
  </section>

  <section id="historia" aria-label="História do projeto">
    <h2>História do Projeto</h2>
    <p>Este site nasceu da vontade de refletir nossa identidade criativa e o amor pela tecnologia. Com muito esforço do nosso time, estamos construindo uma plataforma que conecta todos da feira com interatividade e design divertido.</p>
  </section>

  <section id="objetivo" aria-label="Objetivos do projeto">
    <h2>Objetivo</h2>
    <p>Nosso principal objetivo é divulgar os projetos de TI do nosso grupo, facilitar a comunicação entre visitantes e expositores e incentivar a colaboração, tudo isso num ambiente online acessível e amigável.</p>
  </section>

  <section id="integrantes" aria-label="Equipe">
    <h2>Nossa Equipe</h2>
    <div class="team" role="list">
      <div class="team-member" role="listitem" tabindex="0" aria-label="Integrante 1">
        <img src="foto1.jpg" alt="Foto do Integrante 1" />
        <p>Integrante 1</p>
      </div>
      <div class="team-member" role="listitem" tabindex="0" aria-label="Integrante 2">
        <img src="foto2.jpg" alt="Foto do Integrante 2" />
        <p>Integrante 2</p>
      </div>
      <div class="team-member" role="listitem" tabindex="0" aria-label="Integrante 3">
        <img src="foto3.jpg" alt="Foto do Integrante 3" />
        <p>Integrante 3</p>
      </div>
      <div class="team-member" role="listitem" tabindex="0" aria-label="Integrante 4">
        <img src="foto4.jpg" alt="Foto do Integrante 4" />
        <p>Integrante 4</p>
      </div>
      <div class="team-member" role="listitem" tabindex="0" aria-label="Integrante 5">
        <img src="foto5.jpg" alt="Foto do Integrante 5" />
        <p>Integrante 5</p>
      </div>
    </div>
  </section>

  <section id="fala" aria-label="Contato e dúvidas">
    <h2>Fala com a Gente</h2>
    <form id="contatoForm" aria-describedby="resposta">
      <input type="text" name="nome" placeholder="Seu nome" aria-label="Digite seu nome" required />
      <input type="email" name="email" placeholder="Seu e-mail" aria-label="Digite seu e-mail" required />
      <textarea name="mensagem" rows="5" placeholder="Sua mensagem ou dúvida" aria-label="Digite sua mensagem ou dúvida" required></textarea>
      <button type="submit">Enviar</button>
    </form>

    <p id="resposta" role="alert" aria-live="polite" style="display:none; color:#00ff00; font-weight:bold;"></p>

    <div class="qr-container" aria-label="QR code para contato de Erick Regis de Jesus Santos">
      <div class="qr-name">Erick Regis de Jesus Santos</div>
      <img src="https://api.qrserver.com/v1/create-qr-code/?size=200x200&data=mailto:erick.regis@example.com" alt="QR Code para contato" />
      <p>2º TIM1</p>
    </div>

  </section>
</main>

<footer>
  Feira de TI Criativa &copy; 2025- Desenvolvido pela equipe
</footer>

<script>
  // Inicialize EmailJS com seu user ID (substitua 'YOUR_USER_ID')
  emailjs.init('YOUR_USER_ID');

  const form = document.getElementById('contatoForm');
  const resposta = document.getElementById('resposta');

  form.addEventListener('submit', function(event) {
    event.preventDefault();

    // Envia o formulário usando EmailJS (substitua 'YOUR_SERVICE_ID' e 'YOUR_TEMPLATE_ID')
    emailjs.sendForm('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', this)
      .then(function() {
        resposta.style.display = 'block';
        resposta.style.color = '#00ff00';
        resposta.textContent = 'Mensagem enviada com sucesso! Obrigado pelo contato.';
        form.reset();
      }, function(error) {
        resposta.style.display = 'block';
        resposta.style.color = 'red';
        resposta.textContent = 'Erro ao enviar a mensagem. Tente novamente mais tarde.';
        console.error('EmailJS error:', error);
      });
  });
</script>

</body>
</html>
 
