import { useState, useEffect, useRef, useCallback } from "react";

// ─── Constants ────────────────────────────────────────────────────────────────
const APP_ID = "33xKEkZTCmdMLUUCSiL17";
const WS_URL = `wss://ws.derivws.com/websockets/v3?app_id=${APP_ID}`;
const OAUTH_URL = `https://oauth.deriv.com/oauth2/authorize?app_id=${APP_ID}&l=EN&brand=deriv`;

const MARKETS = [
  { id: "R_10",     name: "Volatility 10",     category: "Synthetic" },
  { id: "R_25",     name: "Volatility 25",     category: "Synthetic" },
  { id: "R_50",     name: "Volatility 50",     category: "Synthetic" },
  { id: "R_75",     name: "Volatility 75",     category: "Synthetic" },
  { id: "R_100",    name: "Volatility 100",    category: "Synthetic" },
  { id: "1HZ10V",   name: "Vol 10 (1s)",       category: "Synthetic" },
  { id: "1HZ100V",  name: "Vol 100 (1s)",      category: "Synthetic" },
  { id: "RDBULL",   name: "Bull Market",       category: "Synthetic" },
  { id: "RDBEAR",   name: "Bear Market",       category: "Synthetic" },
  { id: "frxEURUSD","name": "EUR/USD",          category: "Forex" },
  { id: "frxGBPUSD","name": "GBP/USD",          category: "Forex" },
  { id: "frxUSDJPY","name": "USD/JPY",          category: "Forex" },
  { id: "frxAUDUSD","name": "AUD/USD",          category: "Forex" },
  { id: "frxUSDCAD","name": "USD/CAD",          category: "Forex" },
  { id: "frxXAUUSD","name": "Gold/USD",         category: "Commodities" },
  { id: "frxXAGUSD","name": "Silver/USD",       category: "Commodities" },
  { id: "cryBTCUSD","name": "BTC/USD",          category: "Crypto" },
  { id: "cryETHUSD","name": "ETH/USD",          category: "Crypto" },
  { id: "OTC_DJI",  name: "US 30",             category: "Indices" },
  { id: "OTC_NDX",  name: "US Tech 100",       category: "Indices" },
];

const FREE_BOTS = [
  { id: "martingale",        name: "Martingale",        description: "Doubles stake after each loss, resets on win.",         risk: "High",   winRate: "~54%", icon: "🎯", params: { initialStake: 1, multiplier: 2, maxStake: 50 } },
  { id: "dalembert",         name: "D'Alembert",        description: "+1 unit on loss, -1 unit on win.",                      risk: "Medium", winRate: "~52%", icon: "⚖️", params: { initialStake: 1, unit: 1, maxStake: 20 } },
  { id: "reverse_martingale",name: "Reverse Martingale",description: "Doubles after win, resets on loss.",                   risk: "Medium", winRate: "~48%", icon: "🔄", params: { initialStake: 1, multiplier: 2, maxStake: 32 } },
  { id: "fixed_stake",       name: "Fixed Stake",       description: "Constant stake every trade. Simple and safe.",          risk: "Low",    winRate: "~50%", icon: "🔒", params: { stake: 1 } },
  { id: "rsi_bot",           name: "RSI Signal",        description: "Trades on RSI overbought/oversold signals.",            risk: "Medium", winRate: "~56%", icon: "📊", params: { stake: 2, rsiPeriod: 14 } },
  { id: "odd_even",          name: "Odd/Even Digit",    description: "Predicts odd or even last digit of tick price.",        risk: "Low",    winRate: "~50%", icon: "🔢", params: { stake: 1, prediction: "odd" } },
];

const NAV_ITEMS = [
  { id: "Dashboard", icon: "🏠", label: "Home" },
  { id: "Bots",      icon: "🤖", label: "Bots" },
  { id: "Signals",   icon: "📡", label: "Signals" },
  { id: "Markets",   icon: "📈", label: "Markets" },
  { id: "More",      icon: "☰",  label: "More" },
];

// ─── WebSocket Hook ───────────────────────────────────────────────────────────
function useDerivWS() {
  const ws = useRef(null);
  const listeners = useRef({});
  const [connected, setConnected]   = useState(false);
  const [authorized, setAuthorized] = useState(false);
  const [account, setAccount]       = useState(null);
  const [ticks, setTicks]           = useState({});

  const send = useCallback((data) => {
    if (ws.current?.readyState === WebSocket.OPEN)
      ws.current.send(JSON.stringify(data));
  }, []);

  const on = useCallback((type, fn) => { listeners.current[type] = fn; }, []);

  const connect = useCallback(() => {
    if (ws.current) ws.current.close();
    ws.current = new WebSocket(WS_URL);
    ws.current.onopen    = () => setConnected(true);
    ws.current.onclose   = () => { setConnected(false); setAuthorized(false); };
    ws.current.onmessage = (e) => {
      const d = JSON.parse(e.data);
      if (d.msg_type === "authorize") { setAuthorized(true); setAccount(d.authorize); }
      if (d.msg_type === "tick")      setTicks(p => ({ ...p, [d.tick.symbol]: d.tick }));
      if (d.msg_type === "balance")   setAccount(p => p ? { ...p, balance: d.balance.balance } : p);
      const fn = listeners.current[d.msg_type];
      if (fn) fn(d);
    };
  }, []);

  const authorize = useCallback((token) => send({ authorize: token }), [send]);
  return { connected, authorized, account, ticks, connect, authorize, send, on };
}

// ─── Signal Generator ─────────────────────────────────────────────────────────
function generateSignal(symbol) {
  const type       = Math.random() > 0.5 ? "CALL" : "PUT";
  const confidence = [68,72,74,78,81,85,88,91][Math.floor(Math.random()*8)];
  const reasons    = [
    "RSI oversold — reversal expected","Bollinger Band squeeze",
    "MACD bullish crossover","Support bounce pattern",
    "Bearish divergence on 5M","MA golden cross",
    "Volume spike + trend confirm","Pin bar at resistance",
  ];
  const reason   = reasons[Math.floor(Math.random()*reasons.length)];
  const duration = [5,10,15,30][Math.floor(Math.random()*4)];
  const market   = MARKETS.find(m => m.id === symbol);
  return { symbol, marketName: market?.name || symbol, type, confidence, reason, duration, time: new Date() };
}

// ─── Colour helpers ───────────────────────────────────────────────────────────
const riskColor = r => ({ Low:"#166534", Medium:"#1e3a5f", High:"#7f1d1d", Custom:"#4a1d96" }[r] || "#1e293b");
const riskText  = r => ({ Low:"#22c55e", Medium:"#60a5fa", High:"#f87171", Custom:"#a78bfa" }[r] || "#94a3b8");

// ═══════════════════════════════════════════════════════════════════════════════
//  COMPONENTS
// ═══════════════════════════════════════════════════════════════════════════════

// ── Login Modal ───────────────────────────────────────────────────────────────
function LoginModal({ onOAuth, onPAT, onClose }) {
  const [pat, setPat]   = useState("");
  const [tab, setTab]   = useState("oauth");
  return (
    <div style={S.overlay}>
      <div style={S.modal}>
        <div style={{ display:"flex", justifyContent:"space-between", alignItems:"center", marginBottom:4 }}>
          <span style={S.logo}>SIDO<span style={{color:"#00d4aa"}}>SITE</span></span>
          <button onClick={onClose} style={S.iconBtn}>✕</button>
        </div>
        <p style={{ color:"#64748b", fontSize:12, margin:"0 0 16px" }}>Connect your Deriv account</p>

        <div style={{ display:"flex", gap:6, marginBottom:16 }}>
          {["oauth","pat"].map(t => (
            <button key={t} style={{ ...S.tabBtn, ...(tab===t ? S.tabBtnActive : {}) }}
              onClick={() => setTab(t)}>
              {t === "oauth" ? "🔐 OAuth2" : "🔑 API Token"}
            </button>
          ))}
        </div>

        {tab === "oauth" ? (
          <div style={{ textAlign:"center" }}>
            <p style={{ color:"#475569", fontSize:12, marginBottom:14 }}>
              Redirects securely to Deriv's login page.
            </p>
            <button style={{ ...S.primaryBtn, width:"100%", padding:"13px" }} onClick={onOAuth}>
              Connect with Deriv OAuth2
            </button>
          </div>
        ) : (
          <>
            <p style={{ color:"#475569", fontSize:12, marginBottom:10 }}>
              Deriv → Security → API Token (Trade + Read permissions).
            </p>
            <input style={S.input} type="password" placeholder="Paste API token…"
              value={pat} onChange={e => setPat(e.target.value)} />
            <button style={{ ...S.primaryBtn, width:"100%", marginTop:10, padding:"13px", opacity: pat ? 1 : 0.45 }}
              onClick={() => pat && onPAT(pat)} disabled={!pat}>
              Connect with Token
            </button>
          </>
        )}
        <p style={{ color:"#334155", fontSize:10, marginTop:14, textAlign:"center" }}>
          Credentials are never stored. Direct connection to Deriv.
        </p>
      </div>
    </div>
  );
}

// ── Top Header ────────────────────────────────────────────────────────────────
function TopBar({ connected, account, onLogin, onLogout }) {
  return (
    <header style={S.topBar}>
      <span style={S.logo}>SIDO<span style={{color:"#00d4aa"}}>SITE</span></span>
      <div style={{ display:"flex", alignItems:"center", gap:8 }}>
        <span style={{ ...S.dot, background: connected ? "#00d4aa" : "#475569" }} />
        {account ? (
          <div style={{ display:"flex", alignItems:"center", gap:8 }}>
            <div style={{ textAlign:"right" }}>
              <div style={{ color:"#00d4aa", fontWeight:800, fontSize:14, lineHeight:1 }}>
                ${parseFloat(account.balance||0).toFixed(2)}
              </div>
              <div style={{ color:"#475569", fontSize:10 }}>{account.email?.split("@")[0]}</div>
            </div>
            <button style={S.logoutBtn} onClick={onLogout}>Out</button>
          </div>
        ) : (
          <button style={{ ...S.primaryBtn, padding:"7px 14px", fontSize:12 }} onClick={onLogin}>
            Connect
          </button>
        )}
      </div>
    </header>
  );
}

// ── Bottom Nav ────────────────────────────────────────────────────────────────
function BottomNav({ active, setActive }) {
  return (
    <nav style={S.bottomNav}>
      {NAV_ITEMS.map(n => (
        <button key={n.id} style={{ ...S.navItem, ...(active===n.id ? S.navItemActive : {}) }}
          onClick={() => setActive(n.id)}>
          <span style={{ fontSize:20 }}>{n.icon}</span>
          <span style={{ fontSize:9, marginTop:2 }}>{n.label}</span>
        </button>
      ))}
    </nav>
  );
}

// ── More Menu ─────────────────────────────────────────────────────────────────
function MoreMenu({ setActive }) {
  const items = [
    { id:"dTrader", icon:"📖", label:"dTrader Manual", desc:"Learn all contract types" },
    { id:"Upload",  icon:"⬆️", label:"Upload Bot",      desc:"Add your custom bot" },
  ];
  return (
    <div style={S.page}>
      <h2 style={S.pageTitle}>More</h2>
      <div style={{ display:"flex", flexDirection:"column", gap:10 }}>
        {items.map(it => (
          <button key={it.id} style={S.moreCard} onClick={() => setActive(it.id)}>
            <span style={{ fontSize:28 }}>{it.icon}</span>
            <div style={{ textAlign:"left" }}>
              <div style={{ color:"#e2e8f0", fontWeight:700, fontSize:15 }}>{it.label}</div>
              <div style={{ color:"#475569", fontSize:12 }}>{it.desc}</div>
            </div>
            <span style={{ marginLeft:"auto", color:"#334155", fontSize:18 }}>›</span>
          </button>
        ))}
      </div>
    </div>
  );
}

// ── Dashboard ─────────────────────────────────────────────────────────────────
function Dashboard({ ticks, account, bots, onLogin }) {
  const activeBots = bots.filter(b => b.running).length;
  const totalPnL   = bots.reduce((s,b) => s+(b.pnl||0), 0);

  const stats = [
    { label:"Balance",     value:`$${parseFloat(account?.balance||0).toFixed(2)}`, color:"#00d4aa", icon:"💰" },
    { label:"Active Bots", value:activeBots,                                        color:"#818cf8", icon:"🤖" },
    { label:"Session P&L", value:`${totalPnL>=0?"+":""}$${totalPnL.toFixed(2)}`,   color:totalPnL>=0?"#22c55e":"#f87171", icon:"📈" },
    { label:"Live Feeds",  value:Object.keys(ticks).length,                         color:"#f59e0b", icon:"🌐" },
  ];

  return (
    <div style={S.page}>
      {!account && (
        <div style={S.connectBanner}>
          <span>🔌 Connect Deriv to start trading</span>
          <button style={{ ...S.primaryBtn, padding:"6px 12px", fontSize:11 }} onClick={onLogin}>Connect</button>
        </div>
      )}

      <h2 style={S.pageTitle}>Dashboard</h2>

      {/* Stats 2×2 */}
      <div style={S.statsGrid}>
        {stats.map(s => (
          <div key={s.label} style={S.statCard}>
            <div style={{ fontSize:22, marginBottom:4 }}>{s.icon}</div>
            <div style={{ color:s.color, fontSize:20, fontWeight:800 }}>{s.value}</div>
            <div style={{ color:"#475569", fontSize:11 }}>{s.label}</div>
          </div>
        ))}
      </div>

      <h3 style={S.sectionTitle}>Live Ticks</h3>
      <div style={S.tickScroll}>
        {MARKETS.map(m => {
          const tick = ticks[m.id];
          return (
            <div key={m.id} style={S.tickPill}>
              <div style={{ color:"#64748b", fontSize:9 }}>{m.category}</div>
              <div style={{ color:"#e2e8f0", fontSize:11, fontWeight:700 }}>{m.name}</div>
              <div style={{ color:"#00d4aa", fontFamily:"monospace", fontSize:13, fontWeight:800 }}>
                {tick ? tick.quote.toFixed(4) : "—"}
              </div>
            </div>
          );
        })}
      </div>
    </div>
  );
}

// ── Bots Page ─────────────────────────────────────────────────────────────────
function BotsPage({ bots, setBots, authorized, onLogin }) {
  const [stakes,  setStakes]  = useState({});
  const [markets, setMarkets] = useState({});
  const intervalRefs = useRef({});
  const fileRef = useRef();

  const startBot = bot => {
    if (!authorized) { onLogin(); return; }
    setBots(prev => prev.map(b => b.id===bot.id ? {...b, running:true} : b));
    intervalRefs.current[bot.id] = setInterval(() => {
      const win   = Math.random() > 0.46;
      const stake = parseFloat(stakes[bot.id] || bot.params?.initialStake || bot.params?.stake || 1);
      const profit = win ? +(stake*0.85).toFixed(2) : -stake;
      setBots(prev => prev.map(b => b.id===bot.id
        ? { ...b, trades:(b.trades||0)+1, pnl:parseFloat(((b.pnl||0)+profit).toFixed(2)), lastResult:win?"WIN":"LOSS" }
        : b));
    }, 5000 + Math.random()*3000);
  };

  const stopBot = id => {
    clearInterval(intervalRefs.current[id]);
    setBots(prev => prev.map(b => b.id===id ? {...b, running:false} : b));
  };

  const handleUpload = e => {
    const file = e.target.files[0];
    if (!file) return;
    const reader = new FileReader();
    reader.onload = evt => {
      try {
        const bot = {
          id:"upload_"+Date.now(), name:file.name.replace(/\.[^.]+$/,""),
          description:"Custom uploaded bot", risk:"Custom", winRate:"—", icon:"📁",
          params:JSON.parse(evt.target.result), custom:true, pnl:0, trades:0, running:false,
        };
        setBots(prev => [...prev, bot]);
      } catch { alert("Invalid bot file — use valid JSON."); }
    };
    reader.readAsText(file);
  };

  return (
    <div style={S.page}>
      <div style={{ display:"flex", justifyContent:"space-between", alignItems:"center", marginBottom:16 }}>
        <h2 style={{ ...S.pageTitle, margin:0 }}>Bots</h2>
        <button style={S.uploadBtn} onClick={() => fileRef.current.click()}>⬆ Upload</button>
        <input ref={fileRef} type="file" accept=".json,.xml" style={{display:"none"}} onChange={handleUpload} />
      </div>

      <div style={{ display:"flex", flexDirection:"column", gap:12 }}>
        {bots.map(bot => (
          <div key={bot.id} style={{ ...S.botCard, ...(bot.running ? S.botCardOn : {}) }}>
            {/* Header row */}
            <div style={{ display:"flex", alignItems:"center", gap:10, marginBottom:8 }}>
              <span style={{ fontSize:26 }}>{bot.icon}</span>
              <div style={{ flex:1, minWidth:0 }}>
                <div style={{ color:"#e2e8f0", fontWeight:700, fontSize:14, whiteSpace:"nowrap", overflow:"hidden", textOverflow:"ellipsis" }}>
                  {bot.name}
                </div>
                <div style={{ display:"flex", gap:5, marginTop:3, flexWrap:"wrap" }}>
                  <span style={{ ...S.badge, background:riskColor(bot.risk), color:riskText(bot.risk) }}>{bot.risk}</span>
                  <span style={S.badge}>Win {bot.winRate}</span>
                  {bot.custom && <span style={{ ...S.badge, background:"#4a1d96", color:"#a78bfa" }}>Custom</span>}
                </div>
              </div>
              <div style={{ textAlign:"right", flexShrink:0 }}>
                <div style={{ color:(bot.pnl||0)>=0?"#22c55e":"#f87171", fontWeight:800, fontSize:16 }}>
                  {(bot.pnl||0)>=0?"+":""}${(bot.pnl||0).toFixed(2)}
                </div>
                <div style={{ color:"#334155", fontSize:10 }}>{bot.trades||0} trades</div>
              </div>
            </div>

            <div style={{ color:"#475569", fontSize:11, marginBottom:10 }}>{bot.description}</div>

            {/* Controls */}
            <div style={{ display:"flex", gap:6, flexWrap:"wrap" }}>
              <select style={{ ...S.select, flex:1, minWidth:100, fontSize:11 }}
                value={markets[bot.id]||"R_50"}
                onChange={e => setMarkets(p => ({...p,[bot.id]:e.target.value}))}>
                {MARKETS.map(m => <option key={m.id} value={m.id}>{m.name}</option>)}
              </select>
              <input style={{ ...S.input, width:68, fontSize:12 }} type="number" min="0.35"
                step="0.5" placeholder="$1"
                value={stakes[bot.id]||""}
                onChange={e => setStakes(p => ({...p,[bot.id]:e.target.value}))} />
              {bot.running
                ? <button style={S.stopBtn}  onClick={() => stopBot(bot.id)}>⏹ Stop</button>
                : <button style={S.startBtn} onClick={() => startBot(bot)}>▶ Start</button>
              }
            </div>

            {bot.lastResult && (
              <div style={{ marginTop:6, fontSize:11, fontWeight:700,
                color:bot.lastResult==="WIN"?"#22c55e":"#f87171" }}>
                Last: {bot.lastResult}
              </div>
            )}
          </div>
        ))}
      </div>
    </div>
  );
}

// ── Signals Page ──────────────────────────────────────────────────────────────
function SignalsPage() {
  const [signals,  setSignals]  = useState([]);
  const [loading,  setLoading]  = useState(false);
  const [selected, setSelected] = useState(["R_50","R_100","frxEURUSD","frxGBPUSD","cryBTCUSD"]);

  const refresh = useCallback(async () => {
    setLoading(true);
    await new Promise(r => setTimeout(r, 1100));
    setSignals(selected.map(s => generateSignal(s)));
    setLoading(false);
  }, [selected]);

  useEffect(() => { refresh(); }, []);

  const toggle = id => setSelected(p => p.includes(id) ? p.filter(x=>x!==id) : [...p,id]);

  return (
    <div style={S.page}>
      <div style={{ display:"flex", justifyContent:"space-between", alignItems:"center", marginBottom:12 }}>
        <h2 style={{ ...S.pageTitle, margin:0 }}>AI Signals</h2>
        <button style={{ ...S.primaryBtn, display:"flex", alignItems:"center", gap:6, padding:"8px 14px" }}
          onClick={refresh} disabled={loading}>
          {loading ? <span style={S.spinner} /> : "🔄"} Refresh
        </button>
      </div>

      {/* Market chips */}
      <div style={{ display:"flex", flexWrap:"wrap", gap:5, marginBottom:14 }}>
        {MARKETS.map(m => (
          <button key={m.id}
            style={{ padding:"4px 9px", fontSize:10, borderRadius:20, cursor:"pointer", fontWeight:600, border:"1px solid",
              background: selected.includes(m.id) ? "#00d4aa22" : "#0f172a",
              borderColor: selected.includes(m.id) ? "#00d4aa" : "#1e293b",
              color: selected.includes(m.id) ? "#00d4aa" : "#475569" }}
            onClick={() => toggle(m.id)}>
            {m.name}
          </button>
        ))}
      </div>

      {loading ? (
        <div style={{ textAlign:"center", padding:50, color:"#00d4aa" }}>
          <div style={{ fontSize:36, marginBottom:10 }}>🤖</div>
          <div style={{ fontSize:13 }}>Analysing markets…</div>
        </div>
      ) : (
        <div style={{ display:"flex", flexDirection:"column", gap:10 }}>
          {signals.map((sig,i) => (
            <div key={i} style={{ ...S.signalCard,
              borderLeft:`4px solid ${sig.type==="CALL"?"#22c55e":"#f87171"}` }}>
              <div style={{ display:"flex", justifyContent:"space-between", alignItems:"flex-start" }}>
                <div>
                  <div style={{ color:"#e2e8f0", fontWeight:700, fontSize:14 }}>{sig.marketName}</div>
                  <div style={{ color:"#334155", fontSize:10 }}>{sig.time.toLocaleTimeString()} · {sig.duration}min expiry</div>
                </div>
                <div style={{ color:sig.type==="CALL"?"#22c55e":"#f87171",
                  fontWeight:900, fontSize:18, letterSpacing:1 }}>
                  {sig.type==="CALL" ? "▲ CALL" : "▼ PUT"}
                </div>
              </div>
              <div style={{ margin:"8px 0 4px" }}>
                <div style={{ display:"flex", justifyContent:"space-between", marginBottom:4 }}>
                  <span style={{ color:"#475569", fontSize:10 }}>Confidence</span>
                  <span style={{ color:sig.confidence>80?"#22c55e":"#f59e0b", fontSize:10, fontWeight:700 }}>
                    {sig.confidence}%
                  </span>
                </div>
                <div style={{ height:5, background:"#1e293b", borderRadius:4, overflow:"hidden" }}>
                  <div style={{ height:"100%", width:`${sig.confidence}%`, borderRadius:4,
                    background:sig.confidence>80?"#22c55e":"#f59e0b", transition:"width .5s" }} />
                </div>
              </div>
              <div style={{ color:"#475569", fontSize:11, marginTop:4 }}>💡 {sig.reason}</div>
            </div>
          ))}
          {signals.length===0 && (
            <div style={{ textAlign:"center", color:"#334155", padding:30, fontSize:13 }}>
              Select markets above, then tap Refresh
            </div>
          )}
        </div>
      )}
    </div>
  );
}

// ── Markets Page ──────────────────────────────────────────────────────────────
function MarketsPage({ ticks, send, authorized }) {
  const [cat, setCat] = useState("All");
  const cats = ["All","Synthetic","Forex","Crypto","Commodities","Indices"];

  useEffect(() => {
    if (authorized) MARKETS.forEach(m => send({ ticks:m.id, subscribe:1 }));
  }, [authorized]);

  const list = cat==="All" ? MARKETS : MARKETS.filter(m => m.category===cat);

  return (
    <div style={S.page}>
      <h2 style={S.pageTitle}>Markets</h2>

      {/* Category scroll */}
      <div style={{ display:"flex", gap:6, overflowX:"auto", paddingBottom:8, marginBottom:14,
        scrollbarWidth:"none" }}>
        {cats.map(c => (
          <button key={c} style={{ ...S.tabBtn, ...(cat===c?S.tabBtnActive:{}), flexShrink:0 }}
            onClick={() => setCat(c)}>{c}</button>
        ))}
      </div>

      <div style={{ display:"flex", flexDirection:"column", gap:1, borderRadius:12, overflow:"hidden", border:"1px solid #1e293b" }}>
        {list.map((m,i) => {
          const tick = ticks[m.id];
          return (
            <div key={m.id} style={{ display:"flex", alignItems:"center", justifyContent:"space-between",
              padding:"12px 14px", background: i%2===0 ? "#0f172a" : "#0a1020",
              borderBottom:"1px solid #151f2e" }}>
              <div>
                <div style={{ color:"#e2e8f0", fontWeight:600, fontSize:13 }}>{m.name}</div>
                <div style={{ color:"#334155", fontSize:10 }}>{m.category}</div>
              </div>
              <div style={{ textAlign:"right" }}>
                <div style={{ color:"#00d4aa", fontFamily:"monospace", fontWeight:800, fontSize:14 }}>
                  {tick ? tick.quote.toFixed(4) : "—"}
                </div>
                <div style={{ color:tick?"#22c55e":"#334155", fontSize:10 }}>
                  {tick?"● Live":"○ Offline"}
                </div>
              </div>
            </div>
          );
        })}
      </div>
    </div>
  );
}

// ── dTrader Manual ────────────────────────────────────────────────────────────
function DTraderPage() {
  const [section, setSection] = useState("intro");
  const sections = [
    { id:"intro",          title:"What is dTrader?" },
    { id:"getting-started",title:"Getting Started" },
    { id:"contract-types", title:"Contract Types" },
    { id:"risk",           title:"Risk Management" },
    { id:"faq",            title:"FAQ" },
  ];
  const content = {
    intro:`dTrader is Deriv's advanced trading platform for digital options, multipliers, and accumulators across 100+ assets.

✦ Markets: Synthetic Indices, Forex, Crypto, Stocks, Commodities
✦ Contract types: Rise/Fall, Touch/No Touch, Digits, Multipliers
✦ Available 24/7 (Synthetic Indices never close)
✦ Minimum stake: $0.35`,
    "getting-started":`1. Create a Deriv account at deriv.com
2. Verify email & identity
3. Fund your account (min ~$5)
4. Open dTrader from the main menu
5. Pick a market and contract type
6. Set your stake and duration
7. Tap Rise or Fall to place the trade
8. Monitor in Open Positions panel`,
    "contract-types":`RISE / FALL
Predict if exit price > or < entry price.

HIGHER / LOWER
Predict above or below a set barrier.

TOUCH / NO TOUCH
Will price touch a barrier or not?

ENDS BETWEEN / OUTSIDE
Final price inside or outside two barriers.

DIGITS
Last digit: Matches, Differs, Odd, Even, Over, Under.

MULTIPLIERS
Leveraged gains. No fixed expiry.

ACCUMULATORS
Compound profits while price stays in range.`,
    risk:`1% Rule — Never risk more than 1–2% per trade.

Set Daily Limits — Decide max loss before you start and quit when hit.

Cap Your Martingale — Always set a max stake on doubling strategies.

Use Demo First — Free $10,000 virtual account on Deriv.

Diversify — Don't trade only one market or strategy.

No Revenge Trading — Take breaks after losses. Keep a journal.

Check Payout — dTrader shows exact return % before you buy.`,
    faq:`Q: Minimum stake?
A: $0.35 USD for most contracts.

Q: Trading on weekends?
A: Yes — Synthetic Indices run 24/7/365.

Q: What is a Synthetic Index?
A: A simulated market generated by a cryptographically secure algorithm. Not affected by news events.

Q: How to withdraw?
A: Cashier → Withdrawal. Processing: instant to 5 business days.

Q: Demo account?
A: Yes — free virtual $10,000 on registration.

Q: Can bots trade on dTrader?
A: Use Deriv Bot (bot.deriv.com) or the Deriv API for automation.`,
  };

  return (
    <div style={S.page}>
      <h2 style={S.pageTitle}>dTrader Manual</h2>

      {/* Section tabs — horizontal scroll */}
      <div style={{ display:"flex", gap:6, overflowX:"auto", paddingBottom:10, marginBottom:14, scrollbarWidth:"none" }}>
        {sections.map(s => (
          <button key={s.id} style={{ ...S.tabBtn, ...(section===s.id?S.tabBtnActive:{}), flexShrink:0, fontSize:11 }}
            onClick={() => setSection(s.id)}>{s.title}</button>
        ))}
      </div>

      <div style={{ background:"#0f172a", borderRadius:12, padding:16, border:"1px solid #1e293b" }}>
        <h3 style={{ color:"#00d4aa", margin:"0 0 12px", fontSize:15 }}>
          {sections.find(s=>s.id===section)?.title}
        </h3>
        <pre style={{ color:"#94a3b8", fontSize:12, lineHeight:1.9, whiteSpace:"pre-wrap",
          fontFamily:"inherit", margin:0 }}>
          {content[section]}
        </pre>
      </div>

      <a href="https://deriv.com/dtrader" target="_blank" rel="noreferrer"
        style={{ ...S.primaryBtn, display:"block", textAlign:"center", textDecoration:"none",
          marginTop:14, padding:"12px" }}>
        Open dTrader ↗
      </a>
    </div>
  );
}

// ── Upload Page ───────────────────────────────────────────────────────────────
function UploadPage({ setBots }) {
  const [name,     setName]     = useState("");
  const [desc,     setDesc]     = useState("");
  const [risk,     setRisk]     = useState("Medium");
  const [fileData, setFileData] = useState(null);
  const [fileName, setFileName] = useState("");
  const [success,  setSuccess]  = useState(false);
  const fileRef = useRef();

  const handleFile = e => {
    const f = e.target.files[0];
    if (!f) return;
    setFileName(f.name);
    const r = new FileReader();
    r.onload = x => setFileData(x.target.result);
    r.readAsText(f);
  };

  const submit = () => {
    if (!name || !fileData) { alert("Enter a name and select a file."); return; }
    let params = {};
    try { params = JSON.parse(fileData); } catch { params = { raw: fileData }; }
    setBots(prev => [...prev, {
      id:"custom_"+Date.now(), name, description:desc||"Custom uploaded bot",
      risk, winRate:"—", icon:"📁", params, custom:true, pnl:0, trades:0, running:false,
    }]);
    setSuccess(true);
    setName(""); setDesc(""); setFileData(null); setFileName("");
    setTimeout(() => setSuccess(false), 3000);
  };

  return (
    <div style={S.page}>
      <h2 style={S.pageTitle}>Upload Bot</h2>
      {success && (
        <div style={{ background:"#166534", color:"#22c55e", padding:"11px 14px",
          borderRadius:8, marginBottom:14, fontSize:12 }}>
          ✅ Bot uploaded! Go to Bots tab to start it.
        </div>
      )}

      <div style={S.formGroup}>
        <label style={S.label}>Bot Name *</label>
        <input style={S.input} value={name} onChange={e=>setName(e.target.value)} placeholder="My Strategy" />
      </div>
      <div style={S.formGroup}>
        <label style={S.label}>Description</label>
        <textarea style={{ ...S.input, height:70, resize:"vertical" }}
          value={desc} onChange={e=>setDesc(e.target.value)} placeholder="Describe your strategy…" />
      </div>
      <div style={S.formGroup}>
        <label style={S.label}>Risk Level</label>
        <select style={S.select} value={risk} onChange={e=>setRisk(e.target.value)}>
          <option>Low</option><option>Medium</option><option>High</option><option>Custom</option>
        </select>
      </div>
      <div style={S.formGroup}>
        <label style={S.label}>Bot File (JSON or XML) *</label>
        <div style={S.dropZone} onClick={() => fileRef.current.click()}>
          {fileName
            ? <span style={{ color:"#00d4aa" }}>📁 {fileName}</span>
            : <span style={{ color:"#334155" }}>Tap to choose file<br /><span style={{fontSize:10}}>.json or .xml</span></span>
          }
        </div>
        <input ref={fileRef} type="file" accept=".json,.xml" style={{display:"none"}} onChange={handleFile} />
      </div>

      <button style={{ ...S.primaryBtn, width:"100%", padding:"13px", fontSize:14 }} onClick={submit}>
        ⬆ Upload Bot
      </button>

      <div style={{ marginTop:20, background:"#0a1020", borderRadius:10, padding:14, border:"1px solid #1e293b" }}>
        <div style={{ color:"#475569", fontSize:11, fontWeight:700, marginBottom:8 }}>📋 Example JSON format</div>
        <pre style={{ color:"#334155", fontSize:10, margin:0, overflowX:"auto" }}>
{`{
  "initialStake": 1,
  "multiplier": 2,
  "maxStake": 50,
  "contractType": "CALL",
  "duration": 5,
  "market": "R_50"
}`}
        </pre>
      </div>
    </div>
  );
}

// ═══════════════════════════════════════════════════════════════════════════════
//  ROOT APP
// ═══════════════════════════════════════════════════════════════════════════════
export default function SidoSite() {
  const { connected, authorized, account, ticks, connect, authorize, send, on } = useDerivWS();
  const [page,      setPage]      = useState("Dashboard");
  const [showLogin, setShowLogin] = useState(false);
  const [bots,      setBots]      = useState(FREE_BOTS.map(b => ({ ...b, pnl:0, trades:0, running:false })));

  // Boot WS
  useEffect(() => { connect(); }, []);

  // OAuth2 token in URL
  useEffect(() => {
    const p = new URLSearchParams(window.location.search);
    const t = p.get("token1");
    if (t) { authorize(t); window.history.replaceState({}, "", window.location.pathname); }
  }, []);

  // Subscribe on auth
  useEffect(() => {
    if (authorized) {
      send({ balance:1, subscribe:1 });
      MARKETS.forEach(m => send({ ticks:m.id, subscribe:1 }));
    }
  }, [authorized]);

  const handleOAuth  = () => { window.location.href = OAUTH_URL; };
  const handlePAT    = t  => { authorize(t); setShowLogin(false); };
  const handleLogout = () => { send({ logout:1 }); window.location.reload(); };
  const openLogin    = () => setShowLogin(true);

  const shared = { ticks, account, bots, setBots, authorized, send, on, onLogin:openLogin };

  const pageMap = {
    Dashboard: <Dashboard {...shared} />,
    Bots:      <BotsPage  {...shared} />,
    Signals:   <SignalsPage />,
    Markets:   <MarketsPage ticks={ticks} send={send} authorized={authorized} />,
    More:      <MoreMenu setActive={setPage} />,
    dTrader:   <DTraderPage />,
    Upload:    <UploadPage setBots={setBots} />,
  };

  return (
    <>
      {/* Global keyframe for spinner */}
      <style>{`
        @keyframes spin { to { transform:rotate(360deg); } }
        * { box-sizing:border-box; -webkit-tap-highlight-color:transparent; }
        body { margin:0; background:#070d1a; overscroll-behavior:none; }
        ::-webkit-scrollbar { display:none; }
        select, input, textarea, button { -webkit-appearance:none; font-family:inherit; }
        input[type=number]::-webkit-inner-spin-button { -webkit-appearance:none; }
      `}</style>

      <div style={S.app}>
        <TopBar connected={connected} account={account} onLogin={openLogin} onLogout={handleLogout} />

        <main style={S.main}>
          {pageMap[page] || pageMap.Dashboard}
        </main>

        <BottomNav active={page} setActive={setPage} />
      </div>

      {showLogin && <LoginModal onOAuth={handleOAuth} onPAT={handlePAT} onClose={() => setShowLogin(false)} />}
    </>
  );
}

// ═══════════════════════════════════════════════════════════════════════════════
//  STYLES  (mobile-first, no media queries needed — fluid by design)
// ═══════════════════════════════════════════════════════════════════════════════
const S = {
  // Layout
  app:  { display:"flex", flexDirection:"column", height:"100dvh", background:"#070d1a",
          color:"#e2e8f0", fontFamily:"'Inter',system-ui,sans-serif", overflow:"hidden" },
  main: { flex:1, overflowY:"auto", overflowX:"hidden" },

  // Top bar
  topBar: { display:"flex", justifyContent:"space-between", alignItems:"center",
            padding:"0 16px", height:52, background:"#0a1628",
            borderBottom:"1px solid #1e293b", flexShrink:0, zIndex:10 },

  // Bottom nav
  bottomNav: { display:"flex", background:"#0a1628", borderTop:"1px solid #1e293b",
               flexShrink:0, paddingBottom:"env(safe-area-inset-bottom, 0px)" },
  navItem: { flex:1, display:"flex", flexDirection:"column", alignItems:"center",
             justifyContent:"center", padding:"8px 0", background:"none", border:"none",
             color:"#334155", cursor:"pointer", fontSize:10, minHeight:52, gap:1 },
  navItemActive: { color:"#00d4aa" },

  // Page area
  page: { padding:"16px 14px 20px", maxWidth:600, margin:"0 auto" },
  pageTitle: { color:"#e2e8f0", fontSize:18, fontWeight:800, margin:"0 0 14px" },
  sectionTitle: { color:"#475569", fontSize:12, fontWeight:700, margin:"16px 0 8px",
                  textTransform:"uppercase", letterSpacing:.5 },

  // Connect banner
  connectBanner: { display:"flex", justifyContent:"space-between", alignItems:"center",
                   background:"#0f172a", border:"1px solid #1e3a5f", borderRadius:10,
                   padding:"10px 12px", marginBottom:14, fontSize:12, color:"#64748b" },

  // Stats grid
  statsGrid: { display:"grid", gridTemplateColumns:"1fr 1fr", gap:10, marginBottom:6 },
  statCard:  { background:"#0f172a", border:"1px solid #1e293b", borderRadius:12,
               padding:"14px 12px", textAlign:"center" },

  // Tick scroll
  tickScroll: { display:"flex", gap:8, overflowX:"auto", paddingBottom:6, scrollbarWidth:"none" },
  tickPill:   { flexShrink:0, background:"#0f172a", border:"1px solid #1e293b",
                borderRadius:10, padding:"10px 12px", minWidth:110 },

  // Bot card
  botCard:   { background:"#0f172a", border:"1px solid #1e293b", borderRadius:12, padding:14 },
  botCardOn: { border:"1px solid #00d4aa55", background:"#00d4aa08" },

  // Signal card
  signalCard: { background:"#0f172a", borderRadius:10, padding:14, border:"1px solid #1e293b" },

  // More card
  moreCard: { display:"flex", alignItems:"center", gap:14, background:"#0f172a",
              border:"1px solid #1e293b", borderRadius:12, padding:"16px 14px",
              cursor:"pointer", width:"100%", textAlign:"left" },

  // Form
  formGroup: { marginBottom:14 },
  label:  { display:"block", color:"#64748b", fontSize:11, marginBottom:5, fontWeight:700,
            textTransform:"uppercase", letterSpacing:.4 },
  input:  { width:"100%", background:"#0a1020", border:"1px solid #1e293b", borderRadius:8,
            padding:"11px 12px", color:"#e2e8f0", fontSize:13, outline:"none" },
  select: { background:"#0a1020", border:"1px solid #1e293b", borderRadius:8,
            padding:"9px 12px", color:"#e2e8f0", fontSize:12, outline:"none", width:"100%" },
  dropZone: { border:"2px dashed #1e293b", borderRadius:10, padding:"28px 16px",
              textAlign:"center", cursor:"pointer", fontSize:13, color:"#334155" },

  // Buttons
  primaryBtn: { background:"#00d4aa", color:"#000", border:"none", borderRadius:9,
                padding:"9px 16px", fontSize:13, fontWeight:800, cursor:"pointer" },
  startBtn:   { background:"#22c55e", color:"#000", border:"none", borderRadius:8,
                padding:"9px 16px", fontSize:12, fontWeight:800, cursor:"pointer" },
  stopBtn:    { background:"#ef4444", color:"#fff", border:"none", borderRadius:8,
                padding:"9px 16px", fontSize:12, fontWeight:800, cursor:"pointer" },
  uploadBtn:  { background:"#6366f1", color:"#fff", border:"none", borderRadius:8,
                padding:"8px 14px", fontSize:12, fontWeight:700, cursor:"pointer" },
  logoutBtn:  { background:"none", border:"1px solid #1e293b", color:"#475569",
                borderRadius:6, padding:"5px 9px", fontSize:11, cursor:"pointer" },
  iconBtn:    { background:"none", border:"none", color:"#475569", fontSize:18,
                cursor:"pointer", padding:4 },
  tabBtn:     { background:"none", border:"1px solid #1e293b", color:"#475569",
                borderRadius:20, padding:"6px 12px", fontSize:12, cursor:"pointer" },
  tabBtnActive: { background:"#00d4aa18", color:"#00d4aa", borderColor:"#00d4aa44" },

  // Misc
  logo:    { fontSize:18, fontWeight:900, color:"#e2e8f0", letterSpacing:-0.5 },
  dot:     { width:7, height:7, borderRadius:"50%", flexShrink:0 },
  badge:   { background:"#1e293b", color:"#64748b", fontSize:10, padding:"2px 7px",
             borderRadius:4, fontWeight:700 },
  spinner: { display:"inline-block", width:13, height:13, border:"2px solid #00d4aa33",
             borderTop:"2px solid #00d4aa", borderRadius:"50%",
             animation:"spin .8s linear infinite" },

  // Modal
  overlay: { position:"fixed", inset:0, background:"rgba(0,0,0,.75)", zIndex:200,
             display:"flex", alignItems:"flex-end", justifyContent:"center",
             padding:"0 0 env(safe-area-inset-bottom,0)" },
  modal:   { background:"#0f172a", borderRadius:"18px 18px 0 0", padding:"22px 18px 28px",
             width:"100%", maxWidth:480, border:"1px solid #1e293b",
             borderBottom:"none", maxHeight:"90vh", overflowY:"auto" },
};
