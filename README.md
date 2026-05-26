# dcg-ue7
Aide révision dcg ue7 



<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>DCG UE7 — Guide complet</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=IBM+Plex+Mono:wght@400;500&family=IBM+Plex+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#0e0e10;--card:#1c1c22;--border:#2a2a33;
  --accent:#c9a84c;--accent2:#7b61ff;--green:#4caf82;--red:#e05c5c;
  --text:#e8e6e0;--muted:#888;--tag-bg:#252530;
}
body{background:var(--bg);color:var(--text);font-family:'IBM Plex Sans',sans-serif;min-height:100vh}

/* NAV */
nav{position:sticky;top:0;z-index:200;background:rgba(14,14,16,0.97);backdrop-filter:blur(14px);border-bottom:1px solid var(--border);display:flex;gap:0;overflow-x:auto;scrollbar-width:none}
nav::-webkit-scrollbar{display:none}
.nav-btn{flex-shrink:0;padding:1rem 1.4rem;font-family:'IBM Plex Mono',monospace;font-size:0.72rem;letter-spacing:0.07em;color:var(--muted);cursor:pointer;border:none;background:none;transition:all 0.2s;border-bottom:2px solid transparent;white-space:nowrap}
.nav-btn:hover{color:var(--text)}
.nav-btn.active{color:var(--accent);border-bottom-color:var(--accent)}

/* HEADER */
header{padding:3rem 2rem 2rem;position:relative;overflow:hidden;border-bottom:1px solid var(--border)}
header::before{content:'';position:absolute;top:-80px;left:-80px;width:400px;height:400px;background:radial-gradient(circle,rgba(201,168,76,0.10) 0%,transparent 70%);pointer-events:none}
.badge{font-family:'IBM Plex Mono',monospace;font-size:0.68rem;letter-spacing:0.2em;color:var(--accent);text-transform:uppercase;margin-bottom:0.75rem}
h1{font-family:'Playfair Display',serif;font-size:clamp(1.8rem,4vw,2.8rem);line-height:1.1;margin-bottom:0.4rem}
h1 em{font-style:italic;color:var(--accent)}
.sub{color:var(--muted);font-size:0.88rem}
.pills{display:flex;gap:0.6rem;margin-top:1.2rem;flex-wrap:wrap}
.pill{background:var(--tag-bg);border:1px solid var(--border);border-radius:20px;font-size:0.72rem;padding:0.3rem 0.9rem;color:var(--muted);font-family:'IBM Plex Mono',monospace}
.pill span{color:var(--accent);font-weight:600}

/* SECTIONS */
.section{display:none;padding:0 0 4rem}
.section.active{display:block}

/* ─── SECTION 1 : ANNALES ─── */
.annales-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:1rem;padding:2rem}
.annale-card{background:var(--card);border:1px solid var(--border);border-radius:10px;overflow:hidden;cursor:pointer;transition:border-color 0.2s,transform 0.2s}
.annale-card:hover{border-color:rgba(201,168,76,0.4);transform:translateY(-2px)}
.annale-head{padding:1rem 1.25rem 0.75rem;display:flex;justify-content:space-between;align-items:center}
.annale-year{font-family:'Playfair Display',serif;font-size:1.6rem;font-weight:700;color:var(--accent)}
.annale-co{font-family:'IBM Plex Mono',monospace;font-size:0.68rem;color:var(--muted);text-transform:uppercase;letter-spacing:0.1em}
.annale-title{padding:0 1.25rem 0.75rem;font-size:0.9rem;font-weight:600;color:var(--text)}
.annale-body{padding:0 1.25rem 1.25rem}
.annale-themes{display:flex;flex-wrap:wrap;gap:0.35rem;margin-bottom:0.75rem}
.atheme{font-size:0.65rem;padding:0.2rem 0.55rem;border-radius:4px;font-family:'IBM Plex Mono',monospace}
.atheme.strat{background:rgba(201,168,76,0.12);color:var(--accent);border:1px solid rgba(201,168,76,0.25)}
.atheme.struct{background:rgba(123,97,255,0.12);color:#9985e8;border:1px solid rgba(123,97,255,0.25)}
.atheme.rse{background:rgba(76,175,130,0.12);color:var(--green);border:1px solid rgba(76,175,130,0.25)}
.atheme.rh{background:rgba(224,92,92,0.12);color:var(--red);border:1px solid rgba(224,92,92,0.25)}
.atheme.lead{background:rgba(100,180,255,0.12);color:#64b4ff;border:1px solid rgba(100,180,255,0.25)}
.annale-q{font-size:0.8rem;color:#aaa;line-height:1.5;font-style:italic}
.annale-q strong{color:var(--text);font-style:normal}

.freq-bar-wrap{padding:1.5rem 2rem 0;border-top:1px solid var(--border);margin-top:2rem}
.freq-title{font-family:'IBM Plex Mono',monospace;font-size:0.7rem;letter-spacing:0.12em;color:var(--muted);text-transform:uppercase;margin-bottom:1rem}
.freq-row{display:flex;align-items:center;gap:0.75rem;margin-bottom:0.6rem}
.freq-label{font-size:0.78rem;width:160px;flex-shrink:0;color:var(--text)}
.freq-bar-bg{flex:1;height:8px;background:var(--tag-bg);border-radius:4px;overflow:hidden}
.freq-bar{height:100%;border-radius:4px;background:linear-gradient(90deg,var(--accent),var(--accent2));transition:width 1s ease}
.freq-pct{font-family:'IBM Plex Mono',monospace;font-size:0.7rem;color:var(--accent);width:35px;text-align:right}

/* ─── SECTION 2 : RÉPONSES TYPES ─── */
.rt-filters{padding:1.25rem 2rem;display:flex;gap:0.5rem;flex-wrap:wrap;border-bottom:1px solid var(--border);position:sticky;top:49px;background:rgba(14,14,16,0.97);backdrop-filter:blur(12px);z-index:100}
.rt-btn{background:var(--tag-bg);border:1px solid var(--border);border-radius:6px;color:var(--muted);font-family:'IBM Plex Mono',monospace;font-size:0.7rem;letter-spacing:0.05em;padding:0.4rem 0.85rem;cursor:pointer;transition:all 0.2s;white-space:nowrap}
.rt-btn:hover{color:var(--text);border-color:var(--muted)}
.rt-btn.active{background:var(--accent);border-color:var(--accent);color:#0e0e10;font-weight:600}
.rt-grid{padding:2rem;display:flex;flex-direction:column;gap:1.25rem}
.rt-card{background:var(--card);border:1px solid var(--border);border-radius:12px;overflow:hidden;animation:fadeUp 0.3s both}
@keyframes fadeUp{from{opacity:0;transform:translateY(12px)}to{opacity:1;transform:translateY(0)}}
.rt-head{padding:1.25rem 1.5rem;display:flex;justify-content:space-between;align-items:flex-start;cursor:pointer;gap:1rem}
.rt-head:hover .rt-name{color:var(--accent)}
.rt-name{font-family:'Playfair Display',serif;font-size:1.1rem;font-weight:700;transition:color 0.2s}
.rt-meta{display:flex;align-items:center;gap:0.5rem;flex-shrink:0}
.rt-cat{font-family:'IBM Plex Mono',monospace;font-size:0.62rem;padding:0.22rem 0.6rem;border-radius:4px;text-transform:uppercase;letter-spacing:0.08em}
.rt-chevron{color:var(--muted);font-size:0.9rem;transition:transform 0.3s;flex-shrink:0}
.rt-body{display:none;padding:0 1.5rem 1.5rem;border-top:1px solid var(--border)}
.rt-body.open{display:block}
.rt-section{margin-top:1rem}
.rt-section-title{font-family:'IBM Plex Mono',monospace;font-size:0.65rem;letter-spacing:0.15em;color:var(--accent);text-transform:uppercase;margin-bottom:0.6rem}
.rt-text{font-size:0.875rem;line-height:1.7;color:#bbb}
.rt-text strong{color:var(--text)}
.rt-text em{color:var(--accent);font-style:italic}
.rt-box{background:rgba(201,168,76,0.06);border:1px solid rgba(201,168,76,0.15);border-radius:8px;padding:1rem 1.1rem;margin-top:0.75rem;font-size:0.85rem;line-height:1.75;color:#ccc;font-family:'IBM Plex Sans',sans-serif}
.rt-box strong{color:var(--accent)}
.rt-tip{background:rgba(123,97,255,0.07);border-left:3px solid var(--accent2);padding:0.7rem 1rem;border-radius:0 6px 6px 0;margin-top:0.75rem;font-size:0.8rem;color:#9985e8;line-height:1.55}
.rt-tip::before{content:'💡 ';font-style:normal}

/* ─── SECTION 3 : LEXIQUE ─── */
.lex-toolbar{padding:1.25rem 2rem;display:flex;gap:0.75rem;flex-wrap:wrap;align-items:center;border-bottom:1px solid var(--border);position:sticky;top:49px;background:rgba(14,14,16,0.97);backdrop-filter:blur(12px);z-index:100}
.search-wrap{position:relative;flex:1;min-width:180px;max-width:320px}
.search-wrap svg{position:absolute;left:10px;top:50%;transform:translateY(-50%);opacity:0.4}
input[type="search"]{width:100%;background:var(--card);border:1px solid var(--border);border-radius:8px;padding:0.5rem 0.75rem 0.5rem 2.2rem;color:var(--text);font-family:'IBM Plex Sans',sans-serif;font-size:0.83rem;outline:none;transition:border-color 0.2s}
input[type="search"]:focus{border-color:var(--accent)}
input[type="search"]::placeholder{color:var(--muted)}
.lex-filters{display:flex;gap:0.4rem;flex-wrap:wrap}
.lf-btn{background:var(--tag-bg);border:1px solid var(--border);border-radius:6px;color:var(--muted);font-family:'IBM Plex Mono',monospace;font-size:0.68rem;letter-spacing:0.05em;padding:0.35rem 0.75rem;cursor:pointer;transition:all 0.2s;white-space:nowrap}
.lf-btn:hover{color:var(--text)}
.lf-btn.active{background:var(--accent);border-color:var(--accent);color:#0e0e10;font-weight:600}
.lex-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(320px,1fr));gap:1rem;padding:1.5rem 2rem}
.lex-card{background:var(--card);border:1px solid var(--border);border-radius:10px;padding:1.25rem;display:flex;flex-direction:column;gap:0.6rem;transition:border-color 0.2s,transform 0.2s;position:relative;overflow:hidden}
.lex-card::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:linear-gradient(90deg,var(--accent),var(--accent2));opacity:0;transition:opacity 0.3s}
.lex-card:hover{border-color:rgba(201,168,76,0.35);transform:translateY(-2px)}
.lex-card:hover::before{opacity:1}
.lex-top{display:flex;justify-content:space-between;align-items:flex-start;gap:0.5rem}
.lex-concept{font-family:'Playfair Display',serif;font-size:1.05rem;font-weight:700;line-height:1.2}
.lex-cat{background:var(--tag-bg);border:1px solid var(--border);border-radius:4px;font-family:'IBM Plex Mono',monospace;font-size:0.58rem;letter-spacing:0.08em;color:var(--muted);padding:0.2rem 0.5rem;white-space:nowrap;flex-shrink:0;text-transform:uppercase}
.lex-author{font-family:'IBM Plex Mono',monospace;font-size:0.72rem;color:var(--accent);display:flex;align-items:center;gap:0.4rem}
.lex-author::before{content:'';display:inline-block;width:5px;height:5px;border-radius:50%;background:var(--accent);flex-shrink:0}
.lex-def{font-size:0.83rem;line-height:1.62;color:#bbb}
.lex-def strong{color:var(--text);font-weight:500}
.lex-tags{display:flex;gap:0.35rem;flex-wrap:wrap;margin-top:0.25rem;padding-top:0.6rem;border-top:1px solid var(--border)}
.ltag{background:rgba(123,97,255,0.1);border:1px solid rgba(123,97,255,0.2);border-radius:3px;font-size:0.6rem;color:#9985e8;padding:0.15rem 0.45rem;font-family:'IBM Plex Mono',monospace}
.count-line{font-family:'IBM Plex Mono',monospace;font-size:0.72rem;color:var(--muted);padding:0.75rem 2rem 0}
.lex-empty{grid-column:1/-1;text-align:center;padding:3rem;color:var(--muted);font-style:italic;font-family:'Playfair Display',serif}

/* ─── SECTION 4 : MÉTHODOLOGIE ─── */
.metho-wrap{max-width:800px;margin:0 auto;padding:2rem}
.metho-block{background:var(--card);border:1px solid var(--border);border-radius:12px;margin-bottom:1.5rem;overflow:hidden}
.metho-block-head{padding:1.25rem 1.5rem;border-bottom:1px solid var(--border);display:flex;align-items:center;gap:0.75rem}
.metho-num{font-family:'Playfair Display',serif;font-size:2rem;color:var(--accent);line-height:1;min-width:2rem}
.metho-block-title{font-family:'Playfair Display',serif;font-size:1.15rem;font-weight:700}
.metho-block-body{padding:1.25rem 1.5rem;display:flex;flex-direction:column;gap:0.75rem}
.metho-step{display:flex;gap:0.75rem;align-items:flex-start}
.metho-dot{width:8px;height:8px;border-radius:50%;background:var(--accent);flex-shrink:0;margin-top:0.35rem}
.metho-step-text{font-size:0.875rem;line-height:1.65;color:#bbb}
.metho-step-text strong{color:var(--text)}
.metho-step-text em{color:var(--accent);font-style:italic}
.metho-warn{background:rgba(224,92,92,0.07);border:1px solid rgba(224,92,92,0.2);border-radius:8px;padding:0.9rem 1.1rem;font-size:0.82rem;color:#e08080;line-height:1.55}
.metho-warn::before{content:'⚠️  '}
.metho-good{background:rgba(76,175,130,0.07);border:1px solid rgba(76,175,130,0.2);border-radius:8px;padding:0.9rem 1.1rem;font-size:0.82rem;color:#7dd4ac;line-height:1.55}
.metho-good::before{content:'✅  '}
.plan-box{background:rgba(201,168,76,0.05);border:1px solid rgba(201,168,76,0.15);border-radius:8px;padding:1rem 1.2rem;font-size:0.85rem;line-height:1.8;color:#ccc;font-family:'IBM Plex Mono',monospace}
.plan-box .ph{color:var(--accent);font-weight:600}

footer{text-align:center;padding:2rem;color:var(--muted);font-size:0.72rem;border-top:1px solid var(--border);font-family:'IBM Plex Mono',monospace}
</style>
</head>
<body>

<header>
  <div class="badge">DCG · UE7 · Management des organisations</div>
  <h1>Guide <em>complet</em> de révision</h1>
  <p class="sub">Annales analysées · Réponses types · Lexique · Méthodologie</p>
  <div class="pills">
    <div class="pill">Sessions <span>2021–2025</span> analysées</div>
    <div class="pill"><span>58</span> définitions</div>
    <div class="pill"><span>12</span> réponses types</div>
    <div class="pill">Moy. nationale <span>9,1/20</span> en 2025</div>
  </div>
</header>

<nav>
  <button class="nav-btn active" data-tab="annales">📊 Annales</button>
  <button class="nav-btn" data-tab="reponses">✍️ Réponses types</button>
  <button class="nav-btn" data-tab="lexique">📖 Lexique</button>
  <button class="nav-btn" data-tab="metho">🗂️ Méthodologie</button>
</nav>

<!-- ════════════════════════════════════════════
     ONGLET 1 : ANNALES
════════════════════════════════════════════ -->
<div class="section active" id="tab-annales">
  <div class="annales-grid" id="annales-grid"></div>
  <div class="freq-bar-wrap">
    <div class="freq-title">Thèmes les + fréquents sur 10 ans (2015–2025)</div>
    <div id="freq-bars"></div>
  </div>
</div>

<!-- ════════════════════════════════════════════
     ONGLET 2 : RÉPONSES TYPES
════════════════════════════════════════════ -->
<div class="section" id="tab-reponses">
  <div class="rt-filters">
    <button class="rt-btn active" data-rcat="all">Tous</button>
    <button class="rt-btn" data-rcat="outils">Outils d'analyse</button>
    <button class="rt-btn" data-rcat="strategie">Stratégie</button>
    <button class="rt-btn" data-rcat="structure">Structure</button>
    <button class="rt-btn" data-rcat="rse">RSE</button>
    <button class="rt-btn" data-rcat="rh">RH & Motivation</button>
    <button class="rt-btn" data-rcat="decision">Décision</button>
  </div>
  <div class="rt-grid" id="rt-grid"></div>
</div>

<!-- ════════════════════════════════════════════
     ONGLET 3 : LEXIQUE
════════════════════════════════════════════ -->
<div class="section" id="tab-lexique">
  <div class="lex-toolbar">
    <div class="search-wrap">
      <svg width="14" height="14" viewBox="0 0 15 15" fill="none"><circle cx="6" cy="6" r="4.5" stroke="white" stroke-width="1.2"/><line x1="9.5" y1="9.5" x2="13" y2="13" stroke="white" stroke-width="1.2" stroke-linecap="round"/></svg>
      <input type="search" id="lex-search" placeholder="Auteur, concept, mot-clé…">
    </div>
    <div class="lex-filters" id="lex-filters">
      <button class="lf-btn active" data-lcat="all">Tout</button>
      <button class="lf-btn" data-lcat="organisation">Organisation</button>
      <button class="lf-btn" data-lcat="strategie">Stratégie</button>
      <button class="lf-btn" data-lcat="structure">Structure</button>
      <button class="lf-btn" data-lcat="leadership">Leadership</button>
      <button class="lf-btn" data-lcat="decision">Décision</button>
      <button class="lf-btn" data-lcat="motivation">Motivation</button>
      <button class="lf-btn" data-lcat="culture">Culture & GRH</button>
      <button class="lf-btn" data-lcat="environnement">Environnement</button>
      <button class="lf-btn" data-lcat="rse">RSE</button>
    </div>
  </div>
  <div class="count-line" id="lex-count"></div>
  <div class="lex-grid" id="lex-grid"></div>
</div>

<!-- ════════════════════════════════════════════
     ONGLET 4 : MÉTHODOLOGIE
════════════════════════════════════════════ -->
<div class="section" id="tab-metho">
  <div class="metho-wrap">

    <div class="metho-block">
      <div class="metho-block-head">
        <div class="metho-num">1</div>
        <div class="metho-block-title">Structure de l'épreuve UE7</div>
      </div>
      <div class="metho-block-body">
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>Durée :</strong> 3h — aucun document ni calculatrice autorisés.</div></div>
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>Dossier 1 — Analyse managériale (≈ 9 pts) :</strong> 3 à 5 questions à partir d'un dossier documentaire (textes, tableaux, schémas). Il faut identifier les concepts du programme, les nommer et les appliquer à la situation de l'entreprise étudiée.</div></div>
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>Dossier 2 — Question problématisée (≈ 11 pts) :</strong> dissertation managériale courte, avec plan apparent en 2 ou 3 parties, introduction avec problématique, développement argumenté, conclusion. Les documents du dossier 1 <em>peuvent et doivent</em> être réutilisés.</div></div>
        <div class="metho-warn">Les deux dossiers ne sont PAS indépendants. Le dossier 2 s'appuie sur l'entreprise et les documents du dossier 1.</div>
        <div class="metho-good">Le dossier 2 représente légèrement plus de points : ne pas le bâcler !</div>
      </div>
    </div>

    <div class="metho-block">
      <div class="metho-block-head">
        <div class="metho-num">2</div>
        <div class="metho-block-title">Stratégie pour le Dossier 1 — Analyse managériale</div>
      </div>
      <div class="metho-block-body">
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>Lire toutes les questions AVANT de lire les documents.</strong> Identifier les mots-clés et les rattacher à une partie du programme.</div></div>
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>Nommer systématiquement les outils et auteurs.</strong> Ex. : "Selon la chaîne de valeur de Porter (1985), les activités principales de X sont…"</div></div>
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>Structurer chaque réponse :</strong> définition du concept → application au cas → jugement critique ou limite.</div></div>
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>Ne pas paraphraser les documents.</strong> Le jury sanctionne la recopie. Toujours reformuler et interpréter.</div></div>
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>Respecter le barème :</strong> une question à 2 pts = environ 10–15 lignes ; une question à 4 pts = une à deux pages.</div></div>
      </div>
    </div>

    <div class="metho-block">
      <div class="metho-block-head">
        <div class="metho-num">3</div>
        <div class="metho-block-title">Méthode pour le Dossier 2 — Question problématisée</div>
      </div>
      <div class="metho-block-body">
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>Introduction (10 lignes minimum) :</strong> accroche contextuelle → définition des termes clés de la question → problématique reformulée → annonce du plan.</div></div>
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>Plan en 2 parties (2–3 sous-parties chacune) :</strong> chaque sous-partie = 1 idée + 1 concept théorique nommé + 1 illustration tirée du cas ou de l'actualité.</div></div>
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>Transitions visibles :</strong> annoncer le I, conclure le I avant d'attaquer le II.</div></div>
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>Conclusion :</strong> bilan des parties → réponse à la problématique → ouverture sur une question connexe.</div></div>
        <div class="plan-box">
          <span class="ph">INTRO</span> — Accroche · Définitions · Problématique · Annonce du plan<br>
          <span class="ph">I.</span> [Première grande idée] <br>
          &nbsp;&nbsp;&nbsp;A. Argument 1 + auteur + illustration<br>
          &nbsp;&nbsp;&nbsp;B. Argument 2 + auteur + illustration<br>
          &nbsp;&nbsp;&nbsp;C. Argument 3 (si nécessaire)<br>
          <span class="ph">Transition</span> — Bilan du I, annonce du II<br>
          <span class="ph">II.</span> [Deuxième grande idée]<br>
          &nbsp;&nbsp;&nbsp;A. Argument 1 + auteur + illustration<br>
          &nbsp;&nbsp;&nbsp;B. Argument 2 + auteur + illustration<br>
          <span class="ph">CONCLUSION</span> — Bilan · Réponse · Ouverture
        </div>
        <div class="metho-warn">Ce n'est PAS une dissertation de lycée. On n'oppose pas « thèse » et « antithèse ». On répond à une question managériale avec des parties complémentaires.</div>
      </div>
    </div>

    <div class="metho-block">
      <div class="metho-block-head">
        <div class="metho-num">4</div>
        <div class="metho-block-title">Exemples de plans types pour la question problématisée</div>
      </div>
      <div class="metho-block-body">
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>Comment [entreprise] peut-elle attirer et retenir les compétences ? (2025)</strong><br>
        I. Les leviers de la motivation et de l'attractivité (théories Maslow, Herzberg, Vroom) / II. Les politiques RH et managériales au service de la fidélisation (GPEC, culture, leadership)</div></div>
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>Comment [entreprise] peut-elle créer les conditions favorables à l'innovation ? (2024)</strong><br>
        I. La structure et la culture comme facteurs d'innovation (Mintzberg, adhocratie, Schein) / II. La stratégie et les ressources au service de l'innovation (Porter, compétences dynamiques)</div></div>
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>Comment [entreprise] peut-elle concilier performance économique et RSE ?</strong><br>
        I. Les enjeux RSE et leurs fondements (Carroll, Freeman, triple bottom line) / II. Intégrer la RSE comme levier de compétitivité (Porter & Kramer, loi PACTE, ISO 26000)</div></div>
      </div>
    </div>

    <div class="metho-block">
      <div class="metho-block-head">
        <div class="metho-num">5</div>
        <div class="metho-block-title">Gestion du temps — 3 heures</div>
      </div>
      <div class="metho-block-body">
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>0:00 – 0:20</strong> — Lecture globale du sujet, annotation des documents, identification des concepts clés.</div></div>
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>0:20 – 1:30</strong> — Rédaction du Dossier 1 (≈ 70 min pour 9 pts).</div></div>
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>1:30 – 1:45</strong> — Brainstorming et plan détaillé pour le Dossier 2.</div></div>
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>1:45 – 2:50</strong> — Rédaction du Dossier 2 (≈ 65 min pour 11 pts).</div></div>
        <div class="metho-step"><div class="metho-dot"></div><div class="metho-step-text"><strong>2:50 – 3:00</strong> — Relecture, vérification des titres de parties, orthographe.</div></div>
        <div class="metho-good">Ne pas passer plus de 1h30 sur le Dossier 1 même si toutes les réponses ne sont pas parfaites.</div>
      </div>
    </div>

  </div>
</div>

<footer>DCG UE7 Management · Guide de révision · Moy. 2025 : 9,1/20 · Taux de réussite : 46,1%</footer>

<script>
/* ══════════════════════════════════════
   DONNÉES
══════════════════════════════════════ */

const annales = [
  {
    year:2025, co:"Atelier Tuffery",
    themes:[{l:"Stratégie",c:"strat"},{l:"RH & Compétences",c:"rh"},{l:"Leadership",c:"lead"},{l:"Chaîne de valeur",c:"strat"}],
    q2:"Comment l'entreprise Atelier Tuffery peut-elle <strong>attirer et retenir les compétences</strong> ?",
    q1notes:"Entrepreneur vs manageur · Stratégie de niche · Tensions liées à la production · Chaîne de valeur",
    moy:"9,1/20", reussite:"46,1%"
  },
  {
    year:2024, co:"Daan Tech",
    themes:[{l:"Innovation",c:"strat"},{l:"RSE",c:"rse"},{l:"Parties prenantes",c:"rse"},{l:"Structure",c:"struct"}],
    q2:"Comment Daan Tech peut-elle créer les conditions favorables à <strong>l'innovation</strong> ?",
    q1notes:"Contributions des parties prenantes · Évolutions stratégiques · Marketing opérationnel · Processus décisionnel",
    moy:"8,8/20", reussite:"42,7%"
  },
  {
    year:2023, co:"Non communiqué",
    themes:[{l:"RSE",c:"rse"},{l:"Stratégie",c:"strat"},{l:"Management d'équipe",c:"lead"},{l:"Structure",c:"struct"}],
    q2:"Question autour de la <strong>RSE et de la performance durable</strong> de l'organisation.",
    q1notes:"Diagnostic stratégique · Gouvernance · Parties prenantes · Structure organisationnelle",
    moy:"9,0/20", reussite:"44,6%"
  },
  {
    year:2022, co:"Organisation publique",
    themes:[{l:"Structure",c:"struct"},{l:"Motivation",c:"rh"},{l:"Stratégie",c:"strat"},{l:"RSE",c:"rse"}],
    q2:"Question autour de la <strong>conduite du changement et des résistances</strong>.",
    q1notes:"Configurations structurelles (Mintzberg) · Styles de leadership · GPEC · Diagnostic SWOT",
    moy:"9,2/20", reussite:"45,3%"
  },
  {
    year:2021, co:"Organisation mixte",
    themes:[{l:"Leadership",c:"lead"},{l:"Motivation",c:"rh"},{l:"Stratégie",c:"strat"},{l:"Décision",c:"struct"}],
    q2:"Question autour du <strong>management des équipes et de la performance</strong>.",
    q1notes:"Styles de management · Théories de la motivation · Chaîne de valeur · Processus de décision",
    moy:"9,5/20", reussite:"47,1%"
  }
];

const freqs = [
  {label:"Stratégie (diagnostic, Porter…)", pct:100},
  {label:"RSE & Parties prenantes", pct:85},
  {label:"Structure (Mintzberg…)", pct:80},
  {label:"Chaîne de valeur", pct:75},
  {label:"Motivation & RH", pct:70},
  {label:"Leadership & Management", pct:70},
  {label:"Décision (Simon…)", pct:55},
  {label:"Culture organisationnelle", pct:45},
];

const reponses = [
  {
    id:"pestel", name:"PESTEL", cat:"outils", catColor:"#c9a84c", catBg:"rgba(201,168,76,0.12)",
    quand:"Quand on vous demande d'analyser l'environnement macroéconomique d'une organisation.",
    schema:"P — Politique · E — Économique · S — Socioculturel · T — Technologique · E — Environnemental · L — Légal",
    reponse:`L'analyse PESTEL permet d'identifier les <strong>opportunités et menaces</strong> de l'environnement global de [l'entreprise X].

<strong>Politique :</strong> [ex : politiques de soutien à l'industrie locale, instabilité réglementaire…]
<strong>Économique :</strong> [ex : évolution du pouvoir d'achat, taux de chômage, inflation…]
<strong>Socioculturel :</strong> [ex : évolution des modes de consommation, nouvelles attentes des salariés…]
<strong>Technologique :</strong> [ex : digitalisation, automatisation, innovation de rupture…]
<strong>Environnemental :</strong> [ex : pression écologique, réglementation carbone, attentes RSE…]
<strong>Légal :</strong> [ex : nouvelles normes, droit du travail, CSRD…]

Ainsi, [l'entreprise X] évolue dans un environnement <em>[turbulent / stable / incertain]</em> qui l'oblige à [s'adapter / innover / revoir sa stratégie].`,
    tip:"Toujours conclure en qualifiant l'environnement (turbulent, stable…) et en liant à la stratégie. Ne pas faire une liste vide : chaque élément doit être illustré avec le cas."
  },
  {
    id:"swot", name:"Diagnostic SWOT / FFOM", cat:"outils", catColor:"#c9a84c", catBg:"rgba(201,168,76,0.12)",
    quand:"Quand on vous demande un diagnostic stratégique interne ET externe.",
    schema:"Forces / Faiblesses (interne) · Opportunités / Menaces (externe)",
    reponse:`Le diagnostic SWOT (Andrews, École de Harvard, 1965) croise l'analyse interne et externe de [l'entreprise X].

<strong>Forces :</strong> [ex : savoir-faire reconnu, marque forte, ressources humaines qualifiées…]
<strong>Faiblesses :</strong> [ex : dépendance à un seul marché, manque de ressources financières…]
<strong>Opportunités :</strong> [ex : croissance du marché, aides publiques, évolution des usages…]
<strong>Menaces :</strong> [ex : intensification de la concurrence, hausse des coûts, réglementation…]

Ce diagnostic met en évidence que [l'entreprise X] dispose d'<em>atouts distinctifs</em> [Forces] qu'elle doit mobiliser pour saisir les <em>opportunités</em> de son environnement, tout en palliant ses <em>faiblesses</em> face aux <em>menaces</em> identifiées. Cela oriente sa stratégie vers [conclusion stratégique].`,
    tip:"Toujours faire une phrase de synthèse finale qui connecte les 4 quadrants. Le SWOT sans conclusion stratégique ne rapporte pas tous les points."
  },
  {
    id:"porter5", name:"5 forces de Porter", cat:"strategie", catColor:"#9985e8", catBg:"rgba(123,97,255,0.12)",
    quand:"Quand on vous demande d'analyser l'intensité concurrentielle d'un secteur.",
    schema:"Concurrents directs · Entrants potentiels · Substituts · Fournisseurs · Clients",
    reponse:`Selon le modèle des 5 forces concurrentielles de <strong>Porter (1979)</strong>, l'intensité concurrentielle du secteur de [X] s'analyse ainsi :

<strong>Rivalité entre concurrents directs :</strong> [forte/faible] en raison de [ex : marché concentré, guerre des prix…]
<strong>Menace des nouveaux entrants :</strong> [forte/faible] — les barrières à l'entrée sont [ex : élevées grâce aux économies d'échelle / faibles car marché peu capitalistique…]
<strong>Menace des produits substituts :</strong> [ex : émergence de solutions alternatives comme…]
<strong>Pouvoir de négociation des fournisseurs :</strong> [fort/faible] — [ex : peu de fournisseurs alternatifs…]
<strong>Pouvoir de négociation des clients :</strong> [fort/faible] — [ex : clients dispersés / grands comptes concentrés…]

Au total, l'intensité concurrentielle du secteur est <em>[élevée / modérée / faible]</em>, ce qui [avantage / contraint] [l'entreprise X] et justifie sa stratégie de [différenciation / domination par les coûts / focalisation].`,
    tip:"Conclure par l'intensité globale et son impact sur la stratégie de l'entreprise étudiée. Ne pas oublier de relier à Porter (1980) si la question porte ensuite sur la stratégie générique."
  },
  {
    id:"chaineval", name:"Chaîne de valeur", cat:"strategie", catColor:"#9985e8", catBg:"rgba(123,97,255,0.12)",
    quand:"Quand on vous demande d'identifier les sources de création de valeur ou d'avantage concurrentiel.",
    schema:"Activités principales (logistique, production, comm., SAV) + Activités de soutien (infra, RH, R&D, achats)",
    reponse:`La chaîne de valeur de <strong>Porter (1985)</strong> décompose les activités de [l'entreprise X] en deux catégories :

<strong>Activités principales :</strong>
→ Logistique entrante : [ex : approvisionnement en matières premières locales…]
→ Production / opérations : [ex : fabrication artisanale, processus de qualité…]
→ Logistique sortante : [ex : circuit de distribution direct…]
→ Marketing & ventes : [ex : vente en ligne, boutiques propres…]
→ Services après-vente : [ex : garantie étendue, service client…]

<strong>Activités de soutien :</strong>
→ Infrastructure de l'entreprise : [gouvernance, management…]
→ Gestion des ressources humaines : [formation, fidélisation…]
→ Développement technologique / R&D : [innovation produit…]
→ Achats : [sélection des fournisseurs…]

La valeur créée par [X] repose principalement sur [activité clé], qui constitue la source de son <em>avantage concurrentiel</em> [de différenciation / par les coûts].`,
    tip:"Identifier l'activité clé qui crée le plus de valeur et la relier explicitement à l'avantage concurrentiel. C'est ce que le jury attend en priorité."
  },
  {
    id:"mintzberg", name:"Structure selon Mintzberg", cat:"structure", catColor:"#64b4ff", catBg:"rgba(100,180,255,0.12)",
    quand:"Quand on vous demande de caractériser la structure organisationnelle d'une entreprise.",
    schema:"5 composantes · 6 mécanismes de coordination · 5 configurations structurelles",
    reponse:`Selon <strong>Mintzberg (1982)</strong>, toute organisation se compose de 5 parties : le <strong>sommet stratégique</strong>, la <strong>ligne hiérarchique</strong>, le <strong>centre opérationnel</strong>, la <strong>technostructure</strong> et les <strong>fonctions de support</strong>.

Dans le cas de [l'entreprise X], la partie dominante est [ex : le centre opérationnel / le sommet stratégique…], ce qui oriente vers une configuration de type <em>[structure simple / bureaucratie mécaniste / bureaucratie professionnelle / structure divisionnelle / adhocratie]</em>.

Le mécanisme de coordination privilégié est la <strong>[supervision directe / standardisation des procédés / ajustement mutuel…]</strong>, ce qui se traduit par [ex : un contrôle direct du dirigeant sur les équipes / des procédures formalisées…].

Cette structure est <em>[adaptée / inadaptée]</em> aux objectifs de [X] car [justification liée au contexte de l'entreprise].`,
    tip:"Toujours conclure sur l'adéquation entre la structure choisie et l'environnement ou la stratégie (théorie de la contingence : Lawrence & Lorsch)."
  },
  {
    id:"rse-carroll", name:"RSE et pyramide de Carroll", cat:"rse", catColor:"#4caf82", catBg:"rgba(76,175,130,0.12)",
    quand:"Quand on vous demande de définir la RSE, d'analyser l'engagement RSE d'une entreprise.",
    schema:"Économique → Légale → Éthique → Philanthropique (Carroll, 1979)",
    reponse:`La <strong>Responsabilité Sociale des Entreprises (RSE)</strong> se définit, selon la Commission européenne (2001), comme l'intégration volontaire par les entreprises de préoccupations sociales et environnementales dans leurs activités.

Selon la pyramide de <strong>Carroll (1979)</strong>, [l'entreprise X] assume 4 niveaux de responsabilité :
→ <strong>Économique :</strong> être rentable et créer de la valeur [ex : chiffre d'affaires en croissance…]
→ <strong>Légale :</strong> respecter les lois et réglementations en vigueur [ex : normes environnementales, droit du travail…]
→ <strong>Éthique :</strong> agir de manière équitable au-delà des obligations légales [ex : politique d'achats responsables…]
→ <strong>Philanthropique :</strong> contribuer positivement à la société [ex : mécénat, actions territoriales…]

[L'entreprise X] se situe principalement au niveau <em>[éthique / philanthropique]</em> de la pyramide, ce qui témoigne d'un engagement RSE [avancé / en cours de construction].

Cette démarche s'inscrit dans la logique de <strong>Freeman (1984)</strong> qui invite à prendre en compte l'ensemble des parties prenantes, et de <strong>Porter & Kramer (2011)</strong> qui y voient une source d'avantage concurrentiel.`,
    tip:"Citer à minima Carroll ET Freeman. Si la question porte sur le reporting RSE, mentionner la CSRD (2022) et la loi PACTE (2019)."
  },
  {
    id:"motivation", name:"Théories de la motivation", cat:"rh", catColor:"#e05c5c", catBg:"rgba(224,92,92,0.12)",
    quand:"Quand on vous demande d'expliquer comment motiver les salariés ou analyser la politique RH.",
    schema:"Maslow · Herzberg · Vroom · McGregor · Adams",
    reponse:`La motivation au travail est un enjeu central du management des ressources humaines. Plusieurs théories permettent d'analyser la situation de [l'entreprise X] :

Selon <strong>Maslow (1954)</strong>, les besoins des salariés sont hiérarchisés. [L'entreprise X] répond aux besoins [de base / de sécurité / d'appartenance / d'estime / d'accomplissement] de ses collaborateurs via [exemples tirés du cas].

<strong>Herzberg (1959)</strong> distingue les facteurs d'hygiène (salaire, conditions de travail — leur absence démotive) des facteurs de motivation (responsabilité, reconnaissance — leur présence motive). Chez [X], [ex : la politique de rémunération satisfait les facteurs d'hygiène mais les facteurs de motivation semblent insuffisants…].

Selon <strong>Vroom (1964)</strong>, la motivation dépend de l'<em>expectation</em> (croire en sa capacité à réussir), de l'<em>instrumentalité</em> (croire que la performance est récompensée) et de la <em>valence</em> (valeur accordée à la récompense). [L'entreprise X] pourrait renforcer [lequel] en [mesure concrète].

Ainsi, pour améliorer la motivation, [X] devrait [proposition concrète fondée sur les théories].`,
    tip:"Mobiliser 2 à 3 théories minimum en les articulant entre elles. Ne pas plaquer la théorie sans la connecter au cas de l'entreprise."
  },
  {
    id:"leadership", name:"Styles de leadership et management", cat:"rh", catColor:"#e05c5c", catBg:"rgba(224,92,92,0.12)",
    quand:"Quand on vous demande de caractériser le style de management ou de leadership.",
    schema:"Blake & Mouton · Hersey & Blanchard · Burns & Bass · French & Raven",
    reponse:`Le style de management peut être analysé à travers plusieurs grilles de lecture.

Selon la <strong>grille managériale de Blake & Mouton (1964)</strong>, le manager de [X] se situe sur un axe combinant l'intérêt pour la production et l'intérêt pour les personnes. Son style semble être [ex : (9,1) centré tâche / (1,9) centré relations / (9,9) intégrateur].

Le modèle de <strong>Hersey & Blanchard (1969)</strong> invite à adapter le style à la maturité des collaborateurs. Face à des équipes [autonomes / débutantes], le style <em>[délégatif / directif / participatif]</em> apparaît le plus approprié.

Le leadership exercé peut également être qualifié de <strong>transformationnel</strong> (Burns, 1978 ; Bass, 1985) dans la mesure où [le dirigeant inspire une vision, mobilise autour de valeurs fortes…] <em>ou</em> de <strong>transactionnel</strong> si la relation repose sur un système de récompenses et sanctions.

Ce style de management [est cohérent / présente des limites] car [justification contextuelle].`,
    tip:"Si le sujet parle d'un fondateur-dirigeant charismatique, pensez au leadership transformationnel de Burns/Bass. Si on parle de management d'équipe opérationnelle, préférez Hersey & Blanchard."
  },
  {
    id:"decision", name:"Processus de décision (Simon)", cat:"decision", catColor:"#c9a84c", catBg:"rgba(201,168,76,0.12)",
    quand:"Quand on vous demande d'analyser un processus de décision ou une décision stratégique.",
    schema:"Modèle IMC · Rationalité limitée · Décision programmée vs non programmée",
    reponse:`Le processus de décision peut être analysé à travers le modèle de <strong>Simon (1960)</strong>.

Selon Simon, toute décision suit 3 phases :
→ <strong>Intelligence :</strong> identification et diagnostic du problème [ex : X constate une baisse de parts de marché…]
→ <strong>Modélisation (Design) :</strong> conception et évaluation des solutions possibles [ex : diversification, partenariat, internalisation…]
→ <strong>Choice :</strong> sélection de la solution retenue [ex : X choisit d'internaliser la production…]

Simon souligne également que la rationalité des décideurs est <strong>limitée</strong> : ils ne peuvent pas explorer toutes les alternatives faute de temps, d'information et de capacité cognitive. Ils s'arrêtent à la première solution <em>satisfaisante</em> (satisficing) plutôt qu'optimale.

La décision de [X] est une décision <strong>[programmée / non programmée]</strong> car [justification : routinière et reproductible / unique et complexe].`,
    tip:"Le modèle IMC est toujours pertinent pour décomposer n'importe quelle décision. Mentionner la rationalité limitée montre une vraie maîtrise du concept."
  },
  {
    id:"strat-generiques", name:"Stratégies génériques de Porter", cat:"strategie", catColor:"#9985e8", catBg:"rgba(123,97,255,0.12)",
    quand:"Quand on vous demande d'identifier la stratégie concurrentielle d'une entreprise.",
    schema:"Domination par les coûts · Différenciation · Focalisation (Porter, 1980)",
    reponse:`Selon <strong>Porter (1980)</strong>, trois stratégies génériques permettent d'obtenir un avantage concurrentiel durable :

→ La <strong>domination par les coûts</strong> : produire moins cher que les concurrents pour proposer des prix attractifs ou dégager des marges élevées.
→ La <strong>différenciation</strong> : proposer une offre perçue comme unique par les clients, qui acceptent de payer un premium.
→ La <strong>focalisation (concentration)</strong> : se spécialiser sur un segment de marché précis et y appliquer l'une des deux stratégies précédentes.

[L'entreprise X] a choisi une stratégie de <strong>[différenciation / focalisation]</strong>, ce qui se traduit par [ex : une production locale artisanale, des matériaux premium, une identité de marque forte…].

Cette stratégie lui permet de [avantage concret : fidéliser une clientèle, éviter la concurrence par les prix…]. Porter met en garde contre l'<em>enlisement</em> : tenter de combiner les deux stratégies sans clarté conduit à la perte d'avantage concurrentiel.`,
    tip:"Relier systématiquement la stratégie générique aux ressources VRIN de Barney si la question porte aussi sur les ressources et compétences."
  },
  {
    id:"parties-prenantes", name:"Parties prenantes et gouvernance", cat:"rse", catColor:"#4caf82", catBg:"rgba(76,175,130,0.12)",
    quand:"Quand on vous demande d'identifier les acteurs concernés par les décisions de l'entreprise.",
    schema:"Parties prenantes primaires / secondaires · Freeman (1984) · Théorie de l'agence",
    reponse:`Selon <strong>Freeman (1984)</strong>, une partie prenante (stakeholder) est tout individu ou groupe pouvant affecter ou être affecté par la réalisation des objectifs de l'organisation.

On distingue :
→ <strong>Parties prenantes primaires :</strong> actionnaires, salariés, clients, fournisseurs — en relation directe avec [X].
→ <strong>Parties prenantes secondaires :</strong> collectivités locales, ONG, médias, associations — indirectement concernés.

[L'entreprise X] doit arbitrer entre des attentes parfois contradictoires :
→ Les actionnaires attendent [rentabilité / dividendes]
→ Les salariés attendent [sécurité de l'emploi / conditions de travail]
→ Les clients attendent [qualité / prix / engagement RSE]
→ Les pouvoirs publics attendent [respect des normes / contribution au territoire]

La théorie de l'agence (<strong>Jensen & Meckling, 1976</strong>) rappelle que les dirigeants peuvent agir dans leur propre intérêt au détriment des actionnaires, d'où l'importance des mécanismes de gouvernance (conseil d'administration, audit, rémunération incitative).`,
    tip:"Toujours distinguer parties prenantes primaires et secondaires et montrer les tensions entre leurs intérêts. C'est ce qui différencie une bonne copie d'une copie moyenne."
  },
  {
    id:"gpec", name:"GPEC et politique RH", cat:"rh", catColor:"#e05c5c", catBg:"rgba(224,92,92,0.12)",
    quand:"Quand on vous demande comment l'entreprise gère ses ressources humaines ou anticipe ses besoins en compétences.",
    schema:"GPEC · Contrat psychologique (Rousseau) · Théorie de l'agence",
    reponse:`La <strong>Gestion Prévisionnelle des Emplois et des Compétences (GPEC)</strong>, instituée par la loi Borloo (2005), est une démarche d'anticipation visant à adapter les ressources humaines aux besoins futurs de l'organisation.

Elle repose sur 3 étapes :
→ <strong>Diagnostic :</strong> identification des compétences actuelles et des emplois existants chez [X].
→ <strong>Projection :</strong> anticipation des besoins futurs en fonction de la stratégie (ex : développement de nouveaux marchés, digitalisation…).
→ <strong>Plan d'action :</strong> formation, mobilité interne, recrutement, ou ruptures conventionnelles.

Chez [l'entreprise X], les enjeux RH identifiés sont [ex : fidéliser des artisans qualifiés / développer les compétences digitales…].

Au-delà de la GPEC, <strong>Rousseau (1989)</strong> souligne l'importance du <em>contrat psychologique</em> : les attentes implicites des salariés (autonomie, reconnaissance, évolution) doivent être respectées pour maintenir leur engagement. Sa violation peut entraîner démotivation et turnover.`,
    tip:"Associer GPEC + contrat psychologique de Rousseau montre une vision complète de la GRH. Si la question parle d'attraction des talents, ajouter les théories de la motivation (Herzberg, Maslow)."
  }
];

const lexique = [
  {concept:"Organisation",author:"Barnard (1938)",category:"organisation",definition:"Système de coopération consciente, délibérée et finalisée entre des individus. Une organisation naît lorsque des personnes mettent en commun leurs efforts pour atteindre un but qu'aucune ne pourrait réaliser seule.",tags:["fondamental","coopération"]},
  {concept:"OST — Organisation Scientifique du Travail",author:"Taylor (1911)",category:"organisation",definition:"Méthode fondée sur la <strong>division horizontale</strong> (parcellisation des tâches) et <strong>verticale</strong> (séparation conception/exécution) du travail, la standardisation des gestes et la rémunération au rendement.",tags:["taylorisme","productivité"]},
  {concept:"Administration industrielle (POCCC)",author:"Fayol (1916)",category:"organisation",definition:"Fayol identifie <strong>5 fonctions du manager</strong> : Prévoir, Organiser, Commander, Coordonner, Contrôler (POCCC). Il formule 14 principes généraux d'administration.",tags:["POCCC","principes","classique"]},
  {concept:"Bureaucratie",author:"Weber (1922)",category:"organisation",definition:"Organisation rationnelle-légale fondée sur des <strong>règles formelles</strong>, une hiérarchie stricte et la compétence technique. 3 types d'autorité : traditionnelle, charismatique, rationnelle-légale.",tags:["autorité","règles","hiérarchie"]},
  {concept:"Relations humaines",author:"Mayo (1927-1932)",category:"organisation",definition:"Suite aux expériences de Hawthorne, Mayo montre que la <strong>productivité dépend des relations sociales</strong>. L'appartenance au groupe et la reconnaissance sont des facteurs déterminants.",tags:["Hawthorne","groupe","social"]},
  {concept:"Entreprise comme système ouvert",author:"Katz & Kahn (1966)",category:"organisation",definition:"L'entreprise reçoit des <strong>inputs</strong>, les transforme et produit des <strong>outputs</strong>. Elle doit s'adapter en continu à son environnement pour survivre.",tags:["systémique","environnement"]},
  {concept:"Apprentissage organisationnel",author:"Argyris & Schön (1978)",category:"organisation",definition:"<strong>Simple boucle</strong> : correction sans remettre en cause les valeurs. <strong>Double boucle</strong> : remise en cause des valeurs et normes profondes de l'organisation.",tags:["apprentissage","boucle"]},
  {concept:"Théorie X et Théorie Y",author:"McGregor (1960)",category:"motivation",definition:"<strong>X</strong> : l'homme est paresseux, il faut le contrôler. <strong>Y</strong> : l'homme cherche la responsabilité. Le management doit s'appuyer sur Y pour libérer le potentiel.",tags:["représentation","style"]},
  {concept:"Pyramide des besoins",author:"Maslow (1954)",category:"motivation",definition:"Hiérarchie de 5 besoins : <strong>physiologiques → sécurité → appartenance → estime → accomplissement</strong>. Un besoin supérieur n'est activé que si les inférieurs sont satisfaits.",tags:["besoins","hiérarchie"]},
  {concept:"Théorie bi-factorielle",author:"Herzberg (1959)",category:"motivation",definition:"<strong>Facteurs d'hygiène</strong> (salaire, conditions — leur absence démotive) vs <strong>facteurs de motivation</strong> (responsabilité, reconnaissance — leur présence motive).",tags:["hygiène","satisfaction"]},
  {concept:"Théorie des attentes (VIE)",author:"Vroom (1964)",category:"motivation",definition:"Motivation = <strong>Valence × Instrumentalité × Expectation</strong>. L'individu agit si il croit réussir, si la performance est récompensée, et si il valorise la récompense.",tags:["VIE","expectation"]},
  {concept:"Théorie de l'équité",author:"Adams (1965)",category:"motivation",definition:"L'individu compare son ratio <strong>contributions/rétributions</strong> à un référent. En cas d'iniquité perçue, il réduit ses efforts.",tags:["équité","comparaison"]},
  {concept:"Théorie ERG",author:"Alderfer (1969)",category:"motivation",definition:"3 niveaux : <strong>Existence, Relatedness, Growth</strong>. Plusieurs besoins actifs simultanément. Frustration d'un besoin supérieur → renforce les besoins inférieurs.",tags:["ERG","besoins"]},
  {concept:"Stratégie",author:"Chandler (1962)",category:"strategie",definition:"Détermination des <strong>buts à long terme</strong> et allocation des ressources pour les atteindre. Chandler : « <em>la structure suit la stratégie</em> ».",tags:["buts","long terme"]},
  {concept:"Analyse SWOT",author:"Andrews / Harvard (1965)",category:"strategie",definition:"Croise l'<strong>analyse interne</strong> (Forces / Faiblesses) et l'<strong>analyse externe</strong> (Opportunités / Menaces). Permet d'identifier les orientations stratégiques.",tags:["diagnostic","SWOT"]},
  {concept:"5 forces concurrentielles",author:"Porter (1979)",category:"strategie",definition:"Concurrents directs · Entrants potentiels · Substituts · Fournisseurs · Clients. L'intensité de ces forces détermine la rentabilité du secteur.",tags:["concurrence","secteur"]},
  {concept:"Stratégies génériques",author:"Porter (1980)",category:"strategie",definition:"<strong>Domination par les coûts</strong>, <strong>différenciation</strong> ou <strong>focalisation</strong>. Toute ambiguïté entre les deux premières mène à l'enlisement.",tags:["avantage concurrentiel","coût"]},
  {concept:"Chaîne de valeur",author:"Porter (1985)",category:"strategie",definition:"<strong>Activités principales</strong> (logistique, production, commercialisation, SAV) + <strong>Activités de soutien</strong> (infra, RH, R&D, achats). Source d'avantage concurrentiel.",tags:["valeur","activités"]},
  {concept:"Ressources VRIN",author:"Barney (1991)",category:"strategie",definition:"Avantage concurrentiel durable si les ressources sont <strong>V</strong>alables, <strong>R</strong>ares, <strong>I</strong>nimitables, <strong>N</strong>on-substituables.",tags:["VRIN","ressources"]},
  {concept:"Core competencies",author:"Prahalad & Hamel (1990)",category:"strategie",definition:"Les <strong>compétences distinctives</strong> (savoir-faire profonds, difficiles à imiter) constituent le socle de la stratégie et la source d'avantage durable.",tags:["compétences","avantage"]},
  {concept:"Matrice BCG",author:"Boston Consulting Group (1970)",category:"strategie",definition:"Portefeuille d'activités : <strong>Vedettes, Vaches à lait, Dilemmes, Poids morts</strong>. Croise part de marché relative et taux de croissance.",tags:["portefeuille","DAS"]},
  {concept:"Matrice Ansoff",author:"Ansoff (1965)",category:"strategie",definition:"4 voies de développement selon produits (actuels/nouveaux) × marchés (actuels/nouveaux) : pénétration, développement marché, développement produit, diversification.",tags:["croissance","développement"]},
  {concept:"Océan bleu",author:"Kim & Mauborgne (2005)",category:"strategie",definition:"Créer un <strong>espace de marché sans concurrence</strong> via l'outil ERAC (Éliminer, Réduire, Augmenter, Créer) plutôt que se battre sur les marchés existants.",tags:["innovation","ERAC"]},
  {concept:"Capacités dynamiques",author:"Teece, Pisano & Shuen (1997)",category:"strategie",definition:"Aptitude à <strong>reconfigurer ses compétences</strong> face aux évolutions rapides. L'avantage concurrentiel est fondé sur l'adaptation continue.",tags:["adaptation","dynamique"]},
  {concept:"CSV — Valeur partagée",author:"Porter & Kramer (2011)",category:"strategie",definition:"Créer de la valeur économique <strong>tout en créant de la valeur pour la société</strong>. La RSE est source d'innovation et d'avantage concurrentiel, pas un coût.",tags:["CSV","valeur","RSE"]},
  {concept:"5 composantes (Mintzberg)",author:"Mintzberg (1982)",category:"structure",definition:"Sommet stratégique · Ligne hiérarchique · Centre opérationnel · Technostructure · Fonctions de support. Leur configuration → type de structure.",tags:["Mintzberg","composantes"]},
  {concept:"6 mécanismes de coordination",author:"Mintzberg (1982)",category:"structure",definition:"Ajustement mutuel · Supervision directe · Standardisation des procédés / des résultats / des qualifications / des normes.",tags:["coordination","standardisation"]},
  {concept:"Structure et contingence",author:"Lawrence & Lorsch (1967)",category:"structure",definition:"Pas de structure universelle. La structure efficace dépend de l'environnement, de la taille, de la technologie et de la stratégie.",tags:["contingence","différenciation"]},
  {concept:"Technologie et structure",author:"Woodward (1965)",category:"structure",definition:"Production unitaire → organique · Production de masse → mécaniste · Production en continu → organique. Performance liée à l'adéquation structure/technologie.",tags:["technologie","production"]},
  {concept:"Délégation vs Décentralisation",author:"Fayol / Sloan",category:"structure",definition:"<strong>Délégation</strong> : transfert d'autorité ponctuel (responsabilité reste au délégant). <strong>Décentralisation</strong> : dispersion systématique du pouvoir vers les niveaux inférieurs.",tags:["autorité","pouvoir"]},
  {concept:"Leadership situationnel",author:"Hersey & Blanchard (1969)",category:"leadership",definition:"Style efficace selon la <strong>maturité du subordonné</strong> : directif → persuasif → participatif → délégatif.",tags:["situationnel","maturité"]},
  {concept:"Grille managériale",author:"Blake & Mouton (1964)",category:"leadership",definition:"Axes : intérêt pour la production et intérêt pour les hommes. Style idéal (9,9) : management participatif.",tags:["grille","styles"]},
  {concept:"Leadership transformationnel",author:"Burns (1978) / Bass (1985)",category:"leadership",definition:"Le leader inspire et transforme les valeurs de ses collaborateurs (vision, charisme, stimulation intellectuelle) vs leadership transactionnel (récompenses/sanctions).",tags:["vision","charisme"]},
  {concept:"Bases du pouvoir",author:"French & Raven (1959)",category:"leadership",definition:"5 bases : <strong>légitime</strong> (position), <strong>coercitif</strong> (sanction), <strong>de récompense</strong>, <strong>d'expertise</strong>, <strong>de référence</strong> (charisme).",tags:["pouvoir","influence"]},
  {concept:"Leadership serviteur",author:"Greenleaf (1970)",category:"leadership",definition:"Le leader est au <strong>service de ses collaborateurs</strong>. L'autorité découle de la confiance, non du statut.",tags:["service","confiance"]},
  {concept:"Rationalité limitée",author:"Simon (1955)",category:"decision",definition:"Le décideur ne peut explorer toutes les options. Il s'arrête à la première solution <strong>satisfaisante</strong> (satisficing) faute de temps, d'info et de capacité cognitive.",tags:["rationalité","satisficing"]},
  {concept:"Modèle IMC",author:"Simon (1960)",category:"decision",definition:"<strong>Intelligence</strong> (identification du problème) → <strong>Modélisation</strong> (conception de solutions) → <strong>Choice</strong> (sélection). Suivi d'une phase de contrôle.",tags:["IMC","processus"]},
  {concept:"Décision programmée / non programmée",author:"Simon (1960)",category:"decision",definition:"<strong>Programmée</strong> : routinière, traitée par des règles. <strong>Non programmée</strong> : unique, complexe, sans procédure établie.",tags:["programmée","routine"]},
  {concept:"Modèle de la poubelle",author:"Cohen, March & Olsen (1972)",category:"decision",definition:"Dans les anarchies organisées, les décisions résultent de la rencontre <strong>aléatoire</strong> de problèmes, solutions, participants et occasions de choix.",tags:["anarchie","aléatoire"]},
  {concept:"Coalitions (Cyert & March)",author:"Cyert & March (1963)",category:"decision",definition:"L'organisation est une coalition d'individus aux <strong>intérêts divergents</strong>. Les décisions résultent de négociations entre coalitions.",tags:["coalition","négociation"]},
  {concept:"Management par objectifs (DPO)",author:"Drucker (1954)",category:"decision",definition:"Objectifs fixés <strong>conjointement</strong> par manager et subordonné. Évaluation sur l'atteinte. Développe motivation et responsabilisation.",tags:["DPO","objectifs"]},
  {concept:"Culture organisationnelle",author:"Schein (1985)",category:"culture",definition:"3 niveaux : <strong>artefacts</strong> (visible) → valeurs déclarées → hypothèses profondes (invisible). La culture guide les comportements.",tags:["valeurs","Schein"]},
  {concept:"GPEC",author:"Loi Borloo (2005)",category:"culture",definition:"Démarche d'anticipation pour adapter les <strong>RH aux besoins futurs</strong> : diagnostic des compétences, projection, plan d'action (formation, mobilité, recrutement).",tags:["compétences","anticipation"]},
  {concept:"Contrat psychologique",author:"Rousseau (1989)",category:"culture",definition:"Attentes <strong>implicites et réciproques</strong> salarié/employeur au-delà du contrat formel. Sa violation → perte d'engagement.",tags:["attentes","implicite"]},
  {concept:"Théorie de l'agence",author:"Jensen & Meckling (1976)",category:"culture",definition:"Conflits entre mandants (actionnaires) et mandataires (dirigeants). Les mécanismes de gouvernance visent à <strong>aligner les intérêts</strong>.",tags:["agence","gouvernance"]},
  {concept:"Analyse PESTEL",author:"Concept collectif (1960-80)",category:"environnement",definition:"<strong>Politique · Économique · Socioculturel · Technologique · Environnemental · Légal</strong>. Identifie les opportunités et menaces du macro-environnement.",tags:["PESTEL","macro"]},
  {concept:"Turbulence de l'environnement",author:"Ansoff (1979) / Emery & Trist (1965)",category:"environnement",definition:"Plus l'environnement est turbulent, plus la planification cède la place à la flexibilité. Échelle de turbulence d'Ansoff : 1 (stable) à 5 (turbulent).",tags:["turbulence","incertitude"]},
  {concept:"Dépendance aux ressources",author:"Pfeffer & Salancik (1978)",category:"environnement",definition:"Les organisations dépendent de ressources extérieures. Stratégies de réduction : <strong>intégration verticale, alliances, lobbying, diversification</strong>.",tags:["dépendance","alliances"]},
  {concept:"Isomorphisme institutionnel",author:"DiMaggio & Powell (1983)",category:"environnement",definition:"Les organisations se ressemblent sous 3 pressions : <strong>coercitive</strong> (loi), <strong>mimétique</strong> (imitation), <strong>normative</strong> (professionnalisation).",tags:["institutionnel","mimétisme"]},
  {concept:"RSE",author:"Commission européenne (2001) / Carroll (1979)",category:"rse",definition:"Intégration <strong>volontaire</strong> de préoccupations sociales et environnementales. Carroll : pyramide économique → légale → éthique → philanthropique.",tags:["RSE","Carroll","volontaire"]},
  {concept:"Développement durable",author:"Rapport Brundtland / ONU (1987)",category:"rse",definition:"Développement répondant aux besoins présents <strong>sans compromettre ceux des générations futures</strong>. 3 piliers : économique, social, environnemental.",tags:["Brundtland","piliers"]},
  {concept:"Triple bottom line (3P)",author:"Elkington (1994)",category:"rse",definition:"Performance évaluée sur 3 dimensions : <strong>Profit · People · Planet</strong>. La rentabilité seule ne suffit pas.",tags:["3P","Elkington"]},
  {concept:"Parties prenantes",author:"Freeman (1984)",category:"rse",definition:"Tout acteur pouvant <strong>affecter ou être affecté</strong> par les objectifs de l'organisation. Primaires (actionnaires, salariés, clients) et secondaires (ONG, médias).",tags:["Freeman","stakeholders"]},
  {concept:"Pyramide de Carroll",author:"Carroll (1979)",category:"rse",definition:"4 niveaux : <strong>Économique</strong> (base) → <strong>Légale</strong> → <strong>Éthique</strong> → <strong>Philanthropique</strong> (sommet).",tags:["Carroll","éthique","niveaux"]},
  {concept:"CSRD — Reporting extra-financier",author:"Directive européenne (2022)",category:"rse",definition:"Obligation de publier des informations <strong>ESG</strong>. Remplace la DPEF. Normes ESRS, certification par OTI.",tags:["CSRD","ESG","reporting"]},
  {concept:"Greenwashing",author:"TerraChoice (2007)",category:"rse",definition:"Communication <strong>écologique trompeuse</strong> sans actions réelles. Risque juridique croissant (loi Climat & Résilience 2021).",tags:["communication","trompeuse"]},
  {concept:"ISO 26000",author:"ISO (2010)",category:"rse",definition:"Lignes directrices RSE <strong>non certifiables</strong>. 7 questions centrales : gouvernance, droits humains, travail, environnement, loyauté, consommateurs, communautés.",tags:["ISO","norme"]},
  {concept:"Entreprise à mission",author:"Loi PACTE (2019)",category:"rse",definition:"Statut permettant d'inscrire une <strong>raison d'être</strong> et des objectifs RSE dans les statuts. Contrôlé par comité de mission + OTI.",tags:["PACTE","raison d'être"]},
  {concept:"Devoir de vigilance",author:"Loi Vigilance (2017)",category:"rse",definition:"Obligation d'un <strong>plan de vigilance</strong> sur les risques droits humains et environnement, y compris chez les sous-traitants. 1ère loi mondiale du genre.",tags:["vigilance","sous-traitants"]},
];

/* ══════════════════════════════════════
   NAVIGATION
══════════════════════════════════════ */
document.querySelectorAll('.nav-btn').forEach(btn => {
  btn.addEventListener('click', () => {
    document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
    document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
    btn.classList.add('active');
    document.getElementById('tab-' + btn.dataset.tab).classList.add('active');
  });
});

/* ══════════════════════════════════════
   ANNALES
══════════════════════════════════════ */
function renderAnnales() {
  const g = document.getElementById('annales-grid');
  g.innerHTML = annales.map(a => `
    <div class="annale-card">
      <div class="annale-head">
        <div class="annale-year">${a.year}</div>
        <div class="annale-co">${a.moy} · ${a.reussite}</div>
      </div>
      <div class="annale-title">${a.co}</div>
      <div class="annale-body">
        <div class="annale-themes">${a.themes.map(t=>`<span class="atheme ${t.c}">${t.l}</span>`).join('')}</div>
        <div class="annale-q"><strong>Dossier 1 :</strong> ${a.q1notes}</div>
        <div class="annale-q" style="margin-top:0.4rem"><strong>Question problématisée :</strong> ${a.q2}</div>
      </div>
    </div>
  `).join('');

  const fb = document.getElementById('freq-bars');
  fb.innerHTML = freqs.map(f => `
    <div class="freq-row">
      <div class="freq-label">${f.label}</div>
      <div class="freq-bar-bg"><div class="freq-bar" style="width:${f.pct}%"></div></div>
      <div class="freq-pct">${f.pct}%</div>
    </div>
  `).join('');
}
renderAnnales();

/* ══════════════════════════════════════
   RÉPONSES TYPES
══════════════════════════════════════ */
let rtCat = 'all';
function renderRT() {
  const g = document.getElementById('rt-grid');
  const filtered = reponses.filter(r => rtCat === 'all' || r.cat === rtCat);
  g.innerHTML = filtered.map((r,i) => `
    <div class="rt-card" style="animation-delay:${i*0.04}s">
      <div class="rt-head" onclick="toggleRT('${r.id}')">
        <div class="rt-name">${r.name}</div>
        <div class="rt-meta">
          <span class="rt-cat" style="background:${r.catBg};color:${r.catColor};border:1px solid ${r.catColor}40">${r.cat}</span>
          <span class="rt-chevron" id="chev-${r.id}">▼</span>
        </div>
      </div>
      <div class="rt-body" id="rtb-${r.id}">
        <div class="rt-section">
          <div class="rt-section-title">Quand l'utiliser</div>
          <div class="rt-text">${r.quand}</div>
        </div>
        <div class="rt-section">
          <div class="rt-section-title">Structure clé</div>
          <div class="rt-text">${r.schema}</div>
        </div>
        <div class="rt-section">
          <div class="rt-section-title">Réponse type à adapter</div>
          <div class="rt-box">${r.reponse}</div>
        </div>
        <div class="rt-tip">${r.tip}</div>
      </div>
    </div>
  `).join('');
}
function toggleRT(id) {
  const body = document.getElementById('rtb-'+id);
  const chev = document.getElementById('chev-'+id);
  const open = body.classList.toggle('open');
  chev.style.transform = open ? 'rotate(180deg)' : '';
}
document.querySelectorAll('.rt-btn').forEach(btn => {
  btn.addEventListener('click', () => {
    document.querySelectorAll('.rt-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    rtCat = btn.dataset.rcat;
    renderRT();
  });
});
renderRT();

/* ══════════════════════════════════════
   LEXIQUE
══════════════════════════════════════ */
let lexCat = 'all', lexQ = '';
function catLabel(c) {
  const m={organisation:'Organisation',strategie:'Stratégie',structure:'Structure',leadership:'Leadership',decision:'Décision',motivation:'Motivation',culture:'Culture & GRH',environnement:'Environnement',rse:'RSE'};
  return m[c]||c;
}
function renderLex() {
  const g = document.getElementById('lex-grid');
  const filtered = lexique.filter(d => {
    const mc = lexCat==='all'||d.category===lexCat;
    const q = lexQ.toLowerCase();
    const ms = !q||d.concept.toLowerCase().includes(q)||d.author.toLowerCase().includes(q)||d.definition.toLowerCase().includes(q)||d.tags.some(t=>t.toLowerCase().includes(q));
    return mc && ms;
  });
  document.getElementById('lex-count').textContent = filtered.length + ' définition' + (filtered.length>1?'s':'') + ' affichée' + (filtered.length>1?'s':'');
  if(!filtered.length){g.innerHTML='<div class="lex-empty">Aucun résultat…</div>';return;}
  g.innerHTML = filtered.map((d,i)=>`
    <div class="lex-card" style="animation-delay:${Math.min(i*0.03,0.5)}s">
      <div class="lex-top">
        <div class="lex-concept">${d.concept}</div>
        <div class="lex-cat">${catLabel(d.category)}</div>
      </div>
      <div class="lex-author">${d.author}</div>
      <div class="lex-def">${d.definition}</div>
      <div class="lex-tags">${d.tags.map(t=>`<span class="ltag">${t}</span>`).join('')}</div>
    </div>
  `).join('');
}
document.getElementById('lex-search').addEventListener('input',e=>{lexQ=e.target.value;renderLex();});
document.querySelectorAll('.lf-btn').forEach(btn=>{
  btn.addEventListener('click',()=>{
    document.querySelectorAll('.lf-btn').forEach(b=>b.classList.remove('active'));
    btn.classList.add('active');
    lexCat=btn.dataset.lcat;
    renderLex();
  });
});
renderLex();
</script>
</body>
</html>