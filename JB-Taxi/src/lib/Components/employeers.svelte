<script>
  export let name = 'Jögga!'
  export let todayDate = new Intl.DateTimeFormat('sv-SE', { dateStyle: 'full' }).format(new Date())

  export let shift = {
    time: '06:00–14:00',
    vehicle: 'ABC123',
    status: 'Bekräftat',
  }

  export let totals = {
    rides: 0,
    cash: '0 kr',
    card: '0 kr',
    invoice: '0 kr',
    app: '0 kr'
  }

  export let recentRides = [
    { time:'08:15', amount:'240 kr', pay:'Kort',    linked:true  },
    { time:'08:40', amount:'180 kr', pay:'Kontant', linked:true  },
    { time:'09:10', amount:'320 kr', pay:'App',     linked:false }
  ]
</script>

<section class="wrap">
  <header class="head">
    <div>
      <h1>Hej {name}! 👋</h1>
      <p class="sub">{todayDate}</p>
    </div>
    <nav class="actions">
      <a href="#" class="btn ghost">🧾 Mina kvitton</a>
      <a href="#" class="btn">➕ Registrera körning</a>
    </nav>
  </header>

  <section class="panel">
    <h2>Mitt pass idag</h2>
    <div class="pass">
      <div class="big">{shift.time}</div>
      <div class="row">
        <span>🚗 Bil</span> <strong>{shift.vehicle}</strong>
      </div>
      <div class="row">
        <span>📌 Status</span> <strong>{shift.status}</strong>
      </div>
    </div>
  </section>

  <div class="cards">
    <article class="card">
      <div class="label">Antal körningar</div>
      <div class="value">{totals.rides}</div>
    </article>
    <article class="card">
      <div class="label">Kontant</div>
      <div class="value">{totals.cash}</div>
    </article>
    <article class="card">
      <div class="label">Kort</div>
      <div class="value">{totals.card}</div>
    </article>
    <article class="card">
      <div class="label">Faktura</div>
      <div class="value">{totals.invoice}</div>
    </article>
    <article class="card">
      <div class="label">App</div>
      <div class="value">{totals.app}</div>
    </article>
  </div>

  <section class="panel">
    <h2>Senaste körningar</h2>
    <table class="rides">
      <thead>
        <tr><th>Tid</th><th>Belopp</th><th>Betalning</th><th>Status</th></tr>
      </thead>
      <tbody>
        {#each recentRides as r}
          <tr>
            <td>{r.time}</td>
            <td>{r.amount}</td>
            <td>{r.pay}</td>
            <td>
              {#if r.linked}
                <span class="badge ok">Kopplad till pass</span>
              {:else}
                <a href="#" class="badge warn">Saknar pass</a>
              {/if}
            </td>
          </tr>
        {/each}
      </tbody>
    </table>
  </section>

  <section class="panel actions2">
    <button class="btn full">➕ Registrera ny körning</button>
    <button class="btn ghost full">📤 Skicka dagsrapport</button>
  </section>
</section>

<style>
  .wrap { max-width: 900px; margin: 0 auto; padding: 20px; font-family: sans-serif; }
  .head { display:flex; align-items:end; justify-content:space-between; gap:16px; margin-bottom: 20px; }
  h1 { margin:0; font-size: 24px; }
  .sub { margin:4px 0 0; color:#666; font-size: 14px; }
  .actions { display:flex; gap:10px; }
  .btn { background:#111; color:#fff; padding:10px 14px; border-radius:10px; text-decoration:none; font-size:14px; display:inline-block; }
  .btn.ghost { background:#fff; color:#111; border:1px solid #ddd; }
  .btn.full { width:100%; text-align:center; }
  .panel { border:1px solid #eee; border-radius:14px; padding:14px; margin-bottom:20px; }
  .panel h2 { margin:0 0 10px; font-size:18px; }
  .pass { display:grid; gap:8px; }
  .pass .big { font-size: 20px; font-weight: 600; }
  .row { display:flex; gap:8px; align-items:center; }
  .cards { display:grid; grid-template-columns: repeat(auto-fit, minmax(170px,1fr)); gap:12px; margin-bottom: 20px; }
  .card { border:1px solid #eee; border-radius:14px; padding:14px; }
  .label { color:#666; font-size:12px; }
  .value { font-size:20px; font-weight:600; margin-top:6px; }
  .rides { width:100%; border-collapse: collapse; font-size:14px; }
  .rides th, .rides td { padding:8px; border-bottom:1px solid #f0f0f0; text-align:left; }
  .badge { font-size:12px; padding:4px 8px; border-radius:999px; text-decoration:none; }
  .badge.ok { background:#eaf8ee; color:#1f7a33; }
  .badge.warn { background:#fff5e5; color:#955900; }
  .actions2 { display:grid; grid-template-columns: 1fr 1fr; gap:12px; }
  @media (max-width: 700px) {
    .head { flex-direction: column; align-items: flex-start; }
    .actions2 { grid-template-columns: 1fr; }
  }
</style>
