<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NasserGPT</title>
<style>
  body {
    font-family: Arial, sans-serif;
    margin: 0;
    height: 100vh;
    display: flex;
    flex-direction: column;
    background: #f6f6f6;
  }
  header {
    background-color: #007bff;
    color: white;
    padding: 15px;
    text-align: center;
    font-size: 24px;
    font-weight: bold;
  }
  #messages {
    flex: 1;
    padding: 20px;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
  }
  .message {
    padding: 10px 15px;
    margin: 5px 0;
    border-radius: 10px;
    max-width: 80%;
    word-wrap: break-word;
  }
  .user {
    background: #007bff;
    color: white;
    align-self: flex-end;
  }
  .bot {
    background: #e5e5e5;
    color: black;
    align-self: flex-start;
  }
  #inputArea {
    display: flex;
    padding: 10px;
    background: white;
    border-top: 1px solid #ccc;
  }
  #input {
    flex: 1;
    padding: 10px;
    border-radius: 5px;
    border: 1px solid #ccc;
    font-size: 16px;
  }
  button {
    padding: 10px 20px;
    margin-left: 10px;
    border: none;
    border-radius: 5px;
    background: #007bff;
    color: white;
    font-size: 16px;
  }
  body::before {
    content: 'به ناسر چی پی تی خوش امدید.';
    position: fixed;
    top: 10px;
    right: 10px;
    font-size: 20px;
    color: #ccc;
  }
</style>
</head>
<body>

<header>NasserGPT</header>

<div id="messages">
  <div class="message bot">سلام! من NasserGPT هستم. هر سوالی داری میتونی از من بپرسی!</div>
</div>

<div id="inputArea">
  <input type="text" id="input" placeholder="پیام خود را بنویسید...">
  <button onclick="sendMessage()">ارسال</button>
</div>

<script>
const messages = document.getElementById('messages');
const input = document.getElementById('input');

function generateReply(text){
  const t = text.toLowerCase();

  // Beispiele für Antworten auf Deutsch
  if(t.includes('hallo') || t.includes('hi')) return 'سلام! خوش آمدی 👋';
  if(t.includes('wie geht')) return 'من خوبم، مرسی! تو چطوری؟';
  if(t.includes('wer bist')) return 'من NasserGPT هستم، یک چت هوش مصنوعی ساده برای گفتگو!';
  if(t.includes('hilfe') || t.includes('مشکل')) return 'می‌توانم به شما کمک کنم. سوالت را بپرس.';
  
  // Wenn Text auf Persisch ist
  if(t.match(/[\u0600-\u06FF]/)) {
    return 'من پاسخ شما را به فارسی می‌دهم: ' + text;
  }

  // Standardantwort
  return 'من نمی‌دانم، لطفاً سوال دیگری بپرسید.';
}

function sendMessage(){
  const text = input.value.trim();
  if(!text) return;

  // Benutzer-Nachricht
  const userMsg = document.createElement('div');
  userMsg.className = 'message user';
  userMsg.textContent = text;
  messages.appendChild(userMsg);
  input.value='';
  messages.scrollTop = messages.scrollHeight;

  // Bot tippt...
  const typing = document.createElement('div');
  typing.className='message bot';
  typing.textContent='NasserGPT در حال پاسخگویی...';
  messages.appendChild(typing);
  messages.scrollTop = messages.scrollHeight;

  setTimeout(()=>{
    typing.remove();
    const botMsg = document.createElement('div');
    botMsg.className='message bot';
    botMsg.textContent = generateReply(text);
    messages.appendChild(botMsg);
    messages.scrollTop = messages.scrollHeight;
  }, 800);
}

// Enter-Taste senden
input.addEventListener('keydown', function(e){
  if(e.key === 'Enter') sendMessage();
});
</script>

</body>
</html>
