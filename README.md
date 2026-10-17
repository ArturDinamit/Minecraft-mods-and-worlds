<!doctype html>
<html lang="ru">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Моды для Minecraft — Моды и миры</title>

  <style>
    /* ---------------------------------------------------
       Визуальная система
       --------------------------------------------------- */
    :root{
      --bg: #e9f3ff;
      --bg-accent: linear-gradient(180deg, rgba(255,255,255,0.7), rgba(255,255,255,0.45));
      --surface: #ffffff;
      --muted: #5b6b82;
      --text: #0e1b2b;
      --accent: #1fb6ff;
      --accent-2: #7c4dff;
      --glass: rgba(255,255,255,0.55);
      --glass-2: rgba(255,255,255,0.12);
      --radius: 14px;
      --card-radius: 16px;
      --shadow-sm: 0 6px 20px rgba(18,30,50,0.08);
      --shadow-lg: 0 28px 60px rgba(10,20,40,0.14);
      --max-width: 1180px;
      --mono: ui-monospace, SFMono-Regular, Menlo, Monaco, "Roboto Mono", "Courier New", monospace;
      --ease: cubic-bezier(.2,.9,.25,1);
    }
    :root[data-theme="dark"]{
      --bg: #071016;
      --bg-accent: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      --surface: #0b1216;
      --muted: #9fb1c8;
      --text: #eaf6ff;
      --accent: #39b7ff;
      --accent-2: #9b7bff;
      --glass: rgba(255,255,255,0.03);
      --glass-2: rgba(255,255,255,0.04);
      --shadow-sm: 0 6px 18px rgba(0,0,0,0.6);
      --shadow-lg: 0 26px 60px rgba(0,0,0,0.6);
    }

    /* ---------------------------------------------------
       Reset & layout
       --------------------------------------------------- */
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family: Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
      background: radial-gradient(1200px 600px at 10% 10%, rgba(31,182,255,0.06), transparent),
                  radial-gradient(1000px 500px at 90% 90%, rgba(124,77,255,0.04), transparent),
                  var(--bg);
      color:var(--text);
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      min-height:100%;
      display:flex;
      flex-direction:column;
      align-items:center;
      padding:36px 20px 140px; /* место для нижней панели */
      gap:22px;
    }

    .container{
      width:100%;
      max-width:var(--max-width);
      display:flex;
      flex-direction:column;
      gap:22px;
    }

    header.top{
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:16px;
    }

    /* ---------------------------------------------------
       Header / Hero
       --------------------------------------------------- */
    .brand{
      display:flex;
      gap:14px;
      align-items:center;
    }
    .logo{
      width:56px;height:56px;border-radius:12px;
      display:flex;align-items:center;justify-content:center;
      background:linear-gradient(135deg,var(--accent),var(--accent-2));
      color:white;font-weight:800;font-size:18px;
      box-shadow:var(--shadow-lg);
    }
    .brand .titles{display:flex;flex-direction:column}
    .brand h1{margin:0;font-size:1.25rem;letter-spacing:-0.01em}
    .brand p{margin:0;color:var(--muted);font-size:0.9rem}

    .header-actions{
      display:flex;gap:10px;align-items:center;
    }

    .search{
      display:flex;align-items:center;gap:10px;padding:8px 12px;border-radius:12px;
      background:var(--surface);box-shadow:var(--shadow-sm);border:1px solid rgba(0,0,0,0.04);
      min-width:320px;max-width:520px;
    }
    .search input{
      border:0;background:transparent;outline:none;font-size:0.95rem;color:var(--text);
      width:100%;
    }
    .chip{
      padding:8px 10px;border-radius:10px;background:var(--glass);font-weight:600;color:var(--muted);cursor:default;
    }

    /* ---------------------------------------------------
       Main layout
       --------------------------------------------------- */
    .layout{
      display:grid;
      grid-template-columns: 1fr 340px;
      gap:20px;
      align-items:start;
    }
    @media (max-width:980px){
      .layout{grid-template-columns:1fr}
    }

    /* ---------------------------------------------------
       Cards & modules
       --------------------------------------------------- */
    .card{
      background: linear-gradient(180deg, var(--surface), color-mix(in srgb, var(--surface) 92%, transparent));
      border-radius:var(--card-radius);
      padding:18px;
      box-shadow:var(--shadow-sm);
      border:1px solid rgba(0,0,0,0.03);
    }
    :root[data-theme="dark"] .card{border-color:rgba(255,255,255,0.03)}

    .mods-grid{
      display:grid;
      grid-template-columns: repeat(3, 1fr);
      gap:16px;
    }
    @media (max-width:1100px){ .mods-grid{grid-template-columns: repeat(2,1fr)} }
    @media (max-width:640px){ .mods-grid{grid-template-columns: repeat(1,1fr)} }

    .mod-card{
      position:relative;
      overflow:hidden;
      border-radius:12px;
      background: linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.01));
      padding:12px;
      display:flex;
      gap:12px;
      align-items:flex-start;
      min-height:96px;
      transition:transform .35s var(--ease), box-shadow .35s var(--ease);
      border:1px solid rgba(0,0,0,0.04);
      cursor:pointer;
    }
    :root[data-theme="dark"] .mod-card{border-color:rgba(255,255,255,0.02)}
    .mod-card:hover{ transform:translateY(-6px); box-shadow:0 20px 60px rgba(3,10,30,0.12) }

    .mod-thumb{
      width:86px;height:86px;border-radius:10px;flex-shrink:0;
      background:linear-gradient(135deg,var(--accent),var(--accent-2));
      display:flex;align-items:center;justify-content:center;color:white;font-weight:800;font-size:20px;
      box-shadow:inset 0 -14px 30px rgba(0,0,0,0.12);
    }
    .mod-info{flex:1;display:flex;flex-direction:column;gap:6px}
    .mod-title{font-weight:700}
    .mod-meta{color:var(--muted);font-size:0.9rem;display:flex;gap:10px;align-items:center}

    .empty-hero{
      display:flex;
      gap:22px;
      align-items:center;
      justify-content:space-between;
      padding:22px;border-radius:12px;background: linear-gradient(90deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
    }
    .empty-hero .left{display:flex;gap:14px;align-items:center}
    .empty-illustration{
      width:110px;height:110px;border-radius:12px;display:flex;align-items:center;justify-content:center;
      background:linear-gradient(135deg,var(--accent),var(--accent-2));
      color:white;font-weight:900;font-size:34px;box-shadow:var(--shadow-sm);
    }
    .empty-text h3{margin:0;font-size:1.05rem}
    .empty-text p{margin:6px 0 0;color:var(--muted)}

    /* ---------------------------------------------------
       Sidebar
       --------------------------------------------------- */
    .sidebar .card{display:flex;flex-direction:column;gap:12px}
    .stat{
      display:flex;gap:14px;align-items:center;justify-content:space-between;
      padding:10px;border-radius:10px;background:var(--glass);
    }
    .stat .num{font-weight:800;font-size:1.1rem}
    .small{font-size:0.85rem;color:var(--muted)}

    /* ---------------------------------------------------
       Bottom floating bar (прозрачная полоса)
       --------------------------------------------------- */
    .bottom-bar{
      position:fixed;
      left:50%;
      transform:translateX(-50%);
      bottom:18px;
      width:clamp(360px, 92%, 1080px);
      display:flex;
      justify-content:space-between;
      gap:18px;
      padding:10px;
      border-radius:14px;
      background: linear-gradient(180deg, rgba(255,255,255,0.06), rgba(255,255,255,0.03));
      backdrop-filter: blur(10px) saturate(120%);
      box-shadow: 0 12px 40px rgba(6,12,20,0.12);
      z-index:60;
      align-items:center;
      pointer-events:auto;
      border:1px solid rgba(0,0,0,0.04);
    }
    :root[data-theme="dark"] .bottom-bar{ background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); border-color:rgba(255,255,255,0.02) }

    .tabs{display:flex;gap:8px;align-items:center}
    .tab{
      padding:10px 14px;border-radius:10px;background:transparent;border:0;color:var(--text);
      display:inline-flex;gap:8px;align-items:center;font-weight:700;cursor:pointer;
    }
    .tab.active{
      background: linear-gradient(90deg, color-mix(in srgb, var(--accent) 18%, transparent), transparent);
      box-shadow:0 6px 18px rgba(0,0,0,0.08);
    }

    .bottom-right{display:flex;gap:10px;align-items:center;color:var(--muted);font-weight:600}

    /* ---------------------------------------------------
       Settings panel popup
       --------------------------------------------------- */
    .settings-panel{
      position:fixed;left:50%;transform:translateX(-50%);
      bottom:86px;width:clamp(320px, 86%, 480px);z-index:70;display:none;
    }
    .settings-panel.open{display:block}
    .settings-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px}
    .option-btn{padding:10px;border-radius:10px;border:1px solid rgba(0,0,0,0.06);background:var(--glass);cursor:pointer;font-weight:700}
    :root[data-theme="dark"] .option-btn{border-color:rgba(255,255,255,0.04)}
    .option-btn.active{background:linear-gradient(90deg,var(--accent),var(--accent-2));color:#001827;box-shadow:0 8px 22px rgba(6,12,32,0.12)}

    /* ---------------------------------------------------
       Modal (детали мода)
       --------------------------------------------------- */
    .modal-backdrop{ position:fixed;inset:0;background:rgba(2,6,12,0.5);display:none;align-items:center;justify-content:center;z-index:120 }
    .modal-backdrop.open{display:flex}
    .modal{
      width:clamp(320px, 80%, 920px);
      max-height:86vh;overflow:auto;border-radius:14px;padding:18px;background:var(--surface);
      box-shadow:var(--shadow-lg);border:1px solid rgba(0,0,0,0.06);
    }
    :root[data-theme="dark"] .modal{border-color:rgba(255,255,255,0.03)}

    .modal .hero{display:flex;gap:12px;align-items:center}
    .modal .hero .thumb{width:120px;height:120px;border-radius:12px;background:linear-gradient(135deg,var(--accent),var(--accent-2));display:flex;align-items:center;justify-content:center;color:white;font-weight:900;font-size:32px}

    .meta-row{display:flex;gap:12px;flex-wrap:wrap;margin-top:10px;color:var(--muted)}
    .modal .actions{display:flex;gap:10px;margin-top:12px}

    /* ---------------------------------------------------
       Tiny helpers & animations
       --------------------------------------------------- */
    .btn{
      padding:10px 14px;border-radius:10px;border:0;background:var(--accent);color:white;font-weight:800;cursor:pointer;transition:transform .18s var(--ease);
    }
    .btn.secondary{background:transparent;border:1px solid rgba(0,0,0,0.06);color:var(--text)}
    :root[data-theme="dark"] .btn.secondary{border-color:rgba(255,255,255,0.04)}
    .btn:active{transform:translateY(1px)}

    .skeleton{
      background: linear-gradient(90deg, rgba(255,255,255,0.03), rgba(255,255,255,0.06), rgba(255,255,255,0.03));
      border-radius:10px;height:12px;animation:shimmer 1.6s linear infinite;
    }
    @keyframes shimmer{0%{background-position:-200px 0}100%{background-position:200px 0}}

    footer.small{ text-align:center;color:var(--muted);font-size:0.85rem;margin-top:6px }

    /* Accessibility focus */
    [role="button"], button { outline: none; }
    button:focus, .tab:focus, .option-btn:focus { box-shadow:0 0 0 4px rgba(31,182,255,0.12); border-radius:10px; }

  </style>
</head>
<body>
  <div class="container" id="app">
    <header class="top" role="banner">
      <div class="brand">
        <div class="logo" aria-hidden="true">MC</div>
        <div class="titles">
          <h1 data-i18n="siteTitle">Моды и миры — Minecraft</h1>
          <p data-i18n="siteSubtitle">Красивый витринный сайт для твоих модов (пока пусто)</p>
        </div>
      </div>

      <div class="header-actions" role="search">
        <div class="search" aria-label="Поиск модов">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true"><path d="M21 21l-4.35-4.35" stroke="currentColor" stroke-width="1.6" stroke-linecap="round"/></svg>
          <input type="search" id="searchInput" placeholder="Поиск модов..." />
          <div style="width:6px"></div>
        </div>
        <div class="chip" id="versionChip">v0.1</div>
      </div>
    </header>

    <div class="layout" role="main">
      <!-- LEFT: Main content -->
      <section>
        <div class="card">
          <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:10px">
            <div>
              <h2 style="margin:0" data-i18n="modsTitle">Моды</h2>
              <div class="small" data-i18n="modsSubtitle">Коллекция модов — пока пусто, но дизайн готов</div>
            </div>

            <div style="display:flex;gap:8px;align-items:center">
              <button class="btn" id="newModBtn" title="Добавить мод" aria-label="Добавить мод">Добавить мод</button>
              <button class="btn secondary" id="importBtn" title="Импорт">Импорт</button>
            </div>
          </div>

          <!-- Empty state hero -->
          <div class="empty-hero" id="emptyHero">
            <div class="left">
              <div class="empty-illustration" aria-hidden="true">MC</div>
              <div class="empty-text">
                <h3 data-i18n="emptyTitle">Здесь пока пусто</h3>
                <p data-i18n="emptyDesc">Добавь свои моды — они появятся в красивых карточках с превью и описанием.</p>
                <div style="height:10px"></div>
                <div style="display:flex;gap:8px">
                  <button class="btn" id="ctaAdd">Добавить мод</button>
                  <button class="btn secondary" id="ctaBrowse">Обзор</button>
                </div>
              </div>
            </div>
            <div style="min-width:320px;display:flex;flex-direction:column;gap:10px;align-items:flex-end">
              <div style="width:220px;height:120px;border-radius:12px;background:linear-gradient(135deg, rgba(255,255,255,0.04), rgba(255,255,255,0.01));display:flex;align-items:center;justify-content:center;">
                <div style="text-align:center;color:var(--muted)"><strong>Превью мода</strong><div class="small">Будет здесь</div></div>
              </div>
              <div style="width:220px;display:flex;gap:8px;justify-content:flex-end">
                <div class="skeleton" style="width:90px;height:28px;border-radius:8px"></div>
                <div class="skeleton" style="width:90px;height:28px;border-radius:8px"></div>
              </div>
            </div>
          </div>

          <!-- Grid (hidden by default while empty) -->
          <div id="modsGridWrap" style="margin-top:14px;display:none">
            <div class="mods-grid" id="modsGrid" role="list" aria-live="polite">
              <!-- Example mod cards (if there were mods) -->
            </div>
          </div>
        </div>

        <!-- Optional: Recent activity or changelog -->
        <div style="height:14px"></div>
        <div class="card">
          <h3 style="margin:0 0 8px 0">Что дальше</h3>
          <div class="small">- Поддержка загрузки архивов модов (.jar / .zip)</div>
          <div class="small">- Страницы отдельных модов и рейтинги</div>
          <div class="small">- Экспорт/импорт коллекций</div>
        </div>
      </section>

      <!-- RIGHT: Sidebar -->
      <aside class="sidebar">
        <div class="card">
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div>
              <div class="small">Статистика</div>
              <div style="font-weight:800;font-size:1.25rem" id="modsCount">0 модов</div>
            </div>
            <div style="display:flex;flex-direction:column;gap:8px;align-items:flex-end">
              <div class="small">Тема</div>
              <div id="themeBadge" style="padding:6px 10px;border-radius:8px;background:var(--glass);font-weight:700">Светлая</div>
            </div>
          </div>

          <div style="height:12px"></div>
          <div class="stat"><div class="small">Последнее обновление</div><div class="num">—</div></div>

          <div style="height:10px"></div>
          <div style="display:flex;gap:8px">
            <button class="option-btn" id="openSettingsBtn">Настройки</button>
            <button class="option-btn" id="openAboutBtn">О сайте</button>
          </div>
        </div>

        <div style="height:14px"></div>
        <div class="card">
          <h4 style="margin:0 0 8px 0">Быстрые фильтры</h4>
          <div style="display:flex;gap:8px;flex-wrap:wrap">
            <button class="option-btn" data-filter="all">Все</button>
            <button class="option-btn" data-filter="fun">Развлечение</button>
            <button class="option-btn" data-filter="tech">Техника</button>
            <button class="option-btn" data-filter="worlds">Миры</button>
          </div>
        </div>
      </aside>
    </div>

    <footer class="small" aria-hidden="true">© 2026 Мои моды — макет</footer>
  </div>

  <!-- Bottom transparent bar -->
  <nav class="bottom-bar" role="navigation" aria-label="Навигация">
    <div class="tabs" role="tablist">
      <button class="tab active" id="tabMods" role="tab" aria-pressed="true" aria-controls="modsGridWrap">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" style="opacity:0.95"><path d="M3 7h18M7 7v10M17 7v10" stroke="currentColor" stroke-width="1.4" stroke-linecap="round"/></svg>
        <span data-i18n="modsLabel">Моды</span>
      </button>
      <button class="tab" id="tabSettings" role="tab" aria-pressed="false" aria-controls="settingsPanel">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" style="opacity:0.95"><path d="M12 15.5a3.5 3.5 0 1 0 0-7 3.5 3.5 0 0 0 0 7z" stroke="currentColor" stroke-width="1.2" stroke-linecap="round"/></svg>
        <span data-i18n="settingsLabel">Настройки</span>
      </button>
    </div>

    <div class="bottom-right" aria-hidden="true">
      <div class="small">Тема: <span id="bottomTheme">Светлая</span></div>
      <div class="small">Язык: <span id="bottomLang">RU</span></div>
    </div>
  </nav>

  <!-- Settings popup -->
  <div class="settings-panel" id="settingsPanel" role="dialog" aria-modal="true" aria-labelledby="settingsTitle">
    <div class="card">
      <h3 id="settingsTitle">Настройки</h3>
      <div style="display:flex;gap:8px;align-items:center;justify-content:space-between;margin-top:8px">
        <div>
          <div class="small">Тема</div>
          <div style="display:flex;gap:8px;margin-top:8px">
            <button class="option-btn" id="optLight" data-theme="light">Светлая</button>
            <button class="option-btn" id="optDark" data-theme="dark">Тёмная</button>
          </div>
        </div>
        <div style="min-width:120px">
          <div class="small">Язык</div>
          <select id="langSelect" style="margin-top:8px;padding:8px;border-radius:10px;width:100%">
            <option value="ru">Русский</option>
            <option value="en">English</option>
          </select>
        </div>
      </div>

      <div style="height:12px"></div>
      <div style="display:flex;justify-content:flex-end;gap:8px">
        <button class="option-btn" id="resetBtn">Сбросить</button>
        <button class="btn" id="saveSettingsBtn">Сохранить</button>
      </div>
    </div>
  </div>

  <!-- Modal for mod details -->
  <div class="modal-backdrop" id="modalBackdrop" aria-hidden="true">
    <div class="modal" role="dialog" aria-modal="true" aria-labelledby="modalTitle">
      <div style="display:flex;justify-content:space-between;align-items:center">
        <h3 id="modalTitle">Название мода</h3>
        <button class="option-btn" id="closeModal">Закрыть</button>
      </div>
      <div style="height:12px"></div>

