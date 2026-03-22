<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Livros de Marielle Franco – Biblioteca Antiga</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: "Georgia", "Times New Roman", serif;
      background: radial-gradient(ellipse at center, #4a3a2a 0%, #3a2a1a 100%);
      color: #f0e8d0;
      line-height: 1.6;
      min-height: 100vh;
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 24px;
      background-color: rgba(70, 55, 40, 0.92);
      border-radius: 12px;
      border: 1px solid #604f3d;
      box-shadow: 0 10px 40px rgba(0, 0, 0, 0.4);
      margin-top: 30px;
      margin-bottom: 30px;
    }

    header {
      text-align: center;
      padding: 24px 0 18px;
      border-bottom: 1px solid rgba(140, 120, 100, 0.5);
    }

    header h1 {
      font-size: 2.5rem;
      color: #d4b58d;
      text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.4);
    }

    header p {
      font-size: 1.1rem;
      color: #bdaa8e;
      margin-top: 8px;
    }

    main {
      position: relative;
      margin-top: 24px;
    }

    section {
      margin-bottom: 32px;
      padding: 20px;
      background-color: rgba(90, 70, 55, 0.95);
      border-radius: 8px;
      border: 1px solid rgba(120, 100, 85, 0.5);
    }

    section h2 {
      font-size: 1.7rem;
      color: #d4b58d;
      margin-bottom: 12px;
    }

    /* Livros 3D */
    .books-row {
      display: flex;
      justify-content: center;
      gap: 40px;
      flex-wrap: wrap;
      margin: 16px 0 20px;
    }

    .book-card {
      display: flex;
      flex-direction: column;
      align-items: center;
      width: 230px;
      font-size: 0.95rem;
      text-align: center;
    }

    .book-card h3 {
      margin: 10px 0 6px 0;
      font-size: 1.15rem;
      color: #d4b58d;
    }

    .book-card p {
      margin-bottom: 6px;
      color: #bdaa8e;
      font-size: 0.95rem;
    }

    .book-holder {
      width: 184px;
      height: 244px;
      perspective: 1400px;
      margin: 12px auto 16px;
      position: relative;
    }

    .book {
      position: relative;
      width: 100%;
      height: 100%;
      transform-style: preserve-3d;
      transform: translateZ(0);
      transition: transform 1s cubic-bezier(0.645, 0.045, 0.355, 1.0);
    }

    .book.opened {
      transform: translateZ(22px) rotateY(152deg);
    }

    .book-page {
      position: absolute;
      width: 100%;
      height: 100%;
      backface-visibility: hidden;
      border-radius: 8px;
      box-shadow: 0 5px 14px rgba(0, 0, 0, 0.25);
    }

    .book-cover-placeholder {
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      border-radius: 8px;
      background-color: #5a4535;
      border: 1px solid #7a5c40;
      padding: 10px;
      text-align: center;
      font-size: 0.93rem;
      color: #d4b58d;
      line-height: 1.3;
    }

    .book-cover-placeholder strong {
      font-size: 1.05rem;
      margin-bottom: 4px;
      display: block;
    }

    .book-cover-back-placeholder {
      transform: rotateY(180deg);
      display: flex;
      justify-content: center;
      align-items: center;
      border-radius: 8px;
      background-color: #7a5c40;
      border: 1px solid #604f3d;
      padding: 10px;
      text-align: center;
      font-size: 0.9rem;
      color: #faf6ea;
    }

    .open-book-btn {
      display: inline-block;
      padding: 9px 15px;
      background-color: #a57f5a;
      color: #fff;
      border: 1px solid #8a6e50;
      border-radius: 6px;
      cursor: pointer;
      font-size: 0.97rem;
      transition: all 0.3s ease;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.18);
    }

    .open-book-btn:hover {
      background-color: #926c4e;
      transform: translateY(-1px);
    }

    .book-details {
      margin-top: 16px;
      font-size: 1.02rem;
      max-width: 720px;
      text-align: left;
      padding: 0 6px;
      color: #e8d9c0;
      display: none;
    }

    .book-details.visible {
      display: block;
    }

    /* Gráfico de barras */
    .chart-container {
      margin: 20px 0 12px;
      padding: 16px 12px;
      background-color: rgba(80, 65, 50, 0.94);
      border-radius: 6px;
      border: 1px solid rgba(110, 95, 80, 0.5);
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
    }

    .chart-bar {
      height: 28px;
      background: linear-gradient(90deg, #a57f5a, #8a6e50);
      margin-bottom: 10px;
      border-radius: 4px;
      display: flex;
      align-items: center;
      padding-left: 12px;
      color: #faf6ea;
      font-size: 0.93rem;
      transition: all 0.3s ease;
    }

    /* Quiz */
    .quiz {
      font-size: 1.02rem;
      color: #e8d9c0;
    }

    .quiz h3 {
      font-size: 1.2rem;
      color: #bdaa8e;
      margin: 10px 0 8px 0;
    }

    .quiz button {
      padding: 8px 14px;
      margin-top: 6px;
      margin-right: 8px;
      background-color: #7a5c40;
      color: #fff;
      border: 1px solid #604f3d;
      border-radius: 4px;
      cursor: pointer;
      font-size: 0.95rem;
      transition: all 0.2s ease;
    }

    .quiz button:hover {
      background-color: #6a503a;
    }

    .quiz .feedback {
      margin-top: 8px;
      padding: 8px;
      border-radius: 4px;
      font-size: 0.95rem;
    }

    .quiz .feedback.correct {
      background-color: rgba(0, 128, 0, 0.3);
      color: #d4ffcc;
    }

    .quiz .feedback.incorrect {
      background-color: rgba(160, 0, 0, 0.3);
      color: #f9b0b0;
    }

    .quiz-result {
      margin-top: 16px;
      padding: 12px;
      background-color: rgba(80, 65, 50, 0.94);
      border-radius: 6px;
      border: 1px solid rgba(110, 95, 80, 0.5);
    }

    footer {
      margin-top: 34px;
      padding: 18px 16px;
      text-align: center;
      border-top: 1px solid rgba(120, 100, 85, 0.5);
      color: #bdaa8e;
      font-size: 0.92rem;
    }
  </style>
</head>
<body>
  <div class="container">
    <header>
      <h1>Livros de Marielle Franco – Biblioteca Antiga</h1>
      <p>Um espaço imersivo com livros 3D, gráficos e quiz, sem dependência de JavaScript para navegação.</p>
    </header>

    <nav>
      <p>
        <strong>Seções:</strong>
        <a href="#biography" style="margin-right:12px; color:#d4b58d;">Biografia</a>
        <a href="#foto-book" style="margin-right:12px; color:#d4b58d;">Fotobiografia</a>
        <a href="#laboratorio" style="margin-right:12px; color:#d4b58d;">Laboratório Favela</a>
        <a href="#upp" style="margin-right:12px; color:#d4b58d;">UPP: três letras</a>
        <a href="#quiz" style="color:#d4b58d;">Quiz</a>
      </p>
    </nav>

    <main>
      <!-- Biografia -->
      <section id="biography">
        <h2>Marielle Franco em poucas palavras</h2>
        <p><strong>Marielle Franco (1979–2018)</strong> foi socióloga, vereadora do Rio de Janeiro e uma das principais vozes contra a violência policial, o racismo e a militarização das favelas.</p>
        <p>Cresceu no Complexo da Maré, vivenciou violência estatal e pobreza, e transformou essa experiência em uma trajetória de resistência e análise política.</p>
        <p>Eleita em 2016 com mais de 46 mil votos, Marielle dedicava‑se à defesa de direitos de mulheres, população negra, LGBTQIA+ e faveladas.</p>
        <p>Assassinada em 14 de março de 2018, seu nome vira símbolo internacional de luta pelos direitos humanos.</p>
      </section>

      <!-- Fotobiografia -->
      <section id="foto-book">
        <h2>Livro‑1: O Livro de Marielle Franco (Fotobiografia)</h2>
        <div class="books-row">
          <div class="book-card">
            <div class="book-holder">
              <div id="book-foto" class="book">
                <div class="book-page book-cover-placeholder">
                  <strong>O Livro de Marielle Franco</strong>
                  Fotobiografia<br />
                  Imagens e trajetória política
                </div>
                <div class="book-page book-cover-back-placeholder">
                  <p>“Fotobiografia: um olhar íntimo e político sobre Marielle.”</p>
                </div>
              </div>
            </div>
            <p><em>Fotobiografia com imagens e depoimentos de sua trajetória.</em></p>
            <button id="open-foto" class="open-book-btn">Abrir o livro</button>
            <div id="details-foto" class="book-details">
              <h3>Ideia central</h3>
              <p>Este livro mostra Marielle em sua própria voz, com fotos de infância, juventude, atos públicos e mandato, sem reduzi‑la apenas ao símbolo de seu assassinato.</p>
              <h3>Para quem é?</h3>
              <p>Para estudantes, jovens e militantes que querem conhecer sua trajetória por meio de imagens e narrativa acessível.</p>
            </div>
          </div>
        </div>
      </section>

      <!-- Laboratório Favela -->
      <section id="laboratorio">
        <h2>Livro‑2: Laboratório Favela</h2>
        <div class="books-row">
          <div class="book-card">
            <div class="book-holder">
              <div id="book-lab" class="book">
                <div class="book-page book-cover-placeholder">
                  <strong>Laboratório Favela</strong>
                  Violência y política en Río de Janeiro
                </div>
                <div class="book-page book-cover-back-placeholder">
                  <p>“Análise da favela como laboratório de violência e controle social.”</p>
                </div>
              </div>
            </div>
            <p><em>Análise crítica da militarização e da violência estatal nas favelas.</em></p>
            <button id="open-lab" class="open-book-btn">Abrir o livro</button>
            <div id="details-lab" class="book-details">
              <h3>Princípio central</h3>
              <p>Marielle mostra como a favela vira “laboratório” de políticas de segurança que combinam ocupação militar, controles e criminalização dos pobres.</p>
              <h3>Estado Penal</h3>
              <p>O livro aponta para a formação de um Estado Penal, que usa a “insegurança social” para justificar operações de exceção e suspensão de direitos.</p>
              <div class="chart-container">
                <p><strong>Temas principais (visão rápida)</strong></p>
                <div class="chart-bar" style="width: 95%;">Militarização e violência estatal</div>
                <div class="chart-bar" style="width: 80%;">Criminalização da pobreza</div>
                <div class="chart-bar" style="width: 90%;">Favela como espaço político</div>
                <div class="chart-bar" style="width: 75%;">Organização comunitária e resistência</div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- UPP: a redução da favela a três letras -->
      <section id="upp">
        <h2>Livro‑3: UPP – A redução da favela a três letras</h2>
        <div class="books-row">
          <div class="book-card">
            <div class="book-holder">
              <div id="book-upp" class="book">
                <div class="book-page book-cover-placeholder">
                  <strong>UPP</strong>
                  A redução da favela a três letras
                </div>
                <div class="book-page book-cover-back-placeholder">
                  <p>“Análise crítica das Unidades de Polícia Pacificadora no Rio de Janeiro.”</p>
                </div>
              </div>
            </div>
            <p><em>Estudo das UPPs como política de segurança e controle territorial.</em></p>
            <button id="open-upp" class="open-book-btn">Abrir o livro</button>
            <div id="details-upp" class="book-details">
              <h3>O que são as UPPs?</h3>
              <p>Unidades de Polícia Pacificadora foram postos de polícia comunitária implantados em favelas estratégicas do Rio para criar uma falsa sensação de segurança e preparar a cidade para grandes eventos.</p>
              <h3>Crítica de Marielle</h3>
              <p>Para a autora, as UPPs funcionam como ferramenta de controle seletivo, ligada a interesses imobiliários e de imagem, sem resolver a violência de forma estrutural.</p>
                            <h3>Estado Penal e encarceramento</h3>
              <p>Marielle mostra que a política de segurança amplia o encarceramento em massa e a segregação, tratando a favela como território a ser domesticado, não como sujeito político.</p>

              <div class="chart-container">
                <p><strong>Impactos das UPPs (visão rápida)</strong></p>
                <div class="chart-bar" style="width: 85%;">Fortalecimento do Estado Penal</div>
                <div class="chart-bar" style="width: 70%;">Militarização seletiva</div>
                <div class="chart-bar" style="width: 80%;">Valorização imobiliária</div>
                <div class="chart-bar" style="width: 60%;">Fracasso em reduzir violência estrutural</div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Quiz -->
      <section id="quiz">
        <h2>Quiz sobre Marielle Franco</h2>
        <p>Teste o que você já sabe sobre a vida e a obra de Marielle Franco.</p>

        <div class="quiz">
          <div id="q1">
            <h3>1. Em que cidade Marielle Franco foi vereadora?</h3>
            <button class="quiz-btn" onclick="check(1, 0)">a) São Paulo</button>
            <button class="quiz-btn" onclick="check(1, 1)">b) Rio de Janeiro</button>
            <button class="quiz-btn" onclick="check(1, 2)">c) Belo Horizonte</button>
            <button class="quiz-btn" onclick="check(1, 3)">d) Salvador</button>
            <div id="fb1" class="feedback" style="display: none;"></div>
          </div>

          <div id="q2" style="margin-top: 16px;">
            <h3>2. Qual é o tema central do livro “Laboratório Favela”?</h3>
            <button class="quiz-btn" onclick="check(2, 0)">a) Moda nas favelas</button>
            <button class="quiz-btn" onclick="check(2, 1)">b) Violência e política nas favelas do Rio</button>
            <button class="quiz-btn" onclick="check(2, 2)">c) Economia informal</button>
            <button class="quiz-btn" onclick="check(2, 3)">d) História da arquitetura</button>
            <div id="fb2" class="feedback" style="display: none;"></div>
          </div>

          <div id="q3" style="margin-top: 16px;">
            <h3>3. O que significa UPP no contexto da obra de Marielle?</h3>
            <button class="quiz-btn" onclick="check(3, 0)">a) Unidade de Políticas Públicas</button>
            <button class="quiz-btn" onclick="check(3, 1)">b) Unidades de Polícia Pacificadora</button>
            <button class="quiz-btn" onclick="check(3, 2)">c) Unidade de Produção Popular</button>
            <button class="quiz-btn" onclick="check(3, 3)">d) Unidade de Planejamento Profissional</button>
            <div id="fb3" class="feedback" style="display: none;"></div>
          </div>

          <div id="q4" style="margin-top: 16px;">
            <h3>4. Em que ano Marielle foi eleita vereadora?</h3>
            <button class="quiz-btn" onclick="check(4, 0)">a) 2012</button>
            <button class="quiz-btn" onclick="check(4, 1)">b) 2014</button>
            <button class="quiz-btn" onclick="check(4, 2)">c) 2016</button>
            <button class="quiz-btn" onclick="check(4, 3)">d) 2018</button>
            <div id="fb4" class="feedback" style="display: none;"></div>
          </div>

          <div id="q5" style="margin-top: 16px;">
            <h3>5. Qual é o foco da “fotobiografia” de Marielle?</h3>
            <button class="quiz-btn" onclick="check(5, 0)">a) Receitas de comida típica</button>
            <button class="quiz-btn" onclick="check(5, 1)">b) Memórias de infância em formato de fotos</button>
            <button class="quiz-btn" onclick="check(5, 2)">c) Análise estatística de violência</button>
            <button class="quiz-btn" onclick="check(5, 3)">d) Mapas urbanos de favelas</button>
            <div id="fb5" class="feedback" style="display: none;"></div>
          </div>

          <div id="quiz-result" class="quiz-result" style="display: none;">
            <p id="quiz-result-text"></p>
          </div>
        </div>
      </section>
    </main>

    <footer>
      <p>Site e biblioteca virtual dedicada à memória e à produção intelectual de <strong>Marielle Franco</strong>.</p>
    </footer>
  </div>

  <script>
    // Livro 1 – Fotobiografia
    const bookFoto = document.getElementById("book-foto");
    const openBtnFoto = document.getElementById("open-foto");
    const detailsFoto = document.getElementById("details-foto");

    openBtnFoto.addEventListener("click", function() {
      bookFoto.classList.toggle("opened");
      detailsFoto.classList.toggle("visible");
      openBtnFoto.textContent = detailsFoto.classList.contains("visible")
        ? "Fechar o livro"
        : "Abrir o livro";
    });

    // Livro 2 – Laboratório Favela
    const bookLab = document.getElementById("book-lab");
    const openBtnLab = document.getElementById("open-lab");
    const detailsLab = document.getElementById("details-lab");

    openBtnLab.addEventListener("click", function() {
      bookLab.classList.toggle("opened");
      detailsLab.classList.toggle("visible");
      openBtnLab.textContent = detailsLab.classList.contains("visible")
        ? "Fechar o livro"
        : "Abrir o livro";
    });

    // Livro 3 – UPP
    const bookUpp = document.getElementById("book-upp");
    const openBtnUpp = document.getElementById("open-upp");
    const detailsUpp = document.getElementById("details-upp");

    openBtnUpp.addEventListener("click", function() {
      bookUpp.classList.toggle("opened");
      detailsUpp.classList.toggle("visible");
      openBtnUpp.textContent = detailsUpp.classList.contains("visible")
        ? "Fechar o livro"
        : "Abrir o livro";
    });

    // Quiz (5 perguntas)
    let score = 0;
    const total = 5;

    function check(q, index) {
      const feedback = document.getElementById("fb" + q);
      const resultText = document.getElementById("quiz-result-text");

      feedback.style.display = "block";

      switch (q) {
        case 1:
          if (index === 1) {
            feedback.textContent = "✅ Correto! Marielle foi vereadora do Rio de Janeiro.";
            feedback.classList.add("correct");
            score++;
          } else {
            feedback.textContent = "❌ Errado. A cidade correta é o Rio de Janeiro.";
            feedback.classList.add("incorrect");
          }
          break;
        case 2:
          if (index === 1) {
            feedback.textContent = "✅ Correto! O foco é violência e política nas favelas.";
            feedback.classList.add("correct");
            score++;
          } else {
            feedback.textContent = "❌ Errado. O livro fala de violência e política nas favelas.";
            feedback.classList.add("incorrect");
          }
          break;
        case 3:
          if (index === 1) {
            feedback.textContent = "✅ Correto! UPP = Unidades de Polícia Pacificadora.";
            feedback.classList.add("correct");
            score++;
          } else {
            feedback.textContent = "❌ Errado. UPP é Unidades de Polícia Pacificadora.";
            feedback.classList.add("incorrect");
          }
          break;
        case 4:
          if (index === 2) {
            feedback.textContent = "✅ Correto! Marielle foi eleita em 2016.";
            feedback.classList.add("correct");
            score++;
          } else {
            feedback.textContent = "❌ Errado. O ano correto é 2016.";
            feedback.classList.add("incorrect");
          }
          break;
        case 5:
          if (index === 1) {
            feedback.textContent = "✅ Correto! A fotobiografia foca em imagens de sua trajetória.";
            feedback.classList.add("correct");
            score++;
          } else {
            feedback.textContent = "❌ Errado. A fotobiografia usa imagens e memórias.";
            feedback.classList.add("incorrect");
          }
          break;
      }

      // Mostra resultado após responder todas
      if (q === 5) {
        const percentage = Math.round((score / total) * 100);
        resultText.textContent = `Você acertou ${score}/${total} (${percentage}%). Parabéns!`;
        document.getElementById("quiz-result").style.display = "block";
      }
    }
  </script>
</body>
</html>
