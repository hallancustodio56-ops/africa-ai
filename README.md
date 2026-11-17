from pathlib import Path

html = r'''<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<meta name="theme-color" content="#0b0b0d" />
<title>AFRICA AI — Intelligence Without Limits</title>
<style>
:root{--bg:#0b0b0d;--panel:#141417;--panel2:#1b1b20;--gold:#d9b45b;--gold2:#f3d98b;--text:#f5f3ed;--muted:#aaa8a0;--line:#2c2b2b;--green:#6fbd8b}
*{box-sizing:border-box}
body{margin:0;background:radial-gradient(ellipse at 80% 0%,#282113 0%,transparent 35%),var(--bg);color:var(--text);font-family:Inter,ui-sans-serif,system-ui,-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif;min-height:100vh}
button,input,textarea{font:inherit}
button{cursor:pointer}
.app{display:grid;grid-template-columns:250px minmax(0,1fr);min-height:100vh;max-width:1600px;margin:auto}
.sidebar{border-right:1px solid var(--line);padding:26px 18px;display:flex;flex-direction:column;gap:28px;background:rgba(10,10,12,.72)}
.brand{display:flex;align-items:center;gap:11px;padding:0 8px}
.logo{width:42px;height:42px;border-radius:14px;background:linear-gradient(135deg,var(--gold2),#9d7427);color:#17130a;display:grid;place-items:center;font-weight:900;font-size:19px;box-shadow:0 5px 24px #d9b45b22}
.brand h1{font-size:17px;letter-spacing:1.5px;margin:0}.brand small{display:block;color:var(--gold);font-size:10px;letter-spacing:2px;margin-top:3px}
.new-chat{border:1px solid #5c4b27;background:#211c11;color:var(--gold2);border-radius:12px;padding:12px;text-align:left}
.nav-label{font-size:10px;letter-spacing:1.8px;color:#77756f;padding:0 10px;margin-bottom:-14px}
.nav{display:grid;gap:7px}
.nav button{background:transparent;border:1px solid transparent;color:#c9c7c0;text-align:left;padding:12px;border-radius:10px;display:flex;gap:12px;align-items:center}
.nav button:hover,.nav button.active{background:#1d1a13;border-color:#3e3420;color:var(--gold2)}
.nav .ico{width:20px;text-align:center}
.side-bottom{margin-top:auto;color:var(--muted);font-size:12px;line-height:1.6;padding:12px}
.status{display:inline-flex;align-items:center;gap:7px;color:#9bd5aa}.dot{width:7px;height:7px;background:#69c584;border-radius:50%}
main{padding:26px clamp(18px,4vw,58px) 26px;min-width:0;display:flex;flex-direction:column}
.topbar{display:flex;justify-content:space-between;align-items:center;gap:16px;margin-bottom:45px}
.eyebrow{color:var(--gold);font-size:11px;letter-spacing:2px;text-transform:uppercase}
.top-actions{display:flex;gap:10px;align-items:center}
.lang{background:var(--panel);border:1px solid var(--line);color:var(--text);border-radius:9px;padding:8px 10px}
.avatar{width:35px;height:35px;border-radius:50%;display:grid;place-items:center;background:#2b2517;color:var(--gold2);border:1px solid #66542c}
.hero{max-width:850px;width:100%;margin:0 auto}
.hero h2{font-size:clamp(32px,5vw,54px);line-height:1.07;letter-spacing:-1.8px;margin:12px 0 14px}
.hero h2 span{background:linear-gradient(90deg,var(--gold2),var(--gold));-webkit-background-clip:text;background-clip:text;color:transparent}
.subtitle{color:var(--muted);font-size:16px;line-height:1.65;max-width:620px;margin:0 0 29px}
.searchbox{background:#151518;border:1px solid #39352a;border-radius:18px;padding:14px;box-shadow:0 18px 50px #0005}
textarea{width:100%;min-height:70px;resize:vertical;background:transparent;border:0;outline:none;color:var(--text);padding:8px;font-size:15px}
.composer-bottom{display:flex;align-items:center;justify-content:space-between;gap:12px;padding:7px 4px 0}
.hint{font-size:11px;color:#85827a}
.send{border:0;background:linear-gradient(135deg,var(--gold2),var(--gold));color:#17130a;font-weight:800;border-radius:11px;padding:11px 17px;display:flex;gap:9px;align-items:center}
.send:hover{filter:brightness(1.08);transform:translateY(-1px)}
.section-head{display:flex;justify-content:space-between;align-items:end;margin:36px 0 14px}
.section-head h3{font-size:15px;margin:0}.section-head span{color:#85827a;font-size:12px}
.cards{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:12px}
.card{border:1px solid var(--line);background:linear-gradient(145deg,#19191d,#121214);border-radius:15px;padding:17px;text-align:left;color:var(--text);min-height:146px;transition:.2s}
.card:hover{border-color:#8c7135;transform:translateY(-3px);background:#1b1914}
.card .card-ico{font-size:22px;width:42px;height:42px;border-radius:12px;display:grid;place-items:center;background:#2b2415;margin-bottom:16px}
.card strong{display:block;font-size:13px;margin-bottom:7px}.card p{margin:0;color:var(--muted);font-size:11px;line-height:1.5}
.chat-area{display:none;max-width:850px;width:100%;margin:0 auto;flex:1;min-height:55vh;flex-direction:column}
.chat-title{display:flex;align-items:center;gap:12px;padding-bottom:18px;border-bottom:1px solid var(--line)}
.chat-title h2{font-size:18px;margin:0}.chat-title p{font-size:12px;color:var(--muted);margin:4px 0 0}
.messages{display:flex;flex-direction:column;gap:17px;padding:22px 0;flex:1}
.message{max-width:88%;padding:14px 16px;border-radius:15px;line-height:1.65;font-size:14px;white-space:pre-wrap}
.message.user{align-self:flex-end;background:#292317;border:1px solid #554522}
.message.bot{align-self:flex-start;background:#171719;border:1px solid #2e2d2b}
.message .who{font-size:10px;color:var(--gold);letter-spacing:1px;margin-bottom:6px}
.chat-compose{margin-top:auto}
.notice{color:#77756f;font-size:10px;line-height:1.5;text-align:center;margin:12px auto 0;max-width:620px}
.toast{position:fixed;bottom:20px;left:50%;transform:translateX(-50%);background:#272216;border:1px solid #725d2c;color:#f8e7b5;padding:12px 17px;border-radius:12px;display:none;z-index:10;max-width:90vw;font-size:13px}
footer{max-width:850px;width:100%;margin:28px auto 0;color:#77756f;font-size:11px;display:flex;justify-content:space-between;gap:12px;border-top:1px solid #222;padding-top:17px}
@media(max-width:950px){.cards{grid-template-columns:repeat(2,minmax(0,1fr))}.app{grid-template-columns:210px minmax(0,1fr)}}
@media(max-width:680px){.app{display:block}.sidebar{display:none}main{padding:19px 15px}.topbar{margin-bottom:35px}.hero h2{letter-spacing:-1px}.cards{gap:9px}.card{padding:13px;min-height:135px}.card .card-ico{margin-bottom:12px}.section-head{margin-top:28px}.topbar .eyebrow{font-size:9px}.chat-area{min-height:65vh}footer{font-size:10px}}
</style>
</head>
<body>
<div class="app">
  <aside class="sidebar">
    <div class="brand"><div class="logo">A</div><div><h1>AFRICA AI</h1><small>INTELLIGENCE WITHOUT LIMITS</small></div></div>
    <button class="new-chat" id="newChat">＋ &nbsp; New conversation</button>
    <div class="nav-label">WORKSPACE</div>
    <nav class="nav">
      <button class="active" data-view="home"><span class="ico">⌂</span> Home</button>
      <button data-prompt="Help me study a subject. Ask me which subject and level first."><span class="ico">▤</span> Learn with AI</button>
      <button data-prompt="Help me develop a practical business idea for my budget and location. Ask me a few questions first."><span class="ico">◇</span> Business builder</button>
      <button data-prompt="Help me turn a goal into a step-by-step action plan with realistic tasks."><span class="ico">↗</span> Plan & achieve</button>
    </nav>
    <div class="nav-label">YOUR SPACE</div>
    <nav class="nav"><button id="historyBtn"><span class="ico">◷</span> Recent activity</button><button id="clearBtn"><span class="ico">⌫</span> Clear conversation</button></nav>
    <div class="side-bottom"><div class="status"><span class="dot"></span> Prototype ready</div><p>Built for curious minds, bold ideas and a brighter future across Africa.</p></div>
  </aside>
  <main>
    <header class="topbar">
      <div class="eyebrow">A new way to think bigger</div>
      <div class="top-actions"><select class="lang" id="language" aria-label="Language"><option value="en">English</option><option value="pt">Português</option></select><div class="avatar">A</div></div>
    </header>
    <section class="hero" id="homeView">
      <div class="eyebrow">WELCOME TO AFRICA AI</div>
      <h2>Your ideas.<br><span>Your future.</span></h2>
      <p class="subtitle">One place to learn, build and move forward. Ask a question, explore an idea or turn your next big goal into a practical plan.</p>
      <div class="searchbox">
        <textarea id="prompt" placeholder="Ask anything, or tell us what you want to achieve..." aria-label="Message"></textarea>
        <div class="composer-bottom"><span class="hint">✦ Think boldly. Start anywhere.</span><button class="send" id="sendBtn">Ask Africa AI <span>↗</span></button></div>
      </div>
      <div class="section-head"><h3>What would you like to do?</h3><span>Choose a starting point</span></div>
      <div class="cards">
        <button class="card" data-prompt="Teach me a topic in simple steps and then quiz me. Ask what I want to learn."><span class="card-ico">🎓</span><strong>Learn something</strong><p>Understand topics, practise skills and prepare for exams.</p></button>
        <button class="card" data-prompt="Help me create a business plan. Ask about my idea, location and starting budget."><span class="card-ico">💼</span><strong>Build a business</strong><p>Shape an idea, plan costs and reach customers.</p></button>
        <button class="card" data-prompt="Help me turn my goal into a realistic step-by-step action plan. Ask what my goal is."><span class="card-ico">⚡</span><strong>Plan & achieve</strong><p>Break a big goal into manageable actions.</p></button>
        <button class="card" data-prompt="Help me write or improve something. Ask what I need to create."><span class="card-ico">✍️</span><strong>Create something</strong><p>Draft ideas, messages, captions and useful content.</p></button>
      </div>
    </section>
    <section class="chat-area" id="chatView">
      <div class="chat-title"><div class="logo">A</div><div><h2>AFRICA AI Assistant</h2><p>Your thinking partner</p></div></div>
      <div class="messages" id="messages"></div>
      <div class="chat-compose searchbox"><textarea id="chatPrompt" placeholder="Write your message..." aria-label="Write your message"></textarea><div class="composer-bottom"><span class="hint">Prototype mode</span><button class="send" id="chatSend">Send ↗</button></div></div>
      <p class="notice">This is an interactive demo. Replies are generated locally from simple starter logic; connect a secure AI backend to enable real AI responses.</p>
    </section>
    <footer><span>© 2026 AFRICA AI · Early prototype</span><span>Built for possibility 🌍</span></footer>
  </main>
</div>
<div class="toast" id="toast"></div>
<script>
const $ = id => document.getElementById(id);
const homeView=$('homeView'),chatView=$('chatView'),messages=$('messages');
let conversation=[];
function showToast(msg){const t=$('toast');t.textContent=msg;t.style.display='block';clearTimeout(showToast.timer);showToast.timer=setTimeout(()=>t.style.display='none',3200)}
function openChat(){homeView.style.display='none';chatView.style.display='flex';document.querySelectorAll('.nav button').forEach(b=>b.classList.remove('active'));window.scrollTo({top:0,behavior:'smooth'});}
function goHome(){chatView.style.display='none';homeView.style.display='block';document.querySelector('[data-view="home"]').classList.add('active');}
function botReply(text){
 const s=text.toLowerCase();
 if(/business|sell|company|entrepreneur|neg[oó]cio|empresa|vender/.test(s)) return "Let's turn your idea into a practical business plan.\\n\\n1. Describe the product or service.\\n2. Identify your first customers.\\n3. List startup costs and ongoing expenses.\\n4. Choose a fair price and calculate your margin.\\n5. Test your idea with a small group before investing more.\\n\\nTo tailor this to you: what do you want to sell, where will you operate, and what is your starting budget?";
 if(/study|learn|school|math|exam|estudar|aprender|matem/.test(s)) return "Let's make learning easier.\\n\\n1. Choose one topic.\\n2. Learn the idea through a simple explanation and example.\\n3. Try a few practice questions.\\n4. Review mistakes and practise again.\\n\\nWhich subject and level are you studying, and what topic should we start with?";
 if(/plan|goal|achieve|routine|plano|objetivo|rotina/.test(s)) return "Let's turn your goal into action.\\n\\n• Define the result you want.\\n• Break it into small tasks.\\n• Set a realistic deadline for each task.\\n• Review progress and adjust each week.\\n\\nWhat goal do you want to achieve, and how much time can you spend on it each day?";
 if(/write|caption|letter|speech|create|escrever|texto|criar/.test(s)) return "I can help you shape the first draft. To make it useful, tell me: what are you creating, who is it for, and what tone do you want (professional, friendly, persuasive or creative)?";
 return "Thanks for sharing that with AFRICA AI. This prototype can demonstrate the experience, but it isn't connected to a live AI model yet.\\n\\nA useful next step is to define the result you want, break it into smaller parts, and work through them one by one.\\n\\nTell me a little more about your goal and I'll help you organise the next steps.";
}
function addMessage(role,text){
 const el=document.createElement('div');el.className='message '+role;
 const who=document.createElement('div');who.className='who';who.textContent=role==='user'?'YOU':'AFRICA AI';
 const body=document.createElement('div');body.textContent=text;
 el.append(who,body);messages.appendChild(el);messages.scrollTop=messages.scrollHeight;conversation.push({role,text});
}
function send(text,source){
 text=(text||'').trim();if(!text)return;
 openChat();addMessage('user',text);
 const reply=botReply(text);setTimeout(()=>addMessage('bot',reply),220);
 if(source==='home')$('prompt').value='';else $('chatPrompt').value='';
}
$('sendBtn').addEventListener('click',()=>send($('prompt').value,'home'));
$('prompt').addEventListener('keydown',e=>{if(e.key==='Enter'&&!e.shiftKey){e.preventDefault();send($('prompt').value,'home')}});
$('chatSend').addEventListener('click',()=>send($('chatPrompt').value,'chat'));
$('chatPrompt').addEventListener('keydown',e=>{if(e.key==='Enter'&&!e.shiftKey){e.preventDefault();send($('chatPrompt').value,'chat')}});
document.querySelectorAll('[data-prompt]').forEach(b=>b.addEventListener('click',()=>{const p=b.dataset.prompt;send(p,'home')}));
document.querySelector('[data-view="home"]').addEventListener('click',goHome);
$('newChat').addEventListener('click',()=>{messages.innerHTML='';conversation=[];goHome();$('prompt').focus()});
$('clearBtn').addEventListener('click',()=>{messages.innerHTML='';conversation=[];showToast('Conversation cleared.')});
$('historyBtn').addEventListener('click',()=>showToast(conversation.length?`This session has ${conversation.length} messages.`:'No messages yet in this session.'));
$('language').addEventListener('change',e=>{showToast(e.target.value==='pt'?'A interface ainda está principalmente em inglês. A versão portuguesa pode ser adicionada a seguir.':'Language set to English.')});
</script>
</body>
</html>'''

path = Path("/mnt/data/africa_ai_prototype.html")
path.write_text(html, encoding="utf-8")
print(f"Created: {path} ({path.stat().st_size:,} bytes)")
