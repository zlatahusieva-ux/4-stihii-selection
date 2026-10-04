# <!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>4 Стихии — Mini Selection</title>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@500;600;700&family=Inter:wght@400;500;600&display=swap');

*{box-sizing:border-box}

body{
 margin:0;
 background:#171718;
 color:#f4f1ef;
 font-family:Inter,sans-serif;
}

.container{
 max-width:720px;
 margin:auto;
 padding:25px 20px 50px;
}

.top{
 display:flex;
 justify-content:space-between;
 color:#999;
 font-size:10px;
 letter-spacing:.2em;
 text-transform:uppercase;
}

.progress{
 height:2px;
 background:#333;
 margin:25px 0 45px;
}

.progress-bar{
 height:100%;
 background:#d62a72;
 width:0%;
 transition:.3s;
}

h1,h2{
 font-family:"Cormorant Garamond",serif;
 font-weight:600;
 line-height:.95;
}

h1{font-size:70px}
h2{font-size:55px}

p{
 color:#c9c5c5;
 line-height:1.7;
}

.eyebrow{
 color:#d85d91;
 letter-spacing:.2em;
 font-size:10px;
 text-transform:uppercase;
 margin-bottom:20px;
}

button{
 font:inherit;
}

.btn{
 width:100%;
 padding:17px;
 margin-top:20px;
 border:1px solid #555;
 background:transparent;
 color:white;
 cursor:pointer;
 text-transform:uppercase;
 letter-spacing:.12em;
}

.primary{
 background:#d62a72;
 border-color:#d62a72;
}

.answers{
 display:grid;
 gap:10px;
 margin-top:25px;
}

.answer{
 text-align:left;
 padding:17px;
 background:#202022;
 color:#eee;
 border:1px solid #393939;
 cursor:pointer;
}

.answer:hover{
 border-color:#d62a72;
}

.card{
 background:#202022;
 border:1px solid #393939;
 padding:25px;
 margin-top:25px;
}

.tag{
 display:inline-block;
 border:1px solid #555;
 padding:7px 10px;
 margin:4px;
 font-size:10px;
 letter-spacing:.08em;
}

.field{
 margin:15px 0;
}

label{
 display:block;
 font-size:10px;
 color:#aaa;
 text-transform:uppercase;
 letter-spacing:.12em;
 margin-bottom:7px;
}

input,textarea{
 width:100%;
 background:#202022;
 border:1px solid #444;
 color:white;
 padding:14px;
 font:inherit;
}

textarea{
 min-height:120px;
}

.error{
 color:#e66b99;
 display:none;
 font-size:12px;
}

.hidden{
 display:none;
}

.element{
 font-size:65px;
 font-family:"Cormorant Garamond",serif;
}

footer{
 text-align:center;
 color:#666;
 font-size:9px;
 letter-spacing:.2em;
 margin-top:40px;
}
</style>
</head>

<body>

<div class="container">

<div class="top">
<span>@sashhhh.nyx</span>
<span id="step">Вход</span>
</div>

<div class="progress">
<div class="progress-bar" id="progress"></div>
</div>

<div id="app"></div>

<footer>4 СТИХИИ · MINI SELECTION</footer>

</div>

<script>

const questions=[

{
q:"Когда ты чувствуешь себя наиболее живой?",
a:[
"Когда меня действительно кто-то или что-то зажигает.",
"Когда я создаю, двигаюсь и чувствую азарт.",
"Когда я могу расслабиться и наслаждаться моментом.",
"Честно? Я давно не чувствовала себя по-настоящему живой."
],
m:["fire","fire","water","earth"]
},

{
q:"Когда внутри становится слишком много эмоций, ты обычно…",
a:[
"Переживаю всё внутри и никому не показываю.",
"Начинаю много думать и искать объяснение.",
"Переключаюсь на дела, чтобы ничего не чувствовать.",
"Позволяю себе прожить эмоцию."
],
m:["water","air","earth","water"]
},

{
q:"Что сейчас больше всего мешает тебе двигаться вперёд?",
a:[
"Страх, что у меня не получится.",
"Я не понимаю, чего вообще хочу.",
"Я знаю, чего хочу, но боюсь проявляться.",
"Я уже двигаюсь и хочу выйти на следующий уровень."
],
m:["air","water","air","fire"]
},

{
q:"Как сейчас выглядят твои отношения с собственной жизнью?",
a:[
"Хаос: много хочу, но сложно организовать себя.",
"Я держусь на силе воли, но быстро выгораю.",
"У меня есть фундамент, но хочется его укрепить.",
"Я чувствую опору и постепенно строю жизнь под себя."
],
m:["earth","fire","earth","earth"]
},

{
q:"Что из этого откликается тебе сильнее всего?",
a:[
"Я слишком часто подстраиваюсь под других.",
"Я знаю, что могу больше, но пока не позволяю себе.",
"Я устала быть сильной и хочу научиться чувствовать.",
"Я хочу наконец построить жизнь, которая действительно моя."
],
m:["water","air","water","earth"]
},

{
q:"Представь пространство, где девушки открыто говорят о желаниях, деньгах, отношениях, сексуальности, страхах и амбициях. Как тебе?",
a:[
"Мне очень не хватает такого пространства.",
"Мне интересно, но немного страшно.",
"Я хочу попробовать.",
"Мне такое вообще не подходит."
],
m:["fire","water","fire","reject"]
},

{
q:"Что ты готова принести с собой в это пространство?",
a:[
"Честность.",
"Любопытство.",
"Готовность смотреть на себя без маски.",
"Пока не знаю, хочу просто посмотреть."
],
m:["fire","air","water","earth"]
}

];

const results={

fire:{
icon:"🔥",
name:"ОГОНЬ",
title:"Твой огонь просит внимания.",
shadow:"подавленное желание",
text:"Тебе может быть важно вернуть контакт со своими желаниями, удовольствием и живостью. Не выбирать только «как правильно», а снова спрашивать себя, чего действительно хочется.",
focus:"ЖЕЛАНИЕ · СЕКСУАЛЬНОСТЬ · УДОВОЛЬСТВИЕ · ЖИЗНЕННАЯ ЭНЕРГИЯ",
question:"Если бы мне не нужно было никому ничего доказывать — чего бы я захотела?"
},

water:{
icon:"🌊",
name:"ВОДА",
title:"Твоей воде нужно пространство.",
shadow:"эмоциональное избегание",
text:"Ты можешь чувствовать гораздо больше, чем позволяешь себе показать. Сейчас важно учиться замечать эмоции и понимать, что действительно происходит внутри.",
focus:"ЭМОЦИИ · ГРАНИЦЫ · ЧЕСТНОСТЬ С СОБОЙ · ЛЁГКОСТЬ",
question:"Что я сейчас чувствую — если не пытаться это объяснить?"
},

air:{
icon:"🌬️",
name:"ВОЗДУХ",
title:"Твоему воздуху нужен простор.",
shadow:"жизнь в голове вместо действия",
text:"В тебе есть идеи, амбиции и желание двигаться дальше. Но между «я хочу» и «я делаю» иногда появляется слишком много мыслей и страха оценки.",
focus:"ДЕНЬГИ · КАРЬЕРА · ГОЛОС · ПРОЯВЛЕННОСТЬ",
question:"Что бы я сделала, если бы не боялась, что меня оценят?"
},

earth:{
icon:"🌱",
name:"ЗЕМЛЯ",
title:"Твоей земле нужна опора.",
shadow:"отсутствие фундамента",
text:"Твои планы нуждаются в почве. Земля — это способность выбирать себя маленькими действиями каждый день.",
focus:"СТАБИЛЬНОСТЬ · ПРИВЫЧКИ · ТЕЛО · ГРАНИЦЫ · ФУНДАМЕНТ",
question:"Что я могу сделать сегодня, чтобы моя будущая версия поблагодарила меня?"
}

};

let current=0;

let scores={
fire:0,
water:0,
air:0,
earth:0
};

let answers=[];
let rejected=false;
let result="";

const app=document.getElementById("app");
const progress=document.getElementById("progress");
const step=document.getElementById("step");

function start(){

 current=0;
 answers=[];
 rejected=false;

 scores={
 fire:0,
 water:0,
 air:0,
 earth:0
 };

 showQuestion();
}

function showStart(){

 app.innerHTML=`

 <section>

 <div class="eyebrow">Mini selection · 4 стихии</div>

 <h1>
 А ЧТО,<br>
 ЕСЛИ С ТОБОЙ<br>
 ВСЁ НОРМАЛЬНО?
 </h1>

 <p>
 Это не тест на «хорошую» или «плохую» женщину.
 Здесь нет правильных ответов.
 </p>

 <p>
 Отвечай интуитивно и честно.
 </p>

 <button class="btn primary" onclick="start()">
 НАЧАТЬ ОТБОР
 </button>

 </section>
 `;

 step.innerText="Вход";
 progress.style.width="0%";
}

function showQuestion(){

 let q=questions[current];

 step.innerText=(current+1)+" / "+questions.length;

 progress.style.width=
 ((current/questions.length)*100)+"%";

 app.innerHTML=`

 <section>

 <div class="eyebrow">
 Вопрос ${current+1}
 </div>

 <h2>${q.q}</h2>

 <div class="answers">

 ${q.a.map((answer,i)=>`

 <button
 class="answer"
 onclick="choose(${i})">

 <b>${String.fromCharCode(65+i)}</b>
 ${answer}

 </button>

 `).join("")}

 </div>

 </section>
 `;
}

function choose(index){

 let q=questions[current];

 answers.push(String.fromCharCode(65+index));

 let mapped=q.m[index];

 if(mapped==="reject"){
 rejected=true;
 }else{
 scores[mapped]++;
 }

 current++;

 if(current<questions.length){

 showQuestion();

 }else{

 calculate();

 }

}

function calculate(){

 result=Object
 .entries(scores)
 .sort((a,b)=>b[1]-a[1])[0][0];

 showResult();
}

function showResult(){

 let r=results[result];

 step.innerText="Результат";
 progress.style.width="100%";

 app.innerHTML=`

 <section>

 <div class="eyebrow">
 ТВОЙ РЕЗУЛЬТАТ
 </div>

 <div class="element">
 ${r.icon} ${r.name}
 </div>

 <h2>${r.title}</h2>

 <div class="card">

 <p>${r.text}</p>

 <p>
 <small>ТВОЯ ТЕНЬ</small><br>
 <b>${r.shadow}</b>
 </p>

 <p>
 <small>ТОЧКА ВНИМАНИЯ</small>
 </p>

 <div>
 ${r.focus.split(" · ").map(x=>
 `<span class="tag">${x}</span>`
 ).join("")}
 </div>

 <p>
 «${r.question}»
 </p>

 </div>

 <div class="card">

 <p>
 <b>Но ты не одна стихия.</b><br>
 В тебе есть все четыре.
 Сейчас мы просто нашли ту,
 которая громче остальных просит
 твоего внимания.
 </p>

 </div>

 <button
 class="btn primary"
 onclick="showForm()">

 ПРОДОЛЖИТЬ ОТБОР

 </button>

 </section>
 `;
}

function showForm(){

 step.innerText="Анкета";

 app.innerHTML=`

 <section>

 <div class="eyebrow">
 ПОСЛЕДНИЙ ШАГ
 </div>

 <h2>
 Теперь — немного о тебе.
 </h2>

 <p>
 Ответы помогут нам понять,
 насколько тебе подходит наше пространство.
 </p>

 <div class="field">

 <label>Как к тебе обращаться *</label>

 <input
 id="name"
 placeholder="Имя">

 </div>

 <div class="field">

 <label>Твой Telegram *</label>

 <input
 id="telegram"
 placeholder="@username">

 </div>

 <div class="field">

 <label>Возраст *</label>

 <input
 id="age"
 type="number"
 min="13"
 max="99"
 placeholder="18">

 </div>

 <div class="field">

 <label>
 Что сейчас больше всего хочешь
 изменить в своей жизни?
 </label>

 <textarea
 id="goal"
 placeholder="Напиши несколько слов…">
 </textarea>

 </div>

 <div
 id="error"
 class="error">

 Заполни имя, Telegram и возраст.

 </div>

 <button
 class="btn primary"
 onclick="sendApplication()">

 ОТПРАВИТЬ ЗАЯВКУ

 </button>

 </section>

 `;

}

async function sendApplication(){

 const name=
 document.getElementById("name").value.trim();

 const telegram=
 document.getElementById("telegram").value.trim();

 const age=
 document.getElementById("age").value.trim();

 const goal=
 document.getElementById("goal").value.trim();

 if(!name || !telegram || !age){

 document.getElementById("error")
 .style.display="block";

 return;

 }

 const data={

 name:name,

 telegram:telegram,

 age:age,

 goal:goal,

 element:results[result].name,

 result:result,

 shadow:results[result].shadow,

 answers:answers,

 selection:
 rejected
 ? "manual_review"
 : "passed_test",

 time:new Date().toISOString()

 };

 try{

 const response=await fetch(
 "/api/application",
 {
 method:"POST",
 headers:{
 "Content-Type":"application/json"
 },
 body:JSON.stringify(data)
 }
 );

 if(!response.ok)
 throw new Error();

 showSuccess();

 }catch(error){

 alert(
 "Не удалось отправить заявку. Попробуй ещё раз."
 );

 }

}

function showSuccess(){

 app.innerHTML=`

 <section>

 <div class="eyebrow">
 ЗАЯВКА ПРИНЯТА
 </div>

 <h2>
 Ты дошла до края карты.
 </h2>

 <p>
 Твой результат сохранён,
 а заявка отправлена.
 </p>

 <div class="card">

 <div class="element">
 ${results[result].icon}
 </div>

 <p>
 Твоя стихия:
 <b>${results[result].name}</b>
 </p>

 <p>
 Если пространство тебе подходит,
 следующий шаг — лист ожидания.
 </p>

 </div>

 </section>

 `;

}

showStart();

</script>

</body>
</html>
api
└── application.js
export default async function handler(req, res) {

  if (req.method !== "POST") {
    return res.status(405).json({
      error: "Method not allowed"
    });
  }

  try {

    const {
      name,
      telegram,
      age,
      goal,
      element,
      shadow,
      answers,
      selection,
      time
    } = req.body;

    const token = process.env.TELEGRAM_BOT_TOKEN;
    const chatId = process.env.ADMIN_CHAT_ID;

    if (!token || !chatId) {
      return res.status(500).json({
        error: "Telegram is not configured"
      });
    }

    const status =
      selection === "passed_test"
        ? "🟢 ПРОШЛА МИНИ-ОТБОР"
        : "🟡 НУЖНА РУЧНАЯ ПРОВЕРКА";

    const message = `
🔮 НОВАЯ ЗАЯВКА

👤 Имя: ${name}
📱 Telegram: ${telegram}
🎂 Возраст: ${age}

${element === "ОГОНЬ" ? "🔥" :
  element === "ВОДА" ? "🌊" :
  element === "ВОЗДУХ" ? "🌬️" : "🌱"} Стихия: ${element}

🪞 Тень:
${shadow}

💭 Что хочет изменить:
${goal || "Не указано"}

📝 Ответы теста:
${answers.join(" · ")}

${status}

🕐 ${time}
`;

    const telegramResponse = await fetch(
      `https://api.telegram.org/bot${token}/sendMessage`,
      {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify({
          chat_id: chatId,
          text: message
        })
      }
    );

    const telegramData =
      await telegramResponse.json();

    if (!telegramData.ok) {

      return res.status(500).json({
        error: "Telegram error"
      });

    }

    return res.status(200).json({
      success: true
    });

  } catch (error) {

    return res.status(500).json({
      error: "Server error"
    });

  }

}
4-stihii-selection/
│
├── index.html
│
└── api/
    └── application.jse
TELEGRAM_BOT_TOKEN8864788568:AAHu7PtVz9sCx9RDL1QvyB8VlsTtNmLv0QE