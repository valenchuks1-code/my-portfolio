# my-portfolio
from pathlib import Path

html = """<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Exchange Helpdesk — Classroom Demo</title>
<style>
*{box-sizing:border-box}
body{margin:0;background:#f3f5f8;color:#202938;font:15px Arial,sans-serif}
header{background:#202b3c;color:#fff;padding:18px 22px;display:flex;justify-content:space-between;align-items:center;gap:12px;flex-wrap:wrap}
.brand{font-weight:800;letter-spacing:.04em}
.tag{font-size:11px;background:#ffe6a3;color:#614700;padding:7px 10px;border-radius:5px;font-weight:700}
main{max-width:980px;margin:28px auto;padding:0 16px}
.notice{background:#fff5d9;border:1px solid #e8cf7b;padding:12px 14px;border-radius:8px;margin-bottom:18px;color:#624c0a;line-height:1.5}
.layout{display:grid;grid-template-columns:270px 1fr;gap:16px}
.panel{background:#fff;border:1px solid #e1e6ed;border-radius:10px;padding:18px;min-width:0}
h1{font-size:22px;margin:0 0 8px}
h2{font-size:16px;margin:0 0 14px}
.muted{color:#687386;font-size:13px;line-height:1.5}
label{display:block;font-size:13px;font-weight:700;margin:14px 0 6px}
input{width:100%;padding:12px;border:1px solid #cbd3df;border-radius:6px;font-size:15px}
button{border:0;border-radius:6px;padding:11px 14px;background:#e9c44b;color:#222;font-weight:700;cursor:pointer;margin-top:12px}
button.secondary{background:#eef1f5;color:#263246}
.full{width:100%}
.mail{border-top:1px solid #e8ecf1;padding:14px 0;cursor:pointer}
.mail strong{display:block;margin-bottom:5px}
.mail small{color:#7a8493}
.mail:hover{background:#f8fafc}
#message{margin-top:12px;padding:12px;border-radius:6px;background:#edf6ff;color:#17456b;display:none;line-height:1.5}
#reader{margin-top:16px;border-top:1px solid #e8ecf1;padding-top:16px;line-height:1.6}
#inbox{display:none}
footer{text-align:center;color:#7a8493;font-size:12px;padding:22px}
@media(max-width:700px){.layout{grid-template-columns:1fr}main{margin:16px auto}}
</style>
</head>
<body>
<header>
  <div class="brand">NORTHSTAR EXCHANGE · HELP DESK</div>
  <div class="tag">CLASSROOM DEMONSTRATION — NOT A REAL SERVICE</div>
</header>
<main>
  <div class="notice"><strong>Educational simulation.</strong> This fictional interface is not affiliated with Binance or any exchange. Use only the sample access details shown below. Nothing is sent to a server, and no password is saved.</div>
  <section class="panel" id="login">
    <h1>Helpdesk mailbox</h1>
    <p class="muted">Sign in with the classroom-only demo details to view sample support messages.</p>
    <label for="email">Demo email</label>
    <input id="email" type="email" autocomplete="off" placeholder="student@example.test">
    <label for="password">Demo password</label>
    <input id="password" type="password" autocomplete="off" placeholder="Enter the sample password">
    <button class="full" id="signIn">Open demo mailbox</button>
    <div id="message" role="status"></div>
    <p class="muted"><strong>Sample access:</strong><br>Email: student@example.test<br>Password: class-demo-2026</p>
  </section>

  <section id="inbox" class="layout">
    <aside class="panel">
      <h2>Mailbox folders</h2>
      <p>📥 Inbox <strong>(3)</strong></p>
      <p class="muted">Sent · Drafts · Archive</p>
      <button class="secondary full" id="logout">Sign out of demo</button>
      <p class="muted">Signed in to a local classroom simulation only.</p>
    </aside>
    <section class="panel">
      <h1>Inbox</h1>
      <p class="muted">Select a sample message to read it.</p>
      <div class="mail" tabindex="0" data-message="security">
        <strong>Security Education Team</strong>
        Demo account safety reminder
        <small>Today · 9:15 AM</small>
      </div>
      <div class="mail" tabindex="0" data-message="ticket">
        <strong>Customer Care (Sample)</strong>
        Your practice ticket has been received
        <small>Yesterday · 2:40 PM</small>
      </div>
      <div class="mail" tabindex="0" data-message="notice">
        <strong>Northstar Helpdesk</strong>
        How to identify suspicious messages
        <small>Nov 10 · 11:05 AM</small>
      </div>
      <div id="reader" class="muted">No message selected.</div>
    </section>
  </section>
</main>
<footer>Northstar Exchange is fictional. Classroom demo only · No network requests · No credential collection.</footer>
<script>
const login = document.getElementById('login');
const inbox = document.getElementById('inbox');
const message = document.getElementById('message');
document.getElementById('signIn').addEventListener('click', () => {
  const email = document.getElementById('email').value.trim();
  const password = document.getElementById('password').value;
  if (email === 'student@example.test' && password === 'class-demo-2026') {
    message.style.display = 'block';
    message.textContent = 'Demo access accepted. Opening the sample mailbox.';
    login.style.display = 'none';
    inbox.style.display = 'grid';
  } else {
    message.style.display = 'block';
    message.textContent = 'Demo sign-in not recognised. Use only the sample details printed on this page.';
  }
});
document.getElementById('logout').addEventListener('click', () => {
  inbox.style.display = 'none';
  login.style.display = 'block';
  document.getElementById('password').value = '';
  message.style.display = 'none';
});
const samples = {
  security: ['Demo account safety reminder', 'Hello,\\n\\nThis sample message demonstrates how a helpdesk can remind users to open the official app or type a verified website address themselves. Never share passwords or one-time codes in response to an unexpected message.\\n\\n— Security Education Team'],
  ticket: ['Your practice ticket has been received', 'Hello,\\n\\nYour classroom practice request has been received. Reference: DEMO-1042. This is a fictional ticket and no real support case has been created.\\n\\n— Customer Care (Sample)'],
  notice: ['How to identify suspicious messages', 'Check the sender carefully, be cautious with unexpected attachments, and avoid signing in through links in unsolicited messages. Contact an organisation through contact details you independently verify.\\n\\n— Northstar Helpdesk']
};
document.querySelectorAll('.mail').forEach(item => {
  const open = () => {
    const data = samples[item.dataset.message];
    document.getElementById('reader').innerHTML = '<strong>' + data[0] + '</strong><p></p>';
    document.getElementById('reader').querySelector('p').textContent = data[1];
  };
  item.addEventListener('click', open);
  item.addEventListener('keydown', e => { if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); open(); } });
});
</script>
</body>
</html>
"""

path = Path("/mnt/data/northstar_helpdesk_classroom_demo.html")
path.write_text(html, encoding="utf-8")
print(f"Created: {path}")
print(f"File size: {path.stat().st_size} bytes")

