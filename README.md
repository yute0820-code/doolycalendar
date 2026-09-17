<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>👶 우리 아이 출산 행정 캘린더</title>
<style>
  :root{
    --bg:#f6f7fb;
    --card:#ffffff;
    --text:#1f2430;
    --sub:#6b7280;
    --line:#e6e8ee;
    --accent:#4f46e5;
    --green:#16a34a;   --green-bg:#eafbf1;
    --red:#e0382a;     --red-bg:#fdeceb;
    --orange:#e8720c;  --orange-bg:#fdf1e4;
    --yellow:#c8930a;  --yellow-bg:#fdf6e0;
    --purple:#8b3fd1;  --purple-bg:#f6ecfd;
    --blue:#1c6fd9;    --blue-bg:#eaf2fd;
  }
  *{box-sizing:border-box;}
  body{
    margin:0; font-family:-apple-system,BlinkMacSystemFont,"Apple SD Gothic Neo","Malgun Gothic",sans-serif;
    background:var(--bg); color:var(--text); line-height:1.5; padding-bottom:60px;
  }
  .wrap{max-width:720px; margin:0 auto; padding:20px 16px 40px;}
  header{ text-align:center; margin-bottom:20px; }
  header h1{ font-size:22px; margin:0 0 4px; }
  header p{ color:var(--sub); font-size:13px; margin:0; }

  .input-card{
    background:var(--card); border-radius:16px; padding:18px; margin-bottom:18px;
    box-shadow:0 2px 10px rgba(20,20,40,.06); border:1px solid var(--line);
  }
  .input-row{ display:flex; gap:10px; align-items:center; flex-wrap:wrap; }
  .input-row label{ font-size:14px; font-weight:600; color:var(--text); }
  .input-row input[type=date]{
    flex:1; min-width:160px; padding:10px 12px; border-radius:10px; border:1px solid var(--line);
    font-size:15px; font-family:inherit;
  }
  .dday-banner{
    margin-top:14px; text-align:center; padding:14px; border-radius:12px;
    background:linear-gradient(135deg,#4f46e5,#7c3aed); color:#fff;
  }
  .dday-banner .big{ font-size:26px; font-weight:800; }
  .dday-banner .small{ font-size:12px; opacity:.9; margin-top:2px;}

  .now-section{ margin-bottom:22px; }
  .now-section h2{ font-size:15px; margin:0 0 10px; display:flex; align-items:center; gap:6px;}
  .now-empty{ color:var(--sub); font-size:13px; background:var(--card); border:1px dashed var(--line); border-radius:12px; padding:16px; text-align:center;}

  .now-card{
    background:#fff7ed; border:1.5px solid #f5a34a; border-radius:14px; padding:14px 16px; margin-bottom:10px;
  }
  .now-card .ttl{ font-weight:700; font-size:14.5px; margin-bottom:4px; }
  .now-card .meta{ font-size:12.5px; color:#92400e; }

  .timeline{ position:relative; padding-left:22px; }
  .timeline::before{
    content:""; position:absolute; left:6px; top:6px; bottom:6px; width:2px; background:var(--line);
  }
  .item{ position:relative; margin-bottom:14px; }
  .item::before{
    content:""; position:absolute; left:-22px; top:6px; width:12px; height:12px; border-radius:50%;
    border:3px solid var(--card); box-shadow:0 0 0 2px var(--dot-color,#999);
    background:var(--dot-color,#999);
  }
  .card{
    background:var(--card); border:1px solid var(--line); border-radius:14px; padding:14px 16px;
    box-shadow:0 1px 4px rgba(20,20,40,.04);
  }
  .card.done{ opacity:.55; }
  .card-top{ display:flex; justify-content:space-between; align-items:flex-start; gap:8px; margin-bottom:6px;}
  .card-title{ font-size:15px; font-weight:700; display:flex; align-items:center; gap:6px; }
  .badge{
    font-size:11px; font-weight:700; padding:3px 8px; border-radius:20px; white-space:nowrap;
  }
  .card-date{ font-size:12px; color:var(--sub); margin-bottom:8px; }
  .card-meta{ display:flex; gap:14px; font-size:12.5px; color:var(--sub); margin-bottom:8px; flex-wrap:wrap;}
  .card-meta b{ color:var(--text); }
  .star{ color:#e0382a; font-size:13px; }
  .sub-list{ margin-top:8px; border-top:1px dashed var(--line); padding-top:8px; }
  .sub-item{ display:flex; align-items:flex-start; gap:8px; font-size:13.5px; padding:4px 0; cursor:pointer; }
  .sub-item input{ margin-top:3px; flex-shrink:0; width:16px; height:16px; }
  .sub-item.checked span{ text-decoration:line-through; color:var(--sub); }
  .phase-tag{ display:inline-block; font-size:11px; padding:2px 8px; border-radius:8px; font-weight:700; margin-right:6px;}

  .alarms{
    background:var(--card); border:1px solid var(--line); border-radius:16px; padding:16px; margin:26px 0 16px;
  }
  .alarms h2{ font-size:15px; margin:0 0 12px; }
  .alarm-row{ display:flex; justify-content:space-between; align-items:center; padding:8px 0; border-bottom:1px solid var(--line); font-size:13.5px; gap:8px;}
  .alarm-row:last-child{ border-bottom:none; }
  .alarm-row .a-label{ font-weight:600; }
  .alarm-row .a-date{ color:var(--sub); font-size:12.5px; white-space:nowrap; }
  .btn{
    background:var(--accent); color:#fff; border:none; border-radius:10px; padding:11px 16px;
    font-size:14px; font-weight:700; cursor:pointer; width:100%; margin-top:6px;
  }
  .btn:active{ opacity:.85; }
  .note{ font-size:11.5px; color:var(--sub); margin-top:10px; line-height:1.6; }
  .section-title{ font-size:16px; font-weight:800; margin:26px 0 12px; }
  footer{ text-align:center; font-size:11px; color:var(--sub); margin-top:30px; }
</style>
</head>
<body>
<div class="wrap">

  <header>
    <h1>👶 우리 아이 출산 행정 캘린더</h1>
    <p>강릉 거주 · 출산일을 입력하면 신청 시기·장소·금액이 자동 정리돼요</p>
  </header>

  <div class="input-card">
    <div class="input-row">
      <label for="birthDate">출산(예정)일</label>
      <input type="date" id="birthDate">
    </div>
    <div id="ddayBanner" class="dday-banner" style="display:none;">
      <div class="big" id="ddayBig">-</div>
      <div class="small" id="ddaySmall">-</div>
    </div>
  </div>

  <div class="now-section">
    <h2>📌 지금 확인해야 할 일</h2>
    <div id="nowList"></div>
  </div>

  <div class="section-title">🗂️ 전체 타임라인</div>
  <div class="timeline" id="timeline"></div>

  <div class="alarms">
    <h2>🔔 휴대폰에 등록해두면 좋은 알림 7가지</h2>
    <div id="alarmList"></div>
    <button class="btn" id="icsBtn">📅 캘린더 파일(.ics)로 한번에 저장</button>
    <div class="note">다운로드한 파일을 캘린더 앱(구글 캘린더 등)에서 "가져오기" 하면 알림 7개가 한 번에 등록됩니다.</div>
  </div>

  <footer>
    이 페이지의 모든 데이터는 이 브라우저에만 저장됩니다(서버 전송 없음). 제도·금액은 2026년 기준이며 변경될 수 있으니 신청 전 해당 기관 공지를 다시 확인하세요.
  </footer>
</div>

<script>
const $ = (s)=>document.querySelector(s);
const LS_DATE = 'obc_birth_date';
const LS_CHECK = 'obc_checked_items';

function addDays(date, n){ const d = new Date(date); d.setDate(d.getDate()+n); return d; }
function addMonths(date, n){ const d = new Date(date); d.setMonth(d.getMonth()+n); return d; }
function fmt(d){
  const w = ['일','월','화','수','목','금','토'][d.getDay()];
  return `${d.getFullYear()}.${String(d.getMonth()+1).padStart(2,'0')}.${String(d.getDate()).padStart(2,'0')} (${w})`;
}
function fmtShort(d){ return `${d.getMonth()+1}/${d.getDate()}`; }
function ymd(d){ return `${d.getFullYear()}${String(d.getMonth()+1).padStart(2,'0')}${String(d.getDate()).padStart(2,'0')}`; }
function todayMid(){ const t = new Date(); t.setHours(0,0,0,0); return t; }
function ddayLabel(target){
  const t = todayMid(); const tt = new Date(target); tt.setHours(0,0,0,0);
  const diff = Math.round((tt-t)/86400000);
  if(diff===0) return 'D-DAY';
  return diff>0 ? `D-${diff}` : `D+${-diff}`;
}

const COLORS = {
  green:{c:'green',bg:'var(--green-bg)',fg:'var(--green)'},
  red:{c:'red',bg:'var(--red-bg)',fg:'var(--red)'},
  orange:{c:'orange',bg:'var(--orange-bg)',fg:'var(--orange)'},
  yellow:{c:'yellow',bg:'var(--yellow-bg)',fg:'var(--yellow)'},
  purple:{c:'purple',bg:'var(--purple-bg)',fg:'var(--purple)'},
  blue:{c:'blue',bg:'var(--blue-bg)',fg:'var(--blue)'}
};

// day: 특정일(출산일 기준 오프셋), dayRange:[start,end], ageMonths: 아이 나이(개월), ageMonthsRange:[s,e], fixedDate:'YYYY-MM-DD'
function buildItems(birth){
  return [
    { id:'prep', color:'green', star:false, title:'출산 전 준비 체크리스트',
      dayRange:[-40,-1], org:'보건소 · 복지로 · 회사', amount:'-',
      subs:[
        '산모·신생아 건강관리 서비스 신청 (D-40부터 가능, 산후도우미 이용 예정이면 미리)',
        '산후조리원 계약서·결제 영수증 보관',
        '아기 이름 확정',
        '아기 통장·카드 준비',
        '회사에 배우자 출산휴가 일정 확인',
        '아내 회사에 출산휴가 → 육아휴직 일정 확인',
        '남편 2027년 3월 육아휴직 계획 사전 협의 (6+6 부모함께육아휴직제 활용 여부 확인)'
      ]
    },
    { id:'birthday', color:'red', star:false, title:'출산 당일 챙길 것',
      day:0, org:'병원', amount:'-',
      subs:['출생증명서 발급','산모 퇴원 예정일 확인','산후조리원 입실일 확인','산모·신생아 건강관리서비스 이용 여부 확인','회사에 출산 사실 통보']
    },
    { id:'report', color:'orange', star:true, title:'⭐ 출생신고',
      dayRange:[1,7], org:'주소지 행정복지센터 · 온라인', amount:'-',
      subs:['출생신고 완료 (온라인 신고도 가능)']
    },
    { id:'onestop', color:'orange', star:true, title:'⭐ 행복출산 원스톱 신청 (출생신고와 같이!)',
      dayRange:[1,7], org:'행정복지센터 · 정부24', amount:'첫만남 200만+매월 지원',
      subs:[
        '첫만남이용권 200만원 (바우처, 출생일로부터 약 1년 내 사용)',
        '부모급여 월 100만원 (0세)',
        '아동수당 월 10만원 (전국 기준, 강릉시 추가지원 포함 시 10.5만원 수준)',
        '강릉시 출산지원금 30만원',
        '출산가구 전기요금 할인',
        '기타 강릉시 출산 관련 서비스'
      ]
    },
    { id:'paycheck', color:'yellow', star:false, title:'지원금 입금 확인',
      dayRange:[7,30], org:'-', amount:'-',
      subs:['첫만남이용권 200만원 확인','부모급여 100만원 지급 확인','아동수당 지급 확인','강릉시 출산지원금 30만원 확인','전기요금 할인 적용 확인']
    },
    { id:'insurance', color:'yellow', star:false, title:'아기 건강보험 피부양자 등록',
      dayRange:[7,30], org:'국민건강보험공단', amount:'-',
      subs:['아빠 또는 엄마 건강보험에 등록됐는지 확인']
    },
    { id:'paternity', color:'purple', star:false, title:'배우자 출산휴가 20일(유급) 사용',
      dayRange:[25,35], org:'회사', amount:'20일 유급',
      subs:['출산 직후 연속 사용 또는 분할 사용 가능','급여 관련 고용보험 지원 여부 회사에 확인']
    },
    { id:'d60', color:'blue', star:true, title:'⭐ 아동수당·부모급여 소급 신청 마감',
      day:60, org:'행정복지센터', amount:'마감 주의',
      subs:['출생 후 60일 이내 신청해야 출생월부터 소급 지급됨','60일 지나면 신청한 달부터만 지급되어 금액 손해 발생 — 반드시 재확인']
    },
    { id:'helper', color:'green', star:false, title:'산후도우미(산모·신생아 건강관리서비스) 마무리',
      dayRange:[55,70], org:'보건소', amount:'최대 약 20만원',
      subs:['서비스 이용 완료','본인부담금 영수증 보관','서비스 제공기관 확인','강원도 본인부담금 지원 대상 여부 확인']
    },
    { id:'gnpostpartum', color:'orange', star:true, title:'⭐ 강릉시 산후조리비 신청',
      dayRange:[90,180], org:'강릉시 보건소', amount:'최대 50만원',
      subs:['산후조리원·산후조리 관련 영수증 준비','출생일로부터 6개월(180일) 이내 신청 — 놓치면 못 받음']
    },
    { id:'reminder150', color:'orange', star:true, title:'🔔 강릉 산후조리비 신청 마감 임박 알림',
      day:150, org:'-', amount:'-', subs:['아직 신청 전이라면 지금 서두르기']
    },
    { id:'d180', color:'red', star:false, title:'6개월 마감 최종 점검',
      day:180, org:'-', amount:'-',
      subs:['강릉 산후조리비 신청 완료 확인','산모신생아 본인부담금 지원 확인','산후 건강관리 지원 확인','모든 영수증 정리','정부지원금 누락 여부 최종 확인']
    },
    { id:'age12', color:'yellow', star:false, title:'부모급여 감액 · 강원 육아기본수당 시작',
      ageMonths:12, org:'행정복지센터', amount:'부모급여 50만원 + 육아기본수당 50만원',
      subs:['부모급여 0세→1세 전환 (100만원 → 50만원)','강원 육아기본수당 월 50만원 신청','지급계좌 확인','부모급여와 별도 지급되는지 확인']
    },
    { id:'age12to23', color:'green', star:false, title:'매월 확인 (12~23개월 구간)',
      ageMonthsRange:[12,23], org:'-', amount:'월 약 110만원 수준',
      subs:['부모급여 50만원','강원 육아기본수당 50만원','아동수당 약 10~10.5만원','→ 월 현금성 지원 합계 약 110만원 수준']
    },
    { id:'husbandleave', color:'red', star:true, title:'🔥 남편 육아휴직 시작',
      fixedDate:'2027-03-01', org:'회사 · 고용24', amount:'-',
      subs:['회사에 육아휴직 신청','육아휴직 시작일 확인','고용24에서 육아휴직급여 신청','6+6 부모함께육아휴직제 적용 여부 확인']
    },
    { id:'husbandpay', color:'purple', star:false, title:'남편 육아휴직 급여 확인 (6개월)',
      fixedDate:'2027-03-01', org:'고용24', amount:'월 최대 160만~450만원',
      subs:[
        '1~3개월차: 통상임금 100%, 월 최대 250만원',
        '4~6개월차: 월 최대 200만원 (7개월차부터는 80%, 최대 160만원)',
        '6+6 부모육아휴직제 적용 시(부모 모두 사용) 초반 6개월 상한이 단계적으로 올라 최대 월 450만원까지 가능',
        '2025년부터 사후지급금 제도 폐지 — 휴직 중 매달 상한 내 전액 지급 (최신 고용24 공지로 금액 재확인 권장)'
      ]
    },
    { id:'age48', color:'blue', star:false, title:'강원 육아기본수당 월 30만원 구간 확인', ageMonths:48, org:'-', amount:'월 30만원', subs:[] },
    { id:'age72', color:'blue', star:false, title:'강원 육아기본수당 월 10만원 구간 확인 (종료 임박)', ageMonths:72, org:'-', amount:'월 10만원', subs:[] },
  ].map(it=>{
    let start, end, single=false;
    if(it.day!==undefined){ start = addDays(birth, it.day); end = start; single = true; }
    else if(it.dayRange){ start = addDays(birth, it.dayRange[0]); end = addDays(birth, it.dayRange[1]); }
    else if(it.ageMonths!==undefined){ start = addMonths(birth, it.ageMonths); end = start; single = true; }
    else if(it.ageMonthsRange){ start = addMonths(birth, it.ageMonthsRange[0]); end = addMonths(birth, it.ageMonthsRange[1]); }
    else if(it.fixedDate){ start = new Date(it.fixedDate); end = start; single = true; }
    return {...it, start, end, single};
  }).sort((a,b)=>a.start-b.start);
}

function loadChecks(){ try{ return JSON.parse(localStorage.getItem(LS_CHECK)||'{}'); }catch(e){ return {}; } }
function saveChecks(obj){ localStorage.setItem(LS_CHECK, JSON.stringify(obj)); }

function render(){
  const dateVal = $('#birthDate').value;
  if(!dateVal){ $('#ddayBanner').style.display='none'; $('#timeline').innerHTML=''; $('#nowList').innerHTML='<div class="now-empty">먼저 위에서 출산(예정)일을 입력해주세요.</div>'; $('#alarmList').innerHTML=''; return; }
  localStorage.setItem(LS_DATE, dateVal);
  const birth = new Date(dateVal+'T00:00:00');
  const today = todayMid();
  const items = buildItems(birth);
  const checks = loadChecks();

  // 상단 배너
  const diff = Math.round((birth-today)/86400000);
  $('#ddayBanner').style.display='block';
  $('#ddayBig').textContent = diff>0 ? `출산일까지 D-${diff}` : (diff===0 ? '출산 D-DAY 🎉' : `출산 후 D+${-diff}일`);
  $('#ddaySmall').textContent = `기준일: ${fmt(birth)}`;

  // 지금 확인해야 할 일 (오늘이 구간 안에 있거나, 단일일 기준 앞뒤 5일 이내)
  const nowItems = items.filter(it=>{
    if(it.single){ const d = Math.round((it.start-today)/86400000); return d>=-3 && d<=5; }
    return today>=it.start && today<=addDays(it.end,2);
  });
  const nowList = $('#nowList');
  if(nowItems.length===0){
    nowList.innerHTML = '<div class="now-empty">지금 시점에 특별히 처리할 항목은 없어요. 아래 전체 타임라인을 확인해보세요.</div>';
  } else {
    nowList.innerHTML = nowItems.map(it=>{
      const col = COLORS[it.color];
      return `<div class="now-card" style="border-color:${col.fg}22;">
        <div class="ttl">${it.title}</div>
        <div class="meta">${it.single ? fmt(it.start) : fmt(it.start)+' ~ '+fmt(it.end)} · ${it.org}</div>
      </div>`;
    }).join('');
  }

  // 전체 타임라인
  const tl = $('#timeline');
  tl.innerHTML = items.map(it=>{
    const col = COLORS[it.color];
    const isPast = it.single ? today>it.start : today>addDays(it.end,2);
    const dLabel = it.single ? ddayLabel(it.start) : `${ddayLabel(it.start)}~${ddayLabel(it.end)}`;
    const subsHtml = it.subs.map((s,i)=>{
      const key = it.id+'_'+i;
      const checked = !!checks[key];
      return `<label class="sub-item ${checked?'checked':''}" data-key="${key}">
        <input type="checkbox" ${checked?'checked':''}>
        <span>${s}</span>
      </label>`;
    }).join('');
    return `<div class="item" style="--dot-color:${col.fg}">
      <div class="card ${isPast?'done':''}">
        <div class="card-top">
          <div class="card-title">${it.title}</div>
          <div class="badge" style="background:${col.bg};color:${col.fg}">${dLabel}</div>
        </div>
        <div class="card-date">${it.single ? fmt(it.start) : fmt(it.start)+' ~ '+fmt(it.end)}</div>
        <div class="card-meta"><span><b>신청처</b> ${it.org}</span>${it.amount&&it.amount!=='-' ? `<span><b>금액</b> ${it.amount}</span>`:''}</div>
        ${it.subs.length? `<div class="sub-list">${subsHtml}</div>` : ''}
      </div>
    </div>`;
  }).join('');

  tl.querySelectorAll('.sub-item').forEach(el=>{
    el.addEventListener('click', (e)=>{
      const key = el.dataset.key;
      const cur = loadChecks();
      cur[key] = !cur[key];
      saveChecks(cur);
      render();
    });
  });

  // 알림 7가지
  const alarms = [
    { label:'① 산모·신생아 건강관리 신청', date:addDays(birth,-40) },
    { label:'② 출생증명서 받기', date:birth },
    { label:'③ 출생신고 + 행복출산 원스톱', date:addDays(birth,3) },
    { label:'④ 첫만남·부모급여·아동수당·출산지원금 입금 확인', date:addDays(birth,30) },
    { label:'⑤ 아동수당·부모급여 소급 신청 마감 확인', date:addDays(birth,60) },
    { label:'⑥ 강릉 산후조리비 50만원 신청', date:addDays(birth,150) },
    { label:'⑦ 남편 육아휴직 + 6+6 신청 준비', date:new Date('2027-02-01') },
  ];
  $('#alarmList').innerHTML = alarms.map(a=>`
    <div class="alarm-row">
      <span class="a-label">${a.label}</span>
      <span class="a-date">${fmt(a.date)} · ${ddayLabel(a.date)}</span>
    </div>`).join('');

  window.__alarms = alarms;
}

function downloadICS(){
  const alarms = window.__alarms || [];
  if(alarms.length===0){ alert('먼저 출산(예정)일을 입력해주세요.'); return; }
  let ics = 'BEGIN:VCALENDAR\r\nVERSION:2.0\r\nPRODID:-//baby-admin-calendar//KR\r\nCALSCALE:GREGORIAN\r\n';
  alarms.forEach((a,i)=>{
    const d = ymd(a.date);
    const next = ymd(addDays(a.date,1));
    ics += `BEGIN:VEVENT\r\nUID:baby-admin-${i}-${d}@local\r\nDTSTAMP:${d}T090000Z\r\nDTSTART;VALUE=DATE:${d}\r\nDTEND;VALUE=DATE:${next}\r\nSUMMARY:${a.label}\r\nDESCRIPTION:출산 행정 캘린더 자동 알림\r\nEND:VEVENT\r\n`;
  });
  ics += 'END:VCALENDAR\r\n';
  const blob = new Blob([ics], {type:'text/calendar;charset=utf-8'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url; a.download = '출산행정캘린더_알림.ics';
  document.body.appendChild(a); a.click(); document.body.removeChild(a);
  URL.revokeObjectURL(url);
}

$('#birthDate').addEventListener('change', render);
$('#icsBtn').addEventListener('click', downloadICS);

// 초기 로드
const saved = localStorage.getItem(LS_DATE);
if(saved){ $('#birthDate').value = saved; }
render();
</script>
</body>
</html>
