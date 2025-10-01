<script>
  export let title = 'Chefsöversikt'
  export let kpi = { shiftsToday: 5, ridesToday: 42, cashToday: '3 200 kr' }
  export let shifts = [
    { time: '06:00–14:00', vehicle: 'ABC123', driver: 'Anna' },
    { time: '14:00–22:00', vehicle: 'DEF456', driver: 'Kalle' },
    { time: '22:00–06:00', vehicle: 'GHI789', driver: '' }
  ]
  export let rides = [
    { time: '08:15', vehicle: 'ABC123', driver: 'Anna', amount: '240 kr', pay: 'Kort' },
    { time: '08:40', vehicle: 'DEF456', driver: 'Kalle', amount: '180 kr', pay: 'Kontant' },
    { time: '09:10', vehicle: 'ABC123', driver: 'Anna', amount: '320 kr', pay: 'App' }
  ]
</script>

<section class="wrap">
  <h1>{title}</h1>

  <div class="cards">
    <article class="card">
      <div class="label">Pass idag</div>
      <div class="value">{kpi.shiftsToday}</div>
    </article>
    <article class="card">
      <div class="label">Körningar idag</div>
      <div class="value">{kpi.ridesToday}</div>
    </article>
    <article class="card">
      <div class="label">Kontant att redovisa</div>
      <div class="value">{kpi.cashToday}</div>
    </article>
  </div>

  <section class="panel">
    <h2>Dagens pass</h2>
    <ul>
      {#each shifts as s}
        <li>{s.time} • {s.vehicle} • {s.driver ? `👤 ${s.driver}` : '❗ Obemannat'}</li>
      {/each}
    </ul>
  </section>

  <section class="panel">
    <h2>Senaste körningar</h2>
    <table>
      <thead>
        <tr><th>Tid</th><th>Bil</th><th>Förare</th><th>Belopp</th><th>Betalning</th></tr>
      </thead>
      <tbody>
        {#each rides as r}
          <tr>
            <td>{r.time}</td><td>{r.vehicle}</td><td>{r.driver}</td><td>{r.amount}</td><td>{r.pay}</td>
          </tr>
        {/each}
      </tbody>
    </table>
  </section>
</section>

<style>
  .wrap { max-width: 900px; margin: 0 auto; padding: 20px; font-family: sans-serif; }
  h1 { font-size: 26px; margin-bottom: 20px; }
  .cards { display: grid; grid-template-columns: repeat(auto-fit,minmax(200px,1fr)); gap:12px; margin-bottom:20px; }
  .card { border:1px solid #ddd; border-radius:10px; padding:14px; }
  .label { color:#666; font-size:12px; }
  .value { font-size:20px; font-weight:600; }
  .panel { border:1px solid #ddd; border-radius:10px; padding:14px; margin-bottom:20px; }
  .panel h2 { margin:0 0 10px; font-size:18px; }
  table { width:100%; border-collapse:collapse; font-size:14px; }
  th,td { padding:6px; border-bottom:1px solid #eee; text-align:left; }
</style>
