<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Расписание консультаций</title>
<style id="theme-style"></style>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{padding:0.5rem 0;transition:background .2s,color .2s}
h1{font-size:20px;font-weight:500;margin-bottom:1rem}
button{font-family:inherit;font-size:var(--fs);padding:6px 12px;border:1px solid var(--border);border-radius:var(--radius);background:var(--btn-bg);color:var(--text);cursor:pointer;transition:background .15s}
button:hover{background:var(--btn-hover)}
input,select{font-family:inherit;font-size:var(--fs);padding:7px 10px;border:1px solid var(--border);border-radius:var(--radius);background:var(--input-bg);color:var(--text);outline:none}
input:focus,select:focus{border-color:var(--accent)}
.card{background:var(--card-bg);border:1px solid var(--border);border-radius:calc(var(--radius)*1.5);padding:1rem 1.25rem;margin-bottom:1rem}
.sec-title{font-size:11px;font-weight:500;color:var(--muted);text-transform:uppercase;letter-spacing:.05em;margin-bottom:.75rem}
.chips{display:flex;flex-wrap:wrap;gap:5px;margin-bottom:.75rem;min-height:24px}
.chip{display:inline-flex;align-items:center;gap:4px;padding:3px 10px;border:1px solid var(--border);border-radius:20px;font-size:calc(var(--fs) - 1px);background:var(--chip-bg);color:var(--text)}
.chip-x{background:none;border:none;cursor:pointer;color:var(--muted);font-size:15px;line-height:1;padding:0}
.chip-x:hover{color:#c0392b}
.ghost{font-size:calc(var(--fs) - 1px);color:var(--muted);font-style:italic}
.row{display:flex;gap:8px;flex-wrap:wrap;align-items:center}
.warn-bar{background:#fde8e0;border:1px solid #ea580c;border-radius:var(--radius);padding:8px 12px;font-size:var(--fs);color:#9a3412;margin-bottom:1rem;display:none}
/* Tabs */
.tabs{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:1rem}
.tab{padding:5px 13px;border:1px solid var(--border);border-radius:var(--radius);background:var(--btn-bg);color:var(--muted);font-size:var(--fs)}
.tab.active{color:var(--text);border-color:var(--accent);font-weight:500;background:var(--card-bg)}
.tab.dashed{border-style:dashed}
/* Schedule table */
.sched-block-title{font-size:12px;font-weight:500;color:var(--muted);margin-bottom:.5rem}
.grid-wrap{overflow-x:auto}
table.sched{width:100%;border-collapse:collapse;font-size:var(--fs)}
table.sched th,table.sched td{padding:7px 9px;border:1px solid var(--border);vertical-align:top;text-align:left}
table.sched th{background:var(--th-bg);font-size:calc(var(--fs) - 1px);font-weight:500;color:var(--muted);white-space:nowrap}
table.sched td:first-child{min-width:150px;background:var(--td-first-bg)}
.slot-label{font-weight:500;line-height:1.4}
.slot-sub{font-size:calc(var(--fs) - 2px);color:var(--muted);margin-top:2px}
.cell-inner{display:flex;flex-direction:column;gap:3px}
.assign-label{font-size:calc(var(--fs) - 1px);padding:2px 0;color:var(--text)}
.assign-label.conflict{color:#9a3412;font-weight:600}
.btn-assign{font-size:calc(var(--fs) - 2px);padding:2px 7px;border:1px dashed var(--border);border-radius:var(--radius);margin-top:2px;color:var(--muted)}
.btn-assign:hover{border-color:var(--accent);color:var(--text)}
/* Overlay */
.overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,.35);z-index:100}
.overlay.open{display:block}
.modal{background:var(--card-bg);border:1px solid var(--border);border-radius:calc(var(--radius)*1.5);padding:1.25rem;width:380px;max-width:96vw;max-height:80vh;overflow-y:auto;box-shadow:0 6px 32px rgba(0,0,0,.22);position:absolute}
.modal h3{font-size:15px;font-weight:500;margin-bottom:1rem;color:var(--text)}
.field{margin-bottom:.75rem}
.field label{display:block;font-size:12px;color:var(--muted);margin-bottom:4px}
.field input,.field select{width:100%}
.mrow{display:flex;gap:8px}
.mrow .field{flex:1}
.modal-actions{display:flex;gap:8px;justify-content:flex-end;margin-top:1rem}
.btn-red{border-color:#ea580c !important;color:#9a3412 !important}
.btn-red:hover{background:#fde8e0 !important}
/* Calendar */
.cal-wrap{border:1px solid var(--border);border-radius:var(--radius);overflow:hidden;margin-top:4px}
.cal-header{display:flex;align-items:center;justify-content:space-between;padding:6px 10px;background:var(--th-bg);font-size:13px;font-weight:500;color:var(--text)}
.cal-nav{background:none;border:none;cursor:pointer;color:var(--muted);font-size:18px;padding:0 4px;line-height:1}
.cal-grid{display:grid;grid-template-columns:repeat(7,1fr)}
.cal-day-name{text-align:center;font-size:11px;color:var(--muted);padding:4px 0;background:var(--th-bg)}
.cal-day{text-align:center;font-size:12px;padding:6px 2px;cursor:pointer;color:var(--text);border-radius:4px}
.cal-day:hover{background:var(--btn-hover)}
.cal-day.today{font-weight:600;color:var(--accent)}
.cal-day.selected{background:var(--accent);color:#fff !important}
.cal-day.empty{cursor:default}
/* Pick students */
.pick-list{display:flex;flex-direction:column;gap:2px;max-height:240px;overflow-y:auto;border:1px solid var(--border);border-radius:var(--radius);padding:6px;margin-top:4px}
.pick-class-header{display:flex;align-items:center;justify-content:space-between;padding:4px 6px;font-size:11px;font-weight:600;color:var(--muted);text-transform:uppercase;letter-spacing:.04em;margin-top:4px}
.pick-class-header:first-child{margin-top:0}
.pick-class-header button{font-size:11px;padding:1px 7px;border-radius:6px}
.pick-item{display:flex;align-items:center;gap:8px;padding:4px 6px;border-radius:6px;cursor:pointer;font-size:var(--fs);color:var(--text)}
.pick-item:hover{background:var(--btn-hover)}
.pick-item input[type=checkbox]{width:14px;height:14px;cursor:pointer;accent-color:var(--accent)}
.pick-all-row{display:flex;gap:6px;margin-bottom:6px;flex-wrap:wrap}
.pick-all-row button{font-size:12px;padding:3px 8px}
/* Appearance panel */
.appear-grid{display:grid;grid-template-columns:1fr 1fr;gap:.75rem}
.appear-grid .field{margin-bottom:0}
.color-swatches{display:flex;gap:6px;flex-wrap:wrap;margin-top:4px}
.swatch{width:28px;height:28px;border-radius:50%;cursor:pointer;border:2px solid transparent;transition:transform .1s}
.swatch:hover{transform:scale(1.15)}
.swatch.active{border-color:var(--text)}
/* Legend */
.legend{display:flex;gap:12px;flex-wrap:wrap;font-size:12px;color:var(--muted);margin-top:.75rem}
.leg{display:flex;align-items:center;gap:5px}
.dot{width:10px;height:10px;border-radius:50%;flex-shrink:0}
/* Top bar */
.top-bar{display:flex;align-items:center;justify-content:space-between;margin-bottom:1rem;flex-wrap:wrap;gap:.5rem}
  body {
  max-width: 100% !important;
  padding-left: 0.5rem !important;
  padding-right: 0.5rem !important;
}
.card,
.grid-wrap,
.sched,
.tabs,
.modal {
  max-width: 100% !important;
}
/* Если всё ещё есть ограничитель – перебиваем все возможные контейнеры */
.container, .wrapper, main, article, .site-container {
  max-width: 100% !important;
  width: 100% !important;
}
</style>
</head>
<body>

<div class="top-bar">
  <h1>Расписание консультаций</h1>
  <div style="display:flex;gap:8px;flex-wrap:wrap">
    <button onclick="exportPng()" id="btn-export" style="font-size:12px">📷 Поделиться (PNG)</button>
    <button onclick="openOverlay('m-appear',this)" style="font-size:12px">⚙ Оформление</button>
  </div>
</div>
<div id="warn-bar" class="warn-bar"></div>

<div class="tabs" id="tabs"></div>
<div id="class-panel" class="card"></div>

<div class="card">
  <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:.75rem">
    <div class="sec-title" style="margin:0">Расписание</div>
    <button onclick="openConsultModal(null,this)">+ Добавить консультацию</button>
  </div>
  <div id="sched-root"></div>
  <div class="legend">
    <span class="leg"><span class="dot" style="background:var(--accent)"></span>Назначены ученики</span>
    <span class="leg"><span class="dot" style="background:#ea580c"></span>Конфликт по времени</span>
  </div>
</div>

<!-- Modal: консультация -->
<div class="overlay" id="m-consult">
  <div class="modal">
    <h3 id="m-consult-title">Новая консультация</h3>
    <div class="field"><label>Предмет</label><input id="f-subject" type="text" placeholder="Математика"></div>
    <div class="field"><label>Учитель</label><input id="f-teacher" type="text" placeholder="Иванова А.Б."></div>
    <div class="field"><label>Дата</label>
      <input id="f-date-display" type="text" placeholder="Выберите дату" readonly style="cursor:pointer;width:100%" onclick="toggleCal()">
      <input id="f-date" type="hidden">
      <div class="cal-wrap" id="cal" style="display:none">
        <div class="cal-header"><button class="cal-nav" onclick="calPrev()">&#8249;</button><span id="cal-month-label"></span><button class="cal-nav" onclick="calNext()">&#8250;</button></div>
        <div class="cal-grid" id="cal-day-names"></div>
        <div class="cal-grid" id="cal-days"></div>
      </div>
    </div>
    <div class="mrow">
      <div class="field"><label>Начало</label><input id="f-ts" type="time" value="13:00"></div>
      <div class="field"><label>Окончание</label><input id="f-te" type="time" value="14:00"></div>
    </div>
    <div class="modal-actions">
      <button onclick="closeOverlay('m-consult')">Отмена</button>
      <button onclick="saveConsult()">&#10003; Сохранить</button>
    </div>
  </div>
</div>

<!-- Modal: назначение учеников -->
<div class="overlay" id="m-pick">
  <div class="modal">
    <h3 id="m-pick-title">Назначить учеников</h3>
    <p id="m-pick-sub" style="font-size:12px;color:var(--muted);margin-bottom:.75rem"></p>
    <div class="pick-all-row">
      <button onclick="pickAll(true)">Выбрать всех</button>
      <button onclick="pickAll(false)">Снять всех</button>
    </div>
    <div class="pick-list" id="pick-list"></div>
    <div class="modal-actions">
      <button onclick="closeOverlay('m-pick')">Отмена</button>
      <button onclick="savePick()">&#10003; Применить</button>
    </div>
  </div>
</div>

<!-- Modal: копировать -->
<div class="overlay" id="m-copy">
  <div class="modal">
    <h3>Копировать консультацию</h3>
    <p id="m-copy-sub" style="font-size:12px;color:var(--muted);margin-bottom:.5rem"></p>
    <p style="font-size:12px;color:var(--text);margin-bottom:.5rem">Выберите даты для копирования:</p>
    <div class="cal-wrap">
      <div class="cal-header"><button class="cal-nav" onclick="copyCal(-1)">&#8249;</button><span id="copy-cal-label"></span><button class="cal-nav" onclick="copyCal(1)">&#8250;</button></div>
      <div class="cal-grid" id="copy-cal-names"></div>
      <div class="cal-grid" id="copy-cal-days"></div>
    </div>
    <p style="font-size:12px;color:var(--muted);margin-top:.5rem">Выбрано: <span id="copy-selected-list">—</span></p>
    <div class="modal-actions">
      <button onclick="closeOverlay('m-copy')">Отмена</button>
      <button onclick="saveCopy()">&#10003; Скопировать</button>
    </div>
  </div>
</div>

<!-- Modal: новый класс -->
<div class="overlay" id="m-class">
  <div class="modal">
    <h3>Новый класс</h3>
    <div class="field"><label>Название</label><input id="f-class-name" type="text" placeholder="11В" onkeydown="if(event.key==='Enter')saveClass()"></div>
    <div class="modal-actions">
      <button onclick="closeOverlay('m-class')">Отмена</button>
      <button onclick="saveClass()">&#10003; Создать</button>
    </div>
  </div>
</div>

<!-- Modal: удалить класс -->
<div class="overlay" id="m-del-class">
  <div class="modal">
    <h3 id="m-del-class-title">Удалить класс?</h3>
    <p style="font-size:13px;color:var(--muted);margin-bottom:.5rem">Все данные класса будут удалены.</p>
    <div class="modal-actions">
      <button onclick="closeOverlay('m-del-class')">Отмена</button>
      <button class="btn-red" onclick="confirmDelClass()">&#128465; Удалить</button>
    </div>
  </div>
</div>

<!-- Modal: удалить консультацию -->
<div class="overlay" id="m-del-consult">
  <div class="modal">
    <h3>Удалить консультацию?</h3>
    <p style="font-size:13px;color:var(--muted);margin-bottom:.5rem">Все назначения будут удалены.</p>
    <div class="modal-actions">
      <button onclick="closeOverlay('m-del-consult')">Отмена</button>
      <button class="btn-red" onclick="confirmDelConsult()">&#128465; Удалить</button>
    </div>
  </div>
</div>

<!-- Modal: оформление -->
<div class="overlay" id="m-appear">
  <div class="modal">
    <h3>Оформление</h3>
    <div class="field">
      <label>Цветовая схема</label>
      <div class="color-swatches" id="swatches"></div>
    </div>
    <div class="appear-grid">
      <div class="field">
        <label>Шрифт</label>
        <select id="sel-font" onchange="applyAppear()">
          <option value="system-ui,-apple-system,sans-serif">Системный</option>
          <option value="'Segoe UI',sans-serif">Segoe UI</option>
          <option value="Georgia,serif">Georgia (с засечками)</option>
          <option value="'Courier New',monospace">Courier (моноширинный)</option>
          <option value="Arial,sans-serif">Arial</option>
          <option value="'Times New Roman',serif">Times New Roman</option>
        </select>
      </div>
      <div class="field">
        <label>Размер текста</label>
        <select id="sel-size" onchange="applyAppear()">
          <option value="12">Мелкий (12px)</option>
          <option value="13" selected>Обычный (13px)</option>
          <option value="15">Крупный (15px)</option>
          <option value="17">Очень крупный (17px)</option>
        </select>
      </div>
      <div class="field">
        <label>Скругление углов</label>
        <select id="sel-radius" onchange="applyAppear()">
          <option value="4px">Минимальное</option>
          <option value="8px" selected>Стандартное</option>
          <option value="14px">Большое</option>
        </select>
      </div>
    </div>
    <div class="modal-actions">
      <button onclick="closeOverlay('m-appear')">Закрыть</button>
    </div>
  </div>
</div>

<script>
// ===================== DATA =====================
var STUDENTS = {
  '9А': [
    {full:'Алексеев Артур',    short:'Алексеев А.'},
    {full:'Алексеева Валерия', short:'Алексеева В.'},
    {full:'Вензель Артур',     short:'Вензель А.'},
    {full:'Данилов Максим',    short:'Данилов М.'},
    {full:'Данилова Нарыйаана',short:'Данилова Н.'},
    {full:'Егоров Айтал',      short:'Егоров А.'},
    {full:'Жиркова Алина',     short:'Жиркова А.'},
    {full:'Захарова Айсаара',  short:'Захарова А.'},
    {full:'Иванова Дайаана',   short:'Иванова Д.'},
    {full:'Ксенофонтов Евгений',short:'Ксенофонтов Е.'},
    {full:'Кузьмина Инесса',   short:'Кузьмина И.'},
    {full:'Петрова Амелия',    short:'Петрова А.'},
    {full:'Попова Айыллаана',  short:'Попова А.'},
    {full:'Сметанин Александр',short:'Сметанин А.'},
    {full:'Созонов Николай',   short:'Созонов Н.'},
    {full:'Степанова Нелли',   short:'Степанова Н.'},
    {full:'Сыромятникова Валерия',short:'Сыромятникова В.'},
    {full:'Федоров Сайаан',    short:'Федоров С.'},
    {full:'Федорова Кристина', short:'Федорова К.'},
    {full:'Фёдорова Кристина', short:'Фёдорова К.'}
  ],
  '9Б': [
    {full:'Антонова Амелия',    short:'Антонова А.'},
    {full:'Бойков Андрей',      short:'Бойков А.'},
    {full:'Данилов Константин', short:'Данилов К.'},
    {full:'Егоров Лев',         short:'Егоров Л.'},
    {full:'Захаров Герман',     short:'Захаров Г.'},
    {full:'Иванов Маркел',      short:'Иванов М.'},
    {full:'Колесов Денис',      short:'Колесов Д.'},
    {full:'Максимов Лука',      short:'Максимов Л.'},
    {full:'Матвеев Давид',      short:'Матвеев Д.'},
    {full:'Никифоров Айгылаан', short:'Никифоров А.'},
    {full:'Никифорова Моника',  short:'Никифорова М.'},
    {full:'Оленов Арсентий',    short:'Оленов А.'},
    {full:'Пахомов Владимир',   short:'Пахомов В.'},
    {full:'Скрыбыкина Анэля',   short:'Скрыбыкина А.'},
    {full:'Уломжинский Арсен',  short:'Уломжинский А.'},
    {full:'Федотова Анжелина',  short:'Федотова А.'},
    {full:'Федотова Дайаана',   short:'Федотова Д.'}
  ],
  '9В': [
    {full:'Алексеев Андриан',   short:'Алексеев А.'},
    {full:'Алексеева Анастасия',short:'Алексеева Ан.'},
    {full:'Алексеева Аделина',  short:'Алексеева Ад.'},
    {full:'Аргунова Ильяна',    short:'Аргунова И.'},
    {full:'Буц Арина',          short:'Буц А.'},
    {full:'Васильева Сафина',   short:'Васильева С.'},
    {full:'Винтоняк Аристарх',  short:'Винтоняк А.'},
    {full:'Григорьева Кира',    short:'Григорьева К.'},
    {full:'Колесова Виолетта',  short:'Колесова В.'},
    {full:'Константинов Марк',  short:'Константинов М.'},
    {full:'Лаптев Вячеслав',    short:'Лаптев В.'},
    {full:'Максимова Айталина', short:'Максимова А.'},
    {full:'Мамаев-Слепцов Эрхан',short:'Мамаев-Слепцов Э.'},
    {full:'Петров Даниил',      short:'Петров Д.'},
    {full:'Степанова Айыллаана',short:'Степанова А.'},
    {full:'Стручкова Александра',short:'Стручкова А.'},
    {full:'Тимофеев Илсан',     short:'Тимофеев И.'},
    {full:'Христофоров Сандал', short:'Христофоров С.'}
  ]
};

// Build shortName lookup: full -> short
var SHORT = {};
Object.keys(STUDENTS).forEach(function(cn){
  STUDENTS[cn].forEach(function(s){ SHORT[s.full]=s.short; });
});
function shortName(full){ return SHORT[full]||full; }

var S = {
  classes: [
    {id:'c1', name:'9А', students: STUDENTS['9А'].map(function(s){return s.full;})},
    {id:'c2', name:'9Б', students: STUDENTS['9Б'].map(function(s){return s.full;})},
    {id:'c3', name:'9В', students: STUDENTS['9В'].map(function(s){return s.full;})}
  ],
  consults: [
    {id:'q1',  subject:'Математика', teacher:'Петрова Н.В.',  date:'2026-06-02', ts:'13:00', te:'14:00'},
    {id:'q2',  subject:'Физика',     teacher:'Орлов С.П.',    date:'2026-06-02', ts:'14:00', te:'15:00'},
    {id:'q3',  subject:'История',    teacher:'Смирнов А.Б.',  date:'2026-06-03', ts:'13:00', te:'14:00'},
    {id:'q4',  subject:'Биология',   teacher:'Кузнецова В.И.',date:'2026-06-03', ts:'15:00', te:'16:00'},
    {id:'q5',  subject:'Химия',      teacher:'Тарасов М.Е.',  date:'2026-06-04', ts:'13:00', te:'14:00'},
    {id:'q6',  subject:'Математика', teacher:'Петрова Н.В.',  date:'2026-06-04', ts:'14:30', te:'15:30'},
    {id:'q7',  subject:'Русский язык',teacher:'Ефимова Т.Л.', date:'2026-06-05', ts:'13:00', te:'14:00'},
    {id:'q8',  subject:'Физика',     teacher:'Орлов С.П.',    date:'2026-06-05', ts:'14:00', te:'15:00'},
    {id:'q9',  subject:'География',  teacher:'Волков Д.А.',   date:'2026-06-06', ts:'13:00', te:'14:00'},
    {id:'q10', subject:'История',    teacher:'Смирнов А.Б.',  date:'2026-06-06', ts:'14:00', te:'15:00'},
    {id:'q11', subject:'Информатика',teacher:'Лебедев А.С.',  date:'2026-06-09', ts:'13:00', te:'14:00'},
    {id:'q12', subject:'Математика', teacher:'Петрова Н.В.',  date:'2026-06-09', ts:'15:00', te:'16:00'},
    {id:'q13', subject:'Биология',   teacher:'Кузнецова В.И.',date:'2026-06-10', ts:'13:00', te:'14:00'},
    {id:'q14', subject:'Химия',      teacher:'Тарасов М.Е.',  date:'2026-06-10', ts:'14:00', te:'15:00'},
    {id:'q15', subject:'Русский язык',teacher:'Ефимова Т.Л.', date:'2026-06-11', ts:'13:00', te:'14:00'},
    {id:'q16', subject:'Физика',     teacher:'Орлов С.П.',    date:'2026-06-11', ts:'14:00', te:'15:00'},
    {id:'q17', subject:'География',  teacher:'Волков Д.А.',   date:'2026-06-12', ts:'13:00', te:'14:00'},
    {id:'q18', subject:'Информатика',teacher:'Лебедев А.С.',  date:'2026-06-12', ts:'14:30', te:'15:30'},
    {id:'q19', subject:'Математика', teacher:'Петрова Н.В.',  date:'2026-06-13', ts:'13:00', te:'14:00'},
    {id:'q20', subject:'История',    teacher:'Смирнов А.Б.',  date:'2026-06-13', ts:'14:00', te:'15:00'}
  ],
  schedule: {
    'q1':  {'c1':['Алексеев Артур','Данилов Максим','Жиркова Алина','Иванова Дайаана','Кузьмина Инесса'],
             'c2':['Матвеев Давид','Данилов Константин','Колесов Денис'],
             'c3':['Григорьева Кира','Константинов Марк','Петров Даниил']},
    'q2':  {'c1':['Егоров Айтал','Ксенофонтов Евгений','Созонов Николай'],
             'c2':['Никифоров Айгылаан','Пахомов Владимир','Бойков Андрей','Максимов Лука'],
             'c3':['Аргунова Ильяна','Винтоняк Аристарх','Тимофеев Илсан']},
    'q3':  {'c1':['Петрова Амелия','Степанова Нелли','Федорова Кристина','Захарова Айсаара'],
             'c2':['Антонова Амелия','Федотова Анжелина','Скрыбыкина Анэля'],
             'c3':['Степанова Айыллаана','Стручкова Александра','Христофоров Сандал']},
    'q4':  {'c1':['Вензель Артур','Сметанин Александр','Сыромятникова Валерия'],
             'c2':['Захаров Герман','Иванов Маркел','Уломжинский Арсен'],
             'c3':['Буц Арина','Васильева Сафина','Лаптев Вячеслав','Максимова Айталина']},
    'q5':  {'c1':['Алексеева Валерия','Данилова Нарыйаана','Попова Айыллаана'],
             'c2':['Егоров Лев','Никифорова Моника','Федотова Дайаана'],
             'c3':['Алексеев Андриан','Алексеева Аделина','Колесова Виолетта']},
    'q6':  {'c1':['Алексеев Артур','Жиркова Алина','Кузьмина Инесса','Федоров Сайаан'],
             'c2':['Матвеев Давид','Оленов Арсентий'],
             'c3':['Мамаев-Слепцов Эрхан','Петров Даниил','Григорьева Кира']},
    'q7':  {'c1':['Созонов Николай','Степанова Нелли','Фёдорова Кристина'],
             'c2':['Пахомов Владимир','Скрыбыкина Анэля','Бойков Андрей'],
             'c3':['Алексеева Анастасия','Стручкова Александра']},
    'q8':  {'c1':['Данилов Максим','Егоров Айтал','Иванова Дайаана'],
             'c2':['Захаров Герман','Колесов Денис','Никифоров Айгылаан'],
             'c3':['Аргунова Ильяна','Тимофеев Илсан','Христофоров Сандал']},
    'q9':  {'c1':['Вензель Артур','Захарова Айсаара','Петрова Амелия'],
             'c2':['Антонова Амелия','Данилов Константин','Максимов Лука'],
             'c3':['Константинов Марк','Лаптев Вячеслав']},
    'q10': {'c1':['Сметанин Александр','Сыромятникова Валерия','Ксенофонтов Евгений'],
             'c2':['Иванов Маркел','Федотова Анжелина','Уломжинский Арсен'],
             'c3':['Буц Арина','Максимова Айталина','Степанова Айыллаана']},
    'q11': {'c1':['Алексеева Валерия','Данилова Нарыйаана','Кузьмина Инесса'],
             'c2':['Егоров Лев','Никифорова Моника'],
             'c3':['Алексеев Андриан','Алексеева Аделина','Колесова Виолетта','Васильева Сафина']},
    'q12': {'c1':['Алексеев Артур','Данилов Максим','Жиркова Алина','Иванова Дайаана','Ксенофонтов Евгений','Созонов Николай'],
             'c2':['Матвеев Давид','Данилов Константин','Колесов Денис','Пахомов Владимир'],
             'c3':['Петров Даниил','Григорьева Кира','Тимофеев Илсан']},
    'q13': {'c1':['Егоров Айтал','Петрова Амелия','Степанова Нелли'],
             'c2':['Бойков Андрей','Оленов Арсентий','Скрыбыкина Анэля'],
             'c3':['Аргунова Ильяна','Буц Арина','Мамаев-Слепцов Эрхан']},
    'q14': {'c1':['Вензель Артур','Захарова Айсаара','Федорова Кристина'],
             'c2':['Захаров Герман','Никифоров Айгылаан','Федотова Дайаана'],
             'c3':['Стручкова Александра','Христофоров Сандал']},
    'q15': {'c1':['Алексеева Валерия','Данилов Максим','Созонов Николай','Сыромятникова Валерия'],
             'c2':['Антонова Амелия','Иванов Маркел','Максимов Лука'],
             'c3':['Алексеева Анастасия','Константинов Марк','Лаптев Вячеслав']},
    'q16': {'c1':['Иванова Дайаана','Ксенофонтов Евгений','Кузьмина Инесса'],
             'c2':['Данилов Константин','Никифорова Моника','Уломжинский Арсен'],
             'c3':['Алексеев Андриан','Максимова Айталина','Степанова Айыллаана']},
    'q17': {'c1':['Петрова Амелия','Попова Айыллаана','Федоров Сайаан'],
             'c2':['Бойков Андрей','Егоров Лев','Федотова Анжелина'],
             'c3':['Алексеева Аделина','Колесова Виолетта','Васильева Сафина']},
    'q18': {'c1':['Алексеев Артур','Вензель Артур','Данилова Нарыйаана'],
             'c2':['Захаров Герман','Пахомов Владимир','Скрыбыкина Анэля'],
             'c3':['Буц Арина','Григорьева Кира','Мамаев-Слепцов Эрхан','Петров Даниил']},
    'q19': {'c1':['Данилов Максим','Жиркова Алина','Захарова Айсаара','Иванова Дайаана','Кузьмина Инесса','Ксенофонтов Евгений','Сметанин Александр'],
             'c2':['Колесов Денис','Матвеев Давид','Никифоров Айгылаан','Оленов Арсентий'],
             'c3':['Константинов Марк','Тимофеев Илсан','Христофоров Сандал']},
    'q20': {'c1':['Алексеева Валерия','Петрова Амелия','Степанова Нелли','Фёдорова Кристина'],
             'c2':['Антонова Амелия','Данилов Константин','Иванов Маркел','Федотова Дайаана','Уломжинский Арсен'],
             'c3':['Аргунова Ильяна','Степанова Айыллаана','Стручкова Александра']}
  },
  active: 'c1',
  pendingDelClass: null, pendingDelConsult: null,
  editingConsult: null,
  pickContext: {qid:null},
  calYear: new Date().getFullYear(), calMonth: new Date().getMonth(),
  copyContext: {qid:null},
  copyYear: new Date().getFullYear(), copyMonth: new Date().getMonth(),
  copyDates: []
};

// ===================== SCHEDULE HELPERS =====================
function getAssigned(qid,cid){
  if(!S.schedule[qid]) S.schedule[qid]={};
  if(!S.schedule[qid][cid]) S.schedule[qid][cid]=[];
  return S.schedule[qid][cid];
}
function setAssigned(qid,cid,arr){
  if(!S.schedule[qid]) S.schedule[qid]={};
  S.schedule[qid][cid]=arr;
}

// ===================== CONFLICTS =====================
function timesOverlap(a,b){ return a.id!==b.id&&a.date===b.date&&a.ts<b.te&&a.te>b.ts; }
function conflictingWith(qid){
  var q=S.consults.find(function(x){return x.id===qid;});
  if(!q) return [];
  return S.consults.filter(function(qq){return timesOverlap(q,qq);}).map(function(qq){return qq.id;});
}
function allConflictStudents(){
  var res={};
  S.consults.forEach(function(q){
    var cfs=conflictingWith(q.id);
    if(!cfs.length) return;
    S.classes.forEach(function(c){
      getAssigned(q.id,c.id).forEach(function(name){
        cfs.forEach(function(cqid){
          if(getAssigned(cqid,c.id).indexOf(name)>=0) res[name]=true;
        });
      });
    });
  });
  return res;
}

// ===================== FORMATTING =====================
function e(s){return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;').replace(/'/g,'&#39;');}
var MONTHS=['Январь','Февраль','Март','Апрель','Май','Июнь','Июль','Август','Сентябрь','Октябрь','Ноябрь','Декабрь'];
var DAYS=['Пн','Вт','Ср','Чт','Пт','Сб','Вс'];
function formatDateFull(d){
  if(!d) return '—';
  var p=d.split('-');
  return p[2]+'.'+p[1]+'.'+p[0];
}
function formatDateShort(d){
  if(!d) return '—';
  var p=d.split('-');
  var months=['янв','фев','мар','апр','май','июн','июл','авг','сен','окт','ноя','дек'];
  return p[2]+' '+months[+p[1]-1];
}

// Smart label using SHORT names
function assignLabel(qid,cid){
  var cls=S.classes.find(function(c){return c.id===cid;});
  if(!cls||!cls.students.length) return null;
  var assigned=getAssigned(qid,cid);
  if(!assigned.length) return null;
  var total=cls.students.length;
  var absent=cls.students.filter(function(s){return assigned.indexOf(s)<0;});
  if(absent.length===0) return cls.name+' — Все';
  if(assigned.length/total>=0.7) return cls.name+' — Все, кроме '+absent.map(shortName).join(', ');
  return cls.name+': '+assigned.map(shortName).join(', ');
}

// ===================== RENDER =====================
function renderTabs(){
  var t=document.getElementById('tabs');
  t.innerHTML='';
  S.classes.forEach(function(c){
    var b=document.createElement('button');
    b.className='tab'+(c.id===S.active?' active':'');
    b.textContent=c.name;
    b.onclick=(function(id){return function(){S.active=id;render();};})(c.id);
    t.appendChild(b);
  });
  var a=document.createElement('button');
  a.className='tab dashed';
  a.textContent='+ Класс';
  a.onclick=function(){document.getElementById('f-class-name').value='';openOverlay('m-class',a);setTimeout(function(){document.getElementById('f-class-name').focus();},60);};
  t.appendChild(a);
}

function renderClassPanel(){
  var cls=S.classes.find(function(c){return c.id===S.active;});
  var p=document.getElementById('class-panel');
  if(!cls){p.innerHTML='<span class="ghost">Нет классов</span>';return;}
  var chips=cls.students.length===0
    ?'<span class="ghost">Нет учеников</span>'
    :cls.students.map(function(s){
      return '<span class="chip">'+e(shortName(s))+'<button class="chip-x" onclick="removeStudent(\''+e(cls.id)+'\',\''+e(s)+'\')">×</button></span>';
    }).join('');
  p.innerHTML='<div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:.75rem">'
    +'<div class="sec-title" style="margin:0">Ученики — '+e(cls.name)+' ('+cls.students.length+')</div>'
    +'<button class="btn-red" style="font-size:12px" onclick="askDelClass(\''+e(cls.id)+'\',this)">&#128465; Удалить класс</button>'
    +'</div>'
    +'<div class="chips">'+chips+'</div>'
    +'<div class="row">'
    +'<input id="inp-s" type="text" placeholder="Фамилия Имя" style="flex:1;min-width:140px" onkeydown="if(event.key===\'Enter\')addStudent(\''+e(cls.id)+'\')">'
    +'<button onclick="addStudent(\''+e(cls.id)+'\')">+ Добавить</button>'
    +'</div>';
}

function renderSchedule(){
  var root=document.getElementById('sched-root');
  if(!S.consults.length){root.innerHTML='<p class="ghost">Нет консультаций</p>';return;}
  var sorted=S.consults.slice().sort(function(a,b){
    if(a.date!==b.date) return a.date<b.date?-1:1;
    return a.ts<b.ts?-1:1;
  });
  var dates=[];
  sorted.forEach(function(q){if(dates.indexOf(q.date)<0) dates.push(q.date);});
  var conflictStudents=allConflictStudents();
  var COLS=4;
  var blocks=[];
  for(var i=0;i<dates.length;i+=COLS) blocks.push(dates.slice(i,i+COLS));
  var timeSlots=[];
  sorted.forEach(function(q){
    var key=q.ts+'|'+q.te;
    if(!timeSlots.find(function(t){return t.key===key;})) timeSlots.push({key:key,ts:q.ts,te:q.te});
  });
  var html='';
  blocks.forEach(function(blockDates,bi){
    if(blocks.length>1){
      html+='<div class="sched-block-title">Период '+(bi+1)+': '+formatDateFull(blockDates[0]);
      if(blockDates.length>1) html+=' – '+formatDateFull(blockDates[blockDates.length-1]);
      html+='</div>';
    }
    html+='<div class="grid-wrap"><table class="sched"><thead><tr><th>Время / Предмет / Учитель</th>';
    blockDates.forEach(function(d){
      var dow=DAYS[(new Date(d).getDay()+6)%7];
      html+='<th>'+dow+'<br>'+formatDateFull(d)+'</th>';
    });
    html+='</tr></thead><tbody>';
    timeSlots.forEach(function(slot){
      html+='<tr>';
      var combos=[];
      sorted.filter(function(q){return q.ts===slot.ts&&q.te===slot.te;}).forEach(function(q){
        var key=q.subject+'||'+(q.teacher||'');
        if(!combos.find(function(c){return c.key===key;})) combos.push({key:key,subject:q.subject,teacher:q.teacher});
      });
      var hdr='<div class="slot-label">'+slot.ts+' – '+slot.te+'</div>';
      combos.forEach(function(c){hdr+='<div class="slot-sub">'+e(c.subject)+(c.teacher?' · '+e(c.teacher):'')+'</div>';});
      html+='<td>'+hdr+'</td>';
      blockDates.forEach(function(d){
        var dayQ=sorted.filter(function(q){return q.date===d&&q.ts===slot.ts&&q.te===slot.te;});
        if(!dayQ.length){html+='<td><span class="ghost">—</span></td>';return;}
        html+='<td><div class="cell-inner">';
        dayQ.forEach(function(q){
          var labelsHtml='';
          S.classes.forEach(function(c){
            var lbl=assignLabel(q.id,c.id);
            if(!lbl) return;
            var hasConf=getAssigned(q.id,c.id).some(function(n){return conflictStudents[n];});
            labelsHtml+='<div class="assign-label'+(hasConf?' conflict':'')+'">'+e(lbl)+'</div>';
          });
          html+='<div style="margin-bottom:4px;padding-bottom:4px;border-bottom:1px solid var(--border)">';
          if(dayQ.length>1) html+='<div style="font-size:11px;font-weight:600;color:var(--muted);margin-bottom:2px">'+e(q.subject)+(q.teacher?' · '+e(q.teacher):'')+'</div>';
          html+=labelsHtml||'<span class="ghost" style="font-size:11px">Никто не назначен</span>';
          html+='<div style="display:flex;gap:4px;flex-wrap:wrap;margin-top:3px">'
            +'<button class="btn-assign" onclick="openPickModal(\''+e(q.id)+'\',this)">&#43; Назначить</button>'
            +'<button class="btn-assign" onclick="openCopyModal(\''+e(q.id)+'\',this)">&#128203; Копировать</button>'
            +'<button class="btn-assign" onclick="openConsultModal(\''+e(q.id)+'\',this)">&#9998;</button>'
            +'<button class="btn-assign btn-red" onclick="askDelConsult(\''+e(q.id)+'\',this)">&#128465;</button>'
            +'</div></div>';
        });
        html+='</div></td>';
      });
      html+='</tr>';
    });
    html+='</tbody></table></div><br>';
  });
  root.innerHTML=html;
}

function renderWarn(){
  var cf=allConflictStudents(),names=Object.keys(cf);
  var b=document.getElementById('warn-bar');
  if(!names.length){b.style.display='none';return;}
  b.style.display='block';
  b.innerHTML='⚠️ <strong>Конфликты по времени:</strong> '+names.map(shortName).map(e).join(', ');
}

function render(){renderTabs();renderClassPanel();renderSchedule();renderWarn();}

function openOverlay(id, anchorEl){
  var ov=document.getElementById(id);
  ov.classList.add('open');
  var modal=ov.querySelector('.modal');
  if(!modal) return;
  if(anchorEl){
    var r=anchorEl.getBoundingClientRect();
    var mw=380;
    var mhEst=Math.min(window.innerHeight*0.8, 520);
    // X: align to button left, clamp to viewport
    var left=r.left;
    if(left+mw>window.innerWidth-8) left=window.innerWidth-mw-8;
    if(left<8) left=8;
    // Y: prefer below button, flip above if not enough space
    var top;
    if(r.bottom+6+mhEst<=window.innerHeight){
      top=r.bottom+6;
    } else {
      top=Math.max(8, r.top-mhEst-6);
    }
    modal.style.top=top+'px';
    modal.style.left=left+'px';
    modal.style.transform='none';
  } else {
    modal.style.top=Math.max(8, window.innerHeight/2-200)+'px';
    modal.style.left='50%';
    modal.style.transform='translateX(-50%)';
  }
}
function closeOverlay(id){document.getElementById(id).classList.remove('open');}

// Close overlay when clicking the dark backdrop (not the modal itself)
document.addEventListener('click', function(e){
  document.querySelectorAll('.overlay.open').forEach(function(ov){
    if(e.target === ov) ov.classList.remove('open');
  });
});

// ===================== CALENDAR =====================
function renderCal(){
  var y=S.calYear,m=S.calMonth;
  document.getElementById('cal-month-label').textContent=MONTHS[m]+' '+y;
  document.getElementById('cal-day-names').innerHTML=DAYS.map(function(d){return '<div class="cal-day-name">'+d+'</div>';}).join('');
  var first=new Date(y,m,1).getDay(),offset=(first+6)%7,days=new Date(y,m+1,0).getDate();
  var today=new Date(),sel=document.getElementById('f-date').value,html='';
  for(var i=0;i<offset;i++) html+='<div class="cal-day empty"></div>';
  for(var d=1;d<=days;d++){
    var ds=y+'-'+String(m+1).padStart(2,'0')+'-'+String(d).padStart(2,'0');
    var cls='cal-day';
    if(today.getFullYear()===y&&today.getMonth()===m&&today.getDate()===d) cls+=' today';
    if(sel===ds) cls+=' selected';
    html+='<div class="'+cls+'" onclick="pickCalDate(\''+ds+'\')">'+d+'</div>';
  }
  document.getElementById('cal-days').innerHTML=html;
}
function toggleCal(){var c=document.getElementById('cal');if(c.style.display==='none'){renderCal();c.style.display='block';}else c.style.display='none';}
function calPrev(){if(S.calMonth===0){S.calMonth=11;S.calYear--;}else S.calMonth--;renderCal();}
function calNext(){if(S.calMonth===11){S.calMonth=0;S.calYear++;}else S.calMonth++;renderCal();}
function pickCalDate(d){document.getElementById('f-date').value=d;document.getElementById('f-date-display').value=formatDateFull(d);document.getElementById('cal').style.display='none';}

// ===================== COPY CALENDAR =====================
function renderCopyCal(){
  var y=S.copyYear,m=S.copyMonth;
  document.getElementById('copy-cal-label').textContent=MONTHS[m]+' '+y;
  document.getElementById('copy-cal-names').innerHTML=DAYS.map(function(d){return '<div class="cal-day-name">'+d+'</div>';}).join('');
  var first=new Date(y,m,1).getDay(),offset=(first+6)%7,days=new Date(y,m+1,0).getDate();
  var srcDate=(S.consults.find(function(q){return q.id===S.copyContext.qid;})||{}).date;
  var html='';
  for(var i=0;i<offset;i++) html+='<div class="cal-day empty"></div>';
  for(var d=1;d<=days;d++){
    var ds=y+'-'+String(m+1).padStart(2,'0')+'-'+String(d).padStart(2,'0');
    var cls='cal-day'+(ds===srcDate?' today':'')+(S.copyDates.indexOf(ds)>=0?' selected':'');
    html+='<div class="'+cls+'" onclick="toggleCopyDate(\''+ds+'\')">'+d+'</div>';
  }
  document.getElementById('copy-cal-days').innerHTML=html;
  document.getElementById('copy-selected-list').textContent=S.copyDates.length?S.copyDates.map(formatDateFull).join(', '):'—';
}
function copyCal(dir){S.copyMonth+=dir;if(S.copyMonth<0){S.copyMonth=11;S.copyYear--;}if(S.copyMonth>11){S.copyMonth=0;S.copyYear++;}renderCopyCal();}
function toggleCopyDate(d){var idx=S.copyDates.indexOf(d);if(idx>=0)S.copyDates.splice(idx,1);else S.copyDates.push(d);renderCopyCal();}

// ===================== CONSULT MODAL =====================
function openConsultModal(qid, anchor){
  S.editingConsult=qid||null;
  document.getElementById('m-consult-title').textContent=qid?'Редактировать консультацию':'Новая консультация';
  if(qid){
    var q=S.consults.find(function(x){return x.id===qid;});
    document.getElementById('f-subject').value=q.subject;
    document.getElementById('f-teacher').value=q.teacher||'';
    document.getElementById('f-date').value=q.date;
    document.getElementById('f-date-display').value=formatDateFull(q.date);
    document.getElementById('f-ts').value=q.ts;
    document.getElementById('f-te').value=q.te;
    if(q.date){var p=q.date.split('-');S.calYear=+p[0];S.calMonth=+p[1]-1;}
  } else {
    document.getElementById('f-subject').value='';
    document.getElementById('f-teacher').value='';
    document.getElementById('f-date').value='';
    document.getElementById('f-date-display').value='';
    document.getElementById('f-ts').value='13:00';
    document.getElementById('f-te').value='14:00';
    var now=new Date();S.calYear=now.getFullYear();S.calMonth=now.getMonth();
  }
  document.getElementById('cal').style.display='none';
  openOverlay('m-consult', anchor);
  setTimeout(function(){document.getElementById('f-subject').focus();},60);
}
function saveConsult(){
  var subj=document.getElementById('f-subject').value.trim();
  var teacher=document.getElementById('f-teacher').value.trim();
  var date=document.getElementById('f-date').value;
  var ts=document.getElementById('f-ts').value;
  var te=document.getElementById('f-te').value;
  if(!subj) return;
  if(S.editingConsult){
    var q=S.consults.find(function(x){return x.id===S.editingConsult;});
    if(q){q.subject=subj;q.teacher=teacher;q.date=date;q.ts=ts;q.te=te;}
  } else {
    S.consults.push({id:'q'+Date.now(),subject:subj,teacher:teacher,date:date,ts:ts,te:te});
  }
  closeOverlay('m-consult');render();
}

// ===================== PICK MODAL =====================
function openPickModal(qid, anchor){
  S.pickContext={qid:qid};
  var q=S.consults.find(function(x){return x.id===qid;});
  document.getElementById('m-pick-title').textContent='Назначить учеников';
  document.getElementById('m-pick-sub').textContent=q?q.subject+' · '+formatDateFull(q.date)+' '+q.ts+'–'+q.te:'';
  var html='';
  S.classes.forEach(function(c){
    if(!c.students.length) return;
    var current=getAssigned(qid,c.id);
    html+='<div class="pick-class-header">'
      +'<span>'+e(c.name)+'</span>'
      +'<div style="display:flex;gap:4px">'
      +'<button onclick="pickClass(\''+e(c.id)+'\',true)">Весь '+e(c.name)+'</button>'
      +'<button onclick="pickClass(\''+e(c.id)+'\',false)">Снять</button>'
      +'</div></div>';
    c.students.forEach(function(s){
      var chk=current.indexOf(s)>=0?'checked':'';
      html+='<label class="pick-item"><input type="checkbox" data-cid="'+e(c.id)+'" value="'+e(s)+'" '+chk+'>'+e(shortName(s))+'</label>';
    });
  });
  document.getElementById('pick-list').innerHTML=html;
  openOverlay('m-pick', anchor);
}
function pickClass(cid,val){
  document.querySelectorAll('#pick-list input[data-cid="'+cid+'"]').forEach(function(cb){cb.checked=val;});
}
function pickAll(val){
  document.querySelectorAll('#pick-list input[type=checkbox]').forEach(function(cb){cb.checked=val;});
}
function savePick(){
  var qid=S.pickContext.qid;
  var map={};
  document.querySelectorAll('#pick-list input[type=checkbox]').forEach(function(cb){
    var cid=cb.getAttribute('data-cid');
    if(!map[cid]) map[cid]=[];
    if(cb.checked) map[cid].push(cb.value);
  });
  Object.keys(map).forEach(function(cid){setAssigned(qid,cid,map[cid]);});
  closeOverlay('m-pick');render();
}

// ===================== COPY =====================
function openCopyModal(qid, anchor){
  S.copyContext={qid:qid};S.copyDates=[];
  var q=S.consults.find(function(x){return x.id===qid;});
  document.getElementById('m-copy-sub').textContent=q?q.subject+' · '+formatDateFull(q.date)+' '+q.ts+'–'+q.te:'';
  if(q&&q.date){var p=q.date.split('-');S.copyYear=+p[0];S.copyMonth=+p[1]-1;}
  renderCopyCal();openOverlay('m-copy', anchor);
}
function saveCopy(){
  var src=S.consults.find(function(q){return q.id===S.copyContext.qid;});
  if(!src||!S.copyDates.length){closeOverlay('m-copy');return;}
  S.copyDates.forEach(function(d){
    if(d===src.date) return;
    var newId='q'+Date.now()+Math.random().toString(36).slice(2,5);
    S.consults.push({id:newId,subject:src.subject,teacher:src.teacher,date:d,ts:src.ts,te:src.te});
    S.classes.forEach(function(c){setAssigned(newId,c.id,getAssigned(src.id,c.id).slice());});
  });
  closeOverlay('m-copy');render();
}

// ===================== CLASS MANAGEMENT =====================
function saveClass(){
  var name=document.getElementById('f-class-name').value.trim();
  if(!name) return;
  var id='c'+Date.now();
  S.classes.push({id:id,name:name,students:[]});
  S.active=id;
  closeOverlay('m-class');render();
}
function askDelClass(cid, anchor){
  var cls=S.classes.find(function(c){return c.id===cid;});
  S.pendingDelClass=cid;
  document.getElementById('m-del-class-title').textContent='Удалить класс «'+(cls?cls.name:'')+'»?';
  openOverlay('m-del-class', anchor);
}
function confirmDelClass(){
  var cid=S.pendingDelClass;
  S.classes=S.classes.filter(function(c){return c.id!==cid;});
  Object.keys(S.schedule).forEach(function(qid){if(S.schedule[qid])delete S.schedule[qid][cid];});
  S.active=S.classes[0]?S.classes[0].id:'';
  closeOverlay('m-del-class');render();
}
function askDelConsult(qid, anchor){S.pendingDelConsult=qid;openOverlay('m-del-consult', anchor);}
function confirmDelConsult(){
  var qid=S.pendingDelConsult;
  S.consults=S.consults.filter(function(q){return q.id!==qid;});
  delete S.schedule[qid];
  closeOverlay('m-del-consult');render();
}
function addStudent(cid){
  var inp=document.getElementById('inp-s');
  var raw=inp.value.trim();
  if(!raw) return;
  var cls=S.classes.find(function(c){return c.id===cid;});
  if(!cls) return;
  // Auto-create short if not in lookup
  if(!SHORT[raw]){
    var parts=raw.split(' ');
    SHORT[raw]=parts[0]+(parts[1]?' '+parts[1][0]+'.':'');
  }
  if(cls.students.indexOf(raw)<0){cls.students.push(raw);inp.value='';render();}
}
function removeStudent(cid,name){
  var cls=S.classes.find(function(c){return c.id===cid;});
  if(!cls) return;
  cls.students=cls.students.filter(function(s){return s!==name;});
  Object.keys(S.schedule).forEach(function(qid){
    if(S.schedule[qid]&&S.schedule[qid][cid])
      S.schedule[qid][cid]=S.schedule[qid][cid].filter(function(s){return s!==name;});
  });
  render();
}

// ===================== APPEARANCE =====================
var THEMES = [
  {name:'Синий',    accent:'#3b82f6', bg:'#f0f4ff', card:'#fff', text:'#1a1a2e', muted:'#6b7280', border:'#dde3f0', th:'#eef2ff', tdf:'#f5f8ff', btnBg:'#fff', btnHov:'#eef2ff', inp:'#f8faff'},
  {name:'Зелёный',  accent:'#16a34a', bg:'#f0faf3', card:'#fff', text:'#1a2e1a', muted:'#6b7280', border:'#d1e8d8', th:'#e8f5ec', tdf:'#f5faf6', btnBg:'#fff', btnHov:'#e8f5ec', inp:'#f6fbf7'},
  {name:'Фиолетовый',accent:'#7c3aed',bg:'#f5f0ff', card:'#fff', text:'#1e1a2e', muted:'#6b7280', border:'#ddd5f5', th:'#ede8ff', tdf:'#f8f5ff', btnBg:'#fff', btnHov:'#ede8ff', inp:'#faf8ff'},
  {name:'Тёмный',   accent:'#60a5fa', bg:'#0f172a', card:'#1e293b', text:'#e2e8f0', muted:'#94a3b8', border:'#334155', th:'#1e2d3d', tdf:'#1a2535', btnBg:'#1e293b', btnHov:'#2d3f54', inp:'#1e293b'},
  {name:'Серый',    accent:'#6366f1', bg:'#f4f4f5', card:'#fff', text:'#18181b', muted:'#71717a', border:'#e4e4e7', th:'#f4f4f5', tdf:'#fafafa', btnBg:'#fff', btnHov:'#f4f4f5', inp:'#fafafa'},
  {name:'Тёплый',   accent:'#d97706', bg:'#fdf8ef', card:'#fffcf5', text:'#292015', muted:'#92400e', border:'#e8d9b8', th:'#fdf0d5', tdf:'#fffcf5', btnBg:'#fffcf5', btnHov:'#fdf0d5', inp:'#fffdf8'}
];
var SWATCH_COLORS=['#3b82f6','#16a34a','#7c3aed','#1e293b','#6366f1','#d97706'];
var curTheme=0;

function applyTheme(idx){
  curTheme=idx;
  var t=THEMES[idx];
  var root=document.documentElement;
  var fs=document.getElementById('sel-size')?document.getElementById('sel-size').value:'13';
  var font=document.getElementById('sel-font')?document.getElementById('sel-font').value:'system-ui,-apple-system,sans-serif';
  var radius=document.getElementById('sel-radius')?document.getElementById('sel-radius').value:'8px';
  var css='body{'
    +'font-family:'+font+';'
    +'font-size:'+fs+'px;'
    +'background:'+t.bg+';'
    +'color:'+t.text+';'
    +'--fs:'+fs+'px;'
    +'--accent:'+t.accent+';'
    +'--text:'+t.text+';'
    +'--muted:'+t.muted+';'
    +'--border:'+t.border+';'
    +'--card-bg:'+t.card+';'
    +'--th-bg:'+t.th+';'
    +'--td-first-bg:'+t.tdf+';'
    +'--btn-bg:'+t.btnBg+';'
    +'--btn-hover:'+t.btnHov+';'
    +'--input-bg:'+t.inp+';'
    +'--chip-bg:'+t.tdf+';'
    +'--radius:'+radius+';'
    +'}';
  document.getElementById('theme-style').textContent=css;
  // Update swatches
  document.querySelectorAll('.swatch').forEach(function(sw,i){sw.classList.toggle('active',i===idx);});
}
function applyAppear(){applyTheme(curTheme);}

function initSwatches(){
  var wrap=document.getElementById('swatches');
  THEMES.forEach(function(t,i){
    var d=document.createElement('div');
    d.className='swatch'+(i===curTheme?' active':'');
    d.title=t.name;
    d.style.background=SWATCH_COLORS[i];
    d.onclick=(function(idx){return function(){applyTheme(idx);};})(i);
    wrap.appendChild(d);
  });
}


// ===================== PNG EXPORT =====================
function exportPng(){
  var btn=document.getElementById('btn-export');
  btn.textContent='⏳ Создаю...';
  btn.disabled=true;

  setTimeout(function(){
    try { doExportPng(); }
    catch(err){
      btn.textContent='📷 Поделиться (PNG)';
      btn.disabled=false;
      alert('Ошибка: '+err.message);
    }
  }, 30);
}

function doExportPng(){
  var btn=document.getElementById('btn-export');
  var sorted=S.consults.slice().sort(function(a,b){
    if(a.date!==b.date)return a.date<b.date?-1:1;
    return a.ts<b.ts?-1:1;
  });
  var dates=[];
  sorted.forEach(function(q){if(dates.indexOf(q.date)<0)dates.push(q.date);});
  if(!dates.length){btn.textContent='📷 Поделиться (PNG)';btn.disabled=false;alert('Нет консультаций для экспорта');return;}

  var timeSlots=[];
  sorted.forEach(function(q){
    var key=q.ts+'|'+q.te;
    if(!timeSlots.find(function(t){return t.key===key;}))timeSlots.push({key:key,ts:q.ts,te:q.te});
  });
  var conflictStudents=allConflictStudents();

  var cs=getComputedStyle(document.body);
  var cBg=cs.backgroundColor||'#f4f4f2';
  var cBorder=(cs.getPropertyValue('--border')||'#e0e0e0').trim();
  var cText=(cs.getPropertyValue('--text')||'#1a1a1a').trim();
  var cMuted=(cs.getPropertyValue('--muted')||'#888888').trim();
  var cTh=(cs.getPropertyValue('--th-bg')||'#f7f7f5').trim();
  var cTdF=(cs.getPropertyValue('--td-first-bg')||'#fafaf8').trim();
  var cCard=(cs.getPropertyValue('--card-bg')||'#ffffff').trim();
  var fontSize=parseInt(cs.getPropertyValue('--fs'))||13;
  var fontFam=(document.body.style.fontFamily||'Arial,sans-serif').replace(/"/g,"'");

  var DPR=2, PAD=20, ROWPAD=10, LINE=fontSize+5;
  var COL0=190, COLW=210;
  var numCols=dates.length;
  var totalW=PAD*2+COL0+COLW*numCols;

  // Measure canvas (dummy) for text width
  var dummy=document.createElement('canvas');
  var dctx=dummy.getContext('2d');
  function measureLines(text, maxW, fnt){
    dctx.font=fnt;
    var words=text.split(' ');
    var lines=[], cur='';
    words.forEach(function(w){
      var test=cur?cur+' '+w:w;
      if(dctx.measureText(test).width>maxW-16 && cur){lines.push(cur);cur=w;}
      else cur=test;
    });
    if(cur)lines.push(cur);
    return lines.length?lines:[''];
  }

  // Build cell data: array of {text,color,bold,small}
  function buildCellData(slot, d){
    var dayQ=sorted.filter(function(x){return x.date===d&&x.ts===slot.ts&&x.te===slot.te;});
    if(!dayQ.length)return [{text:'—',color:cMuted,bold:false,small:true}];
    var rows=[];
    dayQ.forEach(function(q, qi){
      if(qi>0) rows.push({text:'',color:cMuted,bold:false,small:false,divider:true});
      if(dayQ.length>1) rows.push({text:q.subject+(q.teacher?' · '+q.teacher:''),color:cMuted,bold:true,small:true});
      var hasAny=false;
      S.classes.forEach(function(c){
        var lbl=assignLabel(q.id,c.id);
        if(!lbl)return;
        hasAny=true;
        var hasConf=getAssigned(q.id,c.id).some(function(n){return conflictStudents[n];});
        rows.push({text:lbl,color:hasConf?'#9a3412':cText,bold:false,small:false});
      });
      if(!hasAny) rows.push({text:'Никто не назначен',color:cMuted,bold:false,small:true});
    });
    return rows;
  }
  function buildHeaderData(slot){
    var rows=[{text:slot.ts+' – '+slot.te,color:cText,bold:true,small:false}];
    var combos=[];
    sorted.filter(function(q){return q.ts===slot.ts&&q.te===slot.te;}).forEach(function(q){
      var key=q.subject+'|'+(q.teacher||'');
      if(!combos.find(function(c){return c.key===key;}))combos.push({key:key,text:q.subject+(q.teacher?' · '+q.teacher:'')});
    });
    combos.forEach(function(c){rows.push({text:c.text,color:cMuted,bold:false,small:true});});
    return rows;
  }

  // Count lines for each row
  function countLines(items, colW){
    var total=0;
    items.forEach(function(item){
      if(item.divider){total+=0.4;return;}
      var fnt=(item.bold?'600 ':'400 ')+(item.small?fontSize-2:fontSize-1)+'px '+fontFam;
      total+=measureLines(item.text,colW,fnt).length;
    });
    return total;
  }

  var HEADER_H=50;
  var rowHeights=timeSlots.map(function(slot){
    var max=countLines(buildHeaderData(slot),COL0);
    dates.forEach(function(d){
      var n=countLines(buildCellData(slot,d),COLW);
      if(n>max)max=n;
    });
    return ROWPAD*2+Math.ceil(max)*LINE+4;
  });

  var totalH=PAD*2+30+HEADER_H+rowHeights.reduce(function(a,b){return a+b;},0)+PAD;

  var canvas=document.createElement('canvas');
  canvas.width=totalW*DPR;
  canvas.height=totalH*DPR;
  var ctx=canvas.getContext('2d');
  ctx.scale(DPR,DPR);

  // BG
  ctx.fillStyle=cBg;ctx.fillRect(0,0,totalW,totalH);
  // Card
  ctx.fillStyle=cCard;
  ctx.beginPath();ctx.roundRect(PAD,PAD,totalW-PAD*2,totalH-PAD*2,10);ctx.fill();

  // Title
  ctx.fillStyle=cText;
  ctx.font='600 15px '+fontFam;
  ctx.fillText('Расписание консультаций',PAD+14,PAD+20);

  var tX=PAD+10, tY=PAD+30;

  // Header row
  drawPngCell(ctx,tX,tY,COL0,HEADER_H,cTh,cBorder);
  ctx.fillStyle=cMuted;ctx.font='500 '+(fontSize-1)+'px '+fontFam;
  ctx.fillText('Время / Предмет / Учитель',tX+8,tY+HEADER_H/2+5);
  dates.forEach(function(d,i){
    var x=tX+COL0+i*COLW;
    drawPngCell(ctx,x,tY,COLW,HEADER_H,cTh,cBorder);
    var dow=DAYS[(new Date(d).getDay()+6)%7];
    ctx.fillStyle=cMuted;ctx.font='600 '+(fontSize-1)+'px '+fontFam;
    ctx.fillText(dow+' '+formatDateFull(d),x+8,tY+HEADER_H/2+5);
  });

  // Data rows
  var rowY=tY+HEADER_H;
  timeSlots.forEach(function(slot,ri){
    var rh=rowHeights[ri];
    // Header cell
    drawPngCell(ctx,tX,rowY,COL0,rh,cTdF,cBorder);
    renderPngItems(ctx,buildHeaderData(slot),tX+8,rowY+ROWPAD,COL0,LINE,fontSize,fontFam);
    // Date cells
    dates.forEach(function(d,ci){
      var x=tX+COL0+ci*COLW;
      drawPngCell(ctx,x,rowY,COLW,rh,cCard,cBorder);
      renderPngItems(ctx,buildCellData(slot,d),x+8,rowY+ROWPAD,COLW,LINE,fontSize,fontFam);
    });
    rowY+=rh;
  });

  btn.textContent='📷 Поделиться (PNG)';
  btn.disabled=false;
  var link=document.createElement('a');
  link.download='расписание_консультаций.png';
  link.href=canvas.toDataURL('image/png');
  link.click();
}

function renderPngItems(ctx,items,x,y,colW,LINE,fontSize,fontFam){
  var curY=y;
  items.forEach(function(item){
    if(item.divider){curY+=Math.round(LINE*0.4);return;}
    var fnt=(item.bold?'600 ':'400 ')+(item.small?fontSize-2:fontSize-1)+'px '+fontFam;
    ctx.font=fnt;
    // word-wrap
    var words=item.text.split(' '), lines=[], cur='';
    words.forEach(function(w){
      var test=cur?cur+' '+w:w;
      if(ctx.measureText(test).width>colW-16 && cur){lines.push(cur);cur=w;}
      else cur=test;
    });
    if(cur)lines.push(cur);
    if(!lines.length)lines=[''];
    lines.forEach(function(line){
      curY+=LINE;
      ctx.fillStyle=item.color;
      ctx.fillText(line,x,curY-3);
    });
  });
}
function drawPngCell(ctx,x,y,w,h,fill,stroke){
  ctx.fillStyle=fill;ctx.fillRect(x,y,w,h);
  ctx.strokeStyle=stroke;ctx.lineWidth=0.5;ctx.strokeRect(x,y,w,h);
}

initSwatches();
applyTheme(0);
render();
</script>
</body>
</html>
