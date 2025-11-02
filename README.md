<!doctype html>
<html lang="de">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Habibi Bloxberg — Forum (Demo)</title>
<style>
/* ===========================
   Habibi Bloxberg — Single-file Forum
   Neon brown-gold theme, responsive.
   Stores data in localStorage (no server required).
   Paste into Solo AI Website Designer as an HTML block.
   =========================== */

/* Root variables */
:root{
  --bg:#080808;
  --panel:#0f0f0f;
  --muted:#cfc6b6;
  --accent:#b88f3a;       /* brown-gold */
  --accent-dark:#8f6e2b;
  --accent-glow: rgba(184,143,58,0.12);
  --neon-outer: rgba(184,143,58,0.14);
  --glass: rgba(255,255,255,0.02);
  --card: rgba(255,255,255,0.02);
  --radius:12px;
  --max-width:1100px;
  --gap:18px;
  --ui-font: system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
}

/* Basic reset */
*{box-sizing:border-box}
html,body{height:100%}
body{
  margin:0;
  font-family:var(--ui-font);
  background:
    radial-gradient(circle at 10% 10%, rgba(255,255,255,0.01), transparent 6%),
    linear-gradient(180deg, #070707 0%, #050505 100%);
  color:#efeae1;
  -webkit-font-smoothing:antialiased;
  -moz-osx-font-smoothing:grayscale;
  padding:20px;
}

/* Container */
.site{
  max-width:var(--max-width);
  margin:0 auto;
}

/* Header / Hero */
.header{
  display:flex;
  align-items:center;
  gap:16px;
  padding:20px;
  border-radius:14px;
  background: linear-gradient(180deg, rgba(255,255,255,0.012), rgba(0,0,0,0.06));
  border:1px solid rgba(255,255,255,0.03);
  margin-bottom:var(--gap);
}
.logo-wrap{
  width:92px;
  height:92px;
  display:flex;
  align-items:center;
  justify-content:center;
  border-radius:16px;
  background: linear-gradient(180deg, rgba(255,255,255,0.01), rgba(0,0,0,0.18));
  box-shadow: 0 8px 28px rgba(0,0,0,0.6);
  flex-shrink:0;
  position:relative;
}
.brand{
  display:flex;
  flex-direction:column;
  gap:6px;
}
.brand h1{
  margin:0;
  font-size:20px;
  letter-spacing:0.2px;
}
.brand p{
  margin:0;
  font-size:13px;
  color:var(--muted);
}

/* Neon text style */
.neon-text{
  color:var(--accent);
  text-shadow:
    0 0 6px rgba(184,143,58,0.6),
    0 0 18px rgba(184,143,58,0.22),
    0 8px 22px rgba(0,0,0,0.6);
  font-weight:800;
}

/* Layout columns */
.columns{
  display:flex;
  gap:var(--gap);
  align-items:flex-start;
}

/* Sidebar */
.sidebar{
  width:340px;
  min-width:260px;
}
.card{
  background:var(--card);
  border-radius:12px;
  padding:14px;
  border:1px solid rgba(255,255,255,0.02);
  margin-bottom:var(--gap);
}

/* Inputs */
.input, textarea {
  width:100%;
  padding:10px 12px;
  border-radius:10px;
  background:var(--glass);
  border:1px solid rgba(255,255,255,0.05);
  color:inherit;
  font-size:14px;
  outline:none;
}
.input:focus, textarea:focus{
  box-shadow: 0 0 0 8px var(--accent-glow);
  border-color:var(--accent);
}

/* Buttons */
.btn{
  display:inline-flex;
  align-items:center;
  justify-content:center;
  gap:8px;
  padding:10px 14px;
  border-radius:10px;
  background:linear-gradient(180deg,var(--accent),var(--accent-dark));
  color:#0a0a0a;
  font-weight:800;
  border:none;
  cursor:pointer;
}
.btn.ghost{
  background:transparent;
  border:1px solid rgba(255,255,255,0.04);
  color:var(--muted);
}

/* Thread list */
.thread-list{ list-style:none; margin:0; padding:0; max-height:640px; overflow:auto; }
.thread-item{
  display:flex;
  flex-direction:column;
  gap:6px;
  padding:12px;
  border-radius:10px;
  margin-bottom:10px;
  transition:transform .12s ease, box-shadow .12s ease;
  border:1px solid rgba(255,255,255,0.02);
}
.thread-item:hover{ transform:translateY(-3px); box-shadow: 0 12px 34px rgba(0,0,0,0.6); background: linear-gradient(180deg, rgba(184,143,58,0.02), rgba(255,255,255,0.01)); }
.thread-title{ font-weight:800; color: #fff; text-decoration:none }
.thread-meta{ font-size:13px; color:var(--muted) }

/* Main content */
.main{
  flex:1;
  min-height:520px;
  background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(0,0,0,0.05));
  border-radius:12px;
  padding:18px;
  border:1px solid rgba(255,255,255,0.02);
}

/* Thread view & posts */
.thread-header{
  display:flex;
  justify-content:space-between;
  align-items:center;
  gap:12px;
  margin-bottom:12px;
}
.posts{ margin-top:12px; }
.post{
  background: linear-gradient(180deg, rgba(255,255,255,0.01), rgba(0,0,0,0.06));
  border-radius:10px;
  padding:12px;
  border:1px solid rgba(255,255,255,0.02);
  margin-bottom:12px;
}
.post-meta{ font-size:13px; color:var(--muted); margin-bottom:8px }
.post-body{ white-space:pre-wrap; color:#f3efe6 }

/* Small helpers */
.row{ display:flex; gap:10px; align-items:center; }
.small{ font-size:13px; color:var(--muted) }

/* Search box */
.search-box{ display:flex; gap:8px; align-items:center; }

/* Reply area */
.reply-area{ margin-top:12px; display:flex; flex-direction:column; gap:8px }

/* Neon logo SVG styling */
.logo-svg {
  width:68px;
  height:68px;
  display:block;
  filter: drop-shadow(0 6px 22px rgba(0,0,0,0.6));
}

/* Footer */
.footer{ text-align:center; color:var(--muted); margin-top:18px; font-size:13px }

/* Responsive */
@media (max-width:980px){
  .columns{ flex-direction:column; }
  .sidebar{ width:100%; order:2; }
  .main{ order:1; }
  .header{ flex-direction:column; gap:12px; align-items:center; text-align:center; }
}

/* Accessibility focus */
a:focus, button:focus, input:focus, textarea:focus { outline: 3px solid rgba(184,143,58,0.15); outline-offset:2px; }

/* Scrollbar tiny styling */
.thread-list::-webkit-scrollbar { width:8px }
.thread-list::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.04); border-radius:8px }
</style>
</head>
<body>
<div class="site">

  <!-- Header / Hero -->
  <header class="header" role="banner">
    <div class="logo-wrap" aria-hidden="true">
      <!-- SVG neon-style HB logo: connected H and B, rounded tubes -->
      <svg class="logo-svg" viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
        <!-- Glow layers for neon effect -->
        <defs>
          <filter id="f1" x="-50%" y="-50%" width="200%" height="200%">
            <feGaussianBlur stdDeviation="6" result="b"/>
            <feMerge>
              <feMergeNode in="b"/>
              <feMergeNode in="SourceGraphic"/>
            </feMerge>
          </filter>
          <linearGradient id="g1" x1="0" x2="1">
            <stop offset="0" stop-color="#f7e6c7"/>
            <stop offset="1" stop-color="#b88f3a"/>
          </linearGradient>
        </defs>

        <!-- Outer warm glow -->
        <g opacity="0.75">
          <path d="M34 30 L34 170" stroke="#b88f3a" stroke-width="18" stroke-linecap="round" stroke-linejoin="round" filter="url(#f1)"/>
          <path d="M34 100 L110 100" stroke="#b88f3a" stroke-width="18" stroke-linecap="round" stroke-linejoin="round" filter="url(#f1)"/>
          <path d="M110 30 L110 170" stroke="#b88f3a" stroke-width="18" stroke-linecap="round" stroke-linejoin="round" filter="url(#f1)"/>
          <!-- B rounded shape connected to H's middle bar -->
          <path d="M110 30 L155 30 C178 30 178 66 155 66 L110 66" stroke="#b88f3a" stroke-width="18" stroke-linecap="round" stroke-linejoin="round" filter="url(#f1)"/>
          <path d="M110 104 L155 104 C178 104 178 140 155 140 L110 140" stroke="#b88f3a" stroke-width="18" stroke-linecap="round" stroke-linejoin="round" filter="url(#f1)"/>
        </g>

        <!-- Inner bright tube -->
        <g>
          <path d="M34 30 L34 170" stroke="url(#g1)" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
          <path d="M34 100 L110 100" stroke="url(#g1)" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
          <path d="M110 30 L110 170" stroke="url(#g1)" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
          <path d="M110 30 L155 30 C178 30 178 66 155 66 L110 66" stroke="url(#g1)" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
          <path d="M110 104 L155 104 C178 104 178 140 155 140 L110 140" stroke="url(#g1)" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
        </g>
      </svg>
    </div>

    <div class="brand">
      <h1><span class="neon-text">Habibi Bloxberg</span></h1>
      <p class="small">Honest Camera Reviews. No Sponsors. Just Real Talk.</p>
    </div>

    <div style="margin-left:auto; display:flex; flex-direction:column; gap:8px; align-items:flex-end;">
      <div class="small" style="color:var(--muted)">Community-driven camera reviews & used gear tips</div>
      <a class="btn" id="btn-new-thread" href="#" title="Create a new thread">Create Thread</a>
    </div>
  </header>

  <!-- Columns: sidebar & main -->
  <div class="columns" role="main">

    <!-- Sidebar -->
    <aside class="sidebar" aria-label="Sidebar">
      <!-- Create thread card -->
      <div class="card" id="create-card">
        <h3 style="margin-top:0">Start a new thread</h3>
        <input id="input-title" class="input" placeholder="Thread title" maxlength="200" />
        <input id="input-author" class="input" placeholder="Your name (optional)" maxlength="50" style="margin-top:8px" />
        <textarea id="input-content" class="input" placeholder="Write your first post..." rows="4" style="margin-top:8px"></textarea>
        <div style="display:flex; gap:8px; margin-top:8px;">
          <button class="btn" id="create-btn">Post thread</button>
          <button class="btn ghost" id="clear-btn">Clear</button>
        </div>
      </div>

      <!-- Search card -->
      <div class="card">
        <h4 style="margin:0 0 8px 0">Search threads</h4>
        <div class="search-box">
          <input id="search-input" class="input" placeholder="Search titles..." />
          <button class="btn ghost" id="search-clear">Reset</button>
        </div>
      </div>

      <!-- Threads list -->
      <div class="card" style="padding-bottom:8px;">
        <h4 style="margin:0 0 8px 0">Recent threads</h4>
        <ul class="thread-list" id="threads-list" aria-live="polite"></ul>
        <div class="small" style="margin-top:8px">Stored locally in your browser.</div>
      </div>
    </aside>

    <!-- Main thread area -->
    <section class="main" id="main">
      <div id="empty-view" style="text-align:center; padding:40px;">
        <h2 style="margin-top:0">Welcome to the forum</h2>
        <p class="small">Click a thread on the left or create a new one. This demo stores posts locally in your browser (localStorage).</p>
      </div>

      <div id="thread-view" style="display:none;">
        <div class="thread-header">
          <div>
            <h2 id="thread-title-display" style="margin:0"></h2>
            <div class="small" id="thread-by"></div>
          </div>
          <div>
            <button class="btn ghost" id="back-btn">Back to threads</button>
          </div>
        </div>

        <div id="posts" class="posts" role="region" aria-live="polite"></div>

        <div class="reply-area card" style="margin-top:12px">
          <h4 style="margin:0 0 6px 0">Write a reply</h4>
          <input id="reply-author" class="input" placeholder="Your name (optional)" />
          <textarea id="reply-content" class="input" placeholder="Your reply..." rows="4"></textarea>
          <div style="display:flex; gap:8px;">
            <button class="btn" id="reply-btn">Post Reply</button>
            <button class="btn ghost" id="reply-clear">Clear</button>
          </div>
        </div>
      </div>

    </section>
  </div>

  <div class="footer">Made with ❤️ — Habibi Bloxberg (demo). Data saved to browser only.</div>
</div>

<script>
/*
  Forum frontend logic (single-file).
  - Stores data in localStorage under key HABIBI_FORUM_V1
  - Provides create thread, list threads, open thread, reply.
  - Simple search and UI interactions.
*/

// Utilities
const STORAGE_KEY = 'HABIBI_FORUM_V1';

function nowISO(){ return new Date().toISOString(); }

function loadData(){
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    if(!raw) return { threads: [], posts: [] };
    return JSON.parse(raw);
  } catch(e){ console.error('load error', e); return { threads: [], posts: [] }; }
}

function saveData(data){
  localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
}

// Initialize demo data if empty
(function initDemo(){
  const d = loadData();
  if(!d.threads || d.threads.length === 0){
    d.threads = [{ id:1, title:"Welcome to Habibi Bloxberg Forum", author:"Admin", created_at: nowISO() }];
    d.posts = [{ id:1, thread_id:1, author:"Admin", content:"This is the first post. Say hi!", created_at: nowISO() }];
    saveData(d);
  }
})();

// State & elements
let state = {
  data: loadData(),
  currentThreadId: null,
  nextThreadId: 1,
  nextPostId: 1
};

// compute next IDs
(function computeNext(){
  const tmax = state.data.threads.reduce((m,t)=> Math.max(m,t.id),0);
  const pmax = state.data.posts.reduce((m,p)=> Math.max(m,p.id),0);
  state.nextThreadId = tmax + 1;
  state.nextPostId = pmax + 1;
})();

const els = {
  threadsList: document.getElementById('threads-list'),
  createBtn: document.getElementById('create-btn'),
  clearBtn: document.getElementById('clear-btn'),
  inputTitle: document.getElementById('input-title'),
  inputAuthor: document.getElementById('input-author'),
  inputContent: document.getElementById('input-content'),
  searchInput: document.getElementById('search-input'),
  searchClear: document.getElementById('search-clear'),
  main: document.getElementById('main'),
  threadView: document.getElementById('thread-view'),
  emptyView: document.getElementById('empty-view'),
  threadTitleDisplay: document.getElementById('thread-title-display'),
  threadBy: document.getElementById('thread-by'),
  posts: document.getElementById('posts'),
  replyAuthor: document.getElementById('reply-author'),
  replyContent: document.getElementById('reply-content'),
  replyBtn: document.getElementById('reply-btn'),
  replyClear: document.getElementById('reply-clear'),
  backBtn: document.getElementById('back-btn'),
  newThreadBtn: document.getElementById('btn-new-thread'),
  createCard: document.getElementById('create-card')
};

// Rendering functions
function renderThreads(filter=''){
  const tlist = state.data.threads.slice().sort((a,b)=>{
    // sort by last post time or thread creation
    const la = lastPostTime(a.id) || a.created_at;
    const lb = lastPostTime(b.id) || b.created_at;
    return new Date(lb) - new Date(la);
  });

  const q = (filter || '').toLowerCase().trim();
  els.threadsList.innerHTML = '';
  if(tlist.length === 0){
    els.threadsList.innerHTML = '<li class="small">No threads yet</li>';
    return;
  }
  for(const t of tlist){
    if(q && !t.title.toLowerCase().includes(q)) continue;
    const item = document.createElement('li');
    item.className = 'thread-item';
    const postCount = state.data.posts.filter(p => p.thread_id === t.id).length;
    const lastAt = lastPostTime(t.id) || t.created_at;
    item.innerHTML = `
      <a href="#" class="thread-link" data-id="${t.id}">
        <div>
          <div class="thread-title">${escapeHtml(t.title)}</div>
          <div class="thread-meta">${postCount} posts • by ${escapeHtml(t.author)} • ${new Date(lastAt).toLocaleString()}</div>
        </div>
        <div class="small">${postCount > 0 ? 'Open' : 'New'}</div>
      </a>
    `;
    const link = item.querySelector('a');
    link.addEventListener('click', (e) => { e.preventDefault(); openThread(t.id); });
    els.threadsList.appendChild(item);
  }
}

function lastPostTime(threadId){
  const posts = state.data.posts.filter(p => p.thread_id === threadId);
  if(posts.length === 0) return null;
  return posts.reduce((m,p)=> p.created_at > m ? p.created_at : m, posts[0].created_at);
}

function escapeHtml(s){
  if(!s) return '';
  return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/\\n/g,'<br>');
}

function openThread(id){
  const thread = state.data.threads.find(t => t.id === id);
  if(!thread) return;
  state.currentThreadId = id;
  els.threadTitleDisplay.textContent = thread.title;
  els.threadBy.textContent = `by ${thread.author} • created ${new Date(thread.created_at).toLocaleString()}`;
  // render posts
  renderPostsForThread(id);
  // show thread view
  els.emptyView.style.display = 'none';
  els.threadView.style.display = 'block';
  // scroll to top of main area
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

function renderPostsForThread(threadId){
  const posts = state.data.posts.filter(p => p.thread_id === threadId).sort((a,b)=> new Date(a.created_at) - new Date(b.created_at));
  els.posts.innerHTML = '';
  for(const p of posts){
    const d = document.createElement('div');
    d.className = 'post';
    d.innerHTML = `
      <div class="post-meta">${escapeHtml(p.author)} • ${new Date(p.created_at).toLocaleString()}</div>
      <div class="post-body">${escapeHtml(p.content)}</div>
    `;
    els.posts.appendChild(d);
  }
  // focus reply content
  els.replyContent.focus();
}

// Create thread
els.createBtn.addEventListener('click', () => {
  const title = (els.inputTitle.value || '').trim();
  const author = (els.inputAuthor.value || '').trim() || 'Anonymous';
  const content = (els.inputContent.value || '').trim();
  if(!title || !content) { alert('Bitte Titel und Inhalt eingeben.'); return; }

  const threadId = state.nextThreadId++;
  const postId = state.nextPostId++;
  const t = { id: threadId, title, author, created_at: nowISO() };
  const p = { id: postId, thread_id: threadId, author, content, created_at: nowISO() };

  state.data.threads.push(t);
  state.data.posts.push(p);
  saveData(state.data);
  renderThreads(els.searchInput.value);
  // clear inputs
  els.inputTitle.value = '';
  els.inputAuthor.value = '';
  els.inputContent.value = '';
  // open created thread
  openThread(threadId);
});

// Clear create form
els.clearBtn.addEventListener('click', () => {
  els.inputTitle.value = '';
  els.inputAuthor.value = '';
  els.inputContent.value = '';
});

// Reply
els.replyBtn.addEventListener('click', () => {
  if(!state.currentThreadId) return alert('Open a thread first');
  const author = (els.replyAuthor.value || '').trim() || 'Anonymous';
  const content = (els.replyContent.value || '').trim();
  if(!content) { alert('Bitte Nachricht eingeben.'); return; }

  const postId = state.nextPostId++;
  const p = { id: postId, thread_id: state.currentThreadId, author, content, created_at: nowISO() };
  state.data.posts.push(p);
  saveData(state.data);
  renderPostsForThread(state.currentThreadId);
  renderThreads(els.searchInput.value);
  els.replyAuthor.value = '';
  els.replyContent.value = '';
});

// Reply clear
els.replyClear.addEventListener('click', () => { els.replyAuthor.value = ''; els.replyContent.value = ''; });

// Back button
els.backBtn.addEventListener('click', () => {
  state.currentThreadId = null;
  els.threadView.style.display = 'none';
  els.emptyView.style.display = 'block';
});

// Quick "Create Thread" header button scrolls to create card
els.newThreadBtn.addEventListener('click', (e) => {
  e.preventDefault();
  // open sidebar create area visually by focusing the first input
  els.inputTitle.focus();
  // smooth scroll (if inside builder this may or may not do something)
  els.inputTitle.scrollIntoView({ behavior:'smooth', block:'center' });
});

// Search
els.searchInput.addEventListener('input', (e) => {
  const q = e.target.value || '';
  renderThreads(q);
});
els.searchClear.addEventListener('click', () => {
  els.searchInput.value = '';
  renderThreads('');
});

// initial render
renderThreads('');

// Accessibility: keyboard shortcuts (optional)
/*
  - N: focus new thread title
  - Esc: clear search
*/
document.addEventListener('keydown', (e) => {
  if(e.key === 'n' || e.key === 'N'){ els.inputTitle.focus(); }
  if(e.key === 'Escape'){ els.searchInput.value=''; renderThreads(''); }
});
</script>

</body>
</html>
