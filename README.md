<html lang="th">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>เกมอ่านจับใจความสำคัญ ม.2</title>

  <style>
    *{
      margin:0;
      padding:0;
      box-sizing:border-box;
      font-family: "Prompt", sans-serif;
    }

    body{
      background: linear-gradient(135deg,#4facfe,#00f2fe);
      min-height:100vh;
      padding:30px;
      color:#333;
    }

    .container{
      max-width:1000px;
      margin:auto;
      background:white;
      border-radius:25px;
      padding:30px;
      box-shadow:0 10px 30px rgba(0,0,0,0.2);
    }

    .title{
      text-align:center;
      margin-bottom:20px;
    }

    .title h1{
      color:#0f4c81;
      font-size:40px;
    }

    .title p{
      color:#666;
      margin-top:10px;
    }

    .game-box{
      margin-top:25px;
    }

    .story{
      background:#f3f9ff;
      border-left:8px solid #2196f3;
      padding:25px;
      border-radius:15px;
      line-height:1.8;
      font-size:18px;
    }

    .question{
      margin-top:25px;
      font-size:24px;
      font-weight:bold;
      color:#0f4c81;
    }

    .choices{
      margin-top:20px;
      display:grid;
      gap:15px;
    }

    .btn{
      padding:18px;
      border:none;
      border-radius:15px;
      background:#e3f2fd;
      font-size:18px;
      cursor:pointer;
      transition:0.3s;
      text-align:left;
    }

    .btn:hover{
      background:#90caf9;
      transform:scale(1.02);
    }

    .correct{
      background:#66bb6a !important;
      color:white;
    }

    .wrong{
      background:#ef5350 !important;
      color:white;
    }

    .result{
      margin-top:25px;
      padding:20px;
      border-radius:15px;
      font-size:20px;
      display:none;
    }

    .next-btn{
      margin-top:20px;
      padding:15px 25px;
      border:none;
      border-radius:15px;
      background:#0f4c81;
      color:white;
      font-size:18px;
      cursor:pointer;
      display:none;
    }

    .score-board{
      margin-top:20px;
      text-align:right;
      font-size:20px;
      color:#0f4c81;
      font-weight:bold;
    }

    .finish{
      text-align:center;
      padding:30px;
    }

    .finish h2{
      font-size:40px;
      color:#0f4c81;
    }

    .finish p{
      margin-top:15px;
      font-size:24px;
    }

    .restart{
      margin-top:25px;
      padding:15px 30px;
      border:none;
      border-radius:15px;
      background:#ff9800;
      color:white;
      font-size:20px;
      cursor:pointer;
    }

  </style>
</head>
<body>

  <div class="container">

    <div class="title">
      <h1>📚 เกมอ่านจับใจความสำคัญ</h1>
      <p>วิชาภาษาไทย ชั้นมัธยมศึกษาปีที่ 2</p>
    </div>

    <div class="score-board">
      คะแนน: <span id="score">0</span>
    </div>

    <div class="game-box" id="gameBox">

    </div>

  </div>

  <script>

    const questions = [

      {
        story: `
        ในช่วงปิดภาคเรียน ต้นกล้าตั้งใจจะใช้เวลาให้เกิดประโยชน์
        เขาจึงสมัครเข้าร่วมกิจกรรมอาสาพัฒนาชุมชนกับเพื่อน ๆ
        โดยช่วยเก็บขยะ ปลูกต้นไม้ และสอนหนังสือเด็กเล็กในหมู่บ้าน
        แม้งานจะเหนื่อย แต่ต้นกล้ารู้สึกภูมิใจที่ได้ช่วยเหลือผู้อื่น
        `,
        question: "ข้อใดคือใจความสำคัญของเรื่องนี้",
        choices: [
          "ต้นกล้าชอบปลูกต้นไม้",
          "ต้นกล้าใช้เวลาว่างทำกิจกรรมเพื่อช่วยเหลือสังคม",
          "เด็กเล็กในหมู่บ้านต้องการคนสอนหนังสือ",
          "กิจกรรมอาสาทำให้ต้นกล้าเหนื่อย"
        ],
        answer: 1
      },

      {
        story: `
        ปัจจุบันหลายคนใช้โทรศัพท์มือถือเป็นเวลานาน
        ส่งผลให้พักผ่อนไม่เพียงพอและเกิดปัญหาสายตา
        ดังนั้นเราควรแบ่งเวลาในการใช้อุปกรณ์อิเล็กทรอนิกส์อย่างเหมาะสม
        และพักสายตาเป็นระยะเพื่อสุขภาพที่ดี
        `,
        question: "ใจความสำคัญของข้อความนี้คืออะไร",
        choices: [
          "โทรศัพท์มือถือมีราคาแพง",
          "หลายคนชอบเล่นเกม",
          "การใช้มือถือมากเกินไปส่งผลเสียต่อสุขภาพ",
          "ควรซื้อแว่นสายตา"
        ],
        answer: 2
      },

      {
        story: `
        การออกกำลังกายเป็นประจำช่วยให้ร่างกายแข็งแรง
        อีกทั้งยังช่วยลดความเครียดและทำให้อารมณ์แจ่มใส
        ผู้ที่ออกกำลังกายสม่ำเสมอมักมีสุขภาพดีกว่าผู้ที่ไม่ออกกำลังกาย
        `,
        question: "ข้อใดสรุปใจความสำคัญได้ดีที่สุด",
        choices: [
          "การออกกำลังกายมีประโยชน์ต่อสุขภาพกายและใจ",
          "คนส่วนใหญ่ออกกำลังกายตอนเย็น",
          "การวิ่งเป็นการออกกำลังกายที่ดีที่สุด",
          "คนที่ไม่ออกกำลังกายจะป่วยเสมอ"
        ],
        answer: 0
      }

    ];

    let currentQuestion = 0;
    let score = 0;

    const gameBox = document.getElementById("gameBox");
    const scoreText = document.getElementById("score");

    function loadQuestion(){

      const q = questions[currentQuestion];

      gameBox.innerHTML = `
        <div class="story">
          ${q.story}
        </div>

        <div class="question">
          ${q.question}
        </div>

        <div class="choices">
          ${q.choices.map((choice,index)=>
            `<button class="btn" onclick="checkAnswer(${index})">
              ${choice}
            </button>`
          ).join("")}
        </div>

        <div class="result" id="result"></div>

        <button class="next-btn" id="nextBtn" onclick="nextQuestion()">
          ข้อต่อไป →
        </button>
      `;
    }

    function checkAnswer(selected){

      const q = questions[currentQuestion];
      const buttons = document.querySelectorAll(".btn");
      const result = document.getElementById("result");
      const nextBtn = document.getElementById("nextBtn");

      buttons.forEach(btn => btn.disabled = true);

      if(selected === q.answer){

        buttons[selected].classList.add("correct");

        result.style.display = "block";
        result.style.background = "#c8e6c9";
        result.innerHTML = "✅ ถูกต้อง! เก่งมาก";

        score += 10;
        scoreText.innerText = score;

      }else{

        buttons[selected].classList.add("wrong");
        buttons[q.answer].classList.add("correct");

        result.style.display = "block";
        result.style.background = "#ffcdd2";
        result.innerHTML = "❌ ยังไม่ถูก ลองอ่านใจความสำคัญอีกครั้ง";
      }

      nextBtn.style.display = "inline-block";
    }

    function nextQuestion(){

      currentQuestion++;

      if(currentQuestion < questions.length){

        loadQuestion();

      }else{

        showFinalScore();
      }
    }

    function showFinalScore(){

      gameBox.innerHTML = `
        <div class="finish">
          <h2>🎉 จบเกมแล้ว</h2>
          <p>คะแนนของคุณคือ ${score} / 30</p>

          <button class="restart" onclick="restartGame()">
            เล่นอีกครั้ง
          </button>
        </div>
      `;
    }

    function restartGame(){

      currentQuestion = 0;
      score = 0;

      scoreText.innerText = score;

      loadQuestion();
    }

    loadQuestion();

  </script>

</body>
</html>
