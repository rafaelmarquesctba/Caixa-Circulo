<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Caixa — Círculo de Oração</title>
<link href="https://fonts.googleapis.com/css2?family=Lora:ital,wght@0,400;0,600;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --verde: #1D9E75;
    --verde-claro: #E1F5EE;
    --verde-medio: #9FE1CB;
    --verde-escuro: #085041;
    --vermelho: #D85A30;
    --vermelho-claro: #FAECE7;
    --vermelho-medio: #F0997B;
    --dourado: #BA7517;
    --dourado-claro: #FAEEDA;
    --cinza-bg: #F7F5F0;
    --cinza-card: #FFFFFF;
    --cinza-borda: #E2DDD5;
    --cinza-texto: #5F5E5A;
    --texto: #2C2C2A;
    --radius: 12px;
    --radius-sm: 8px;
  }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--cinza-bg);
    color: var(--texto);
    min-height: 100vh;
    padding-bottom: 3rem;
  }

  /* Header */
  .page-header {
    background: var(--verde-escuro);
    color: #fff;
    padding: 2rem 1.5rem 3rem;
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  .page-header::before {
    content: '';
    position: absolute;
    width: 300px; height: 300px;
    border-radius: 50%;
    background: rgba(255,255,255,0.04);
    top: -80px; right: -60px;
  }
  .page-header::after {
    content: '';
    position: absolute;
    width: 200px; height: 200px;
    border-radius: 50%;
    background: rgba(255,255,255,0.04);
    bottom: -60px; left: -40px;
  }
  .header-icon {
    font-size: 2rem;
    margin-bottom: 0.5rem;
    opacity: 0.9;
  }
  .page-header h1 {
    font-family: 'Lora', serif;
    font-size: 1.6rem;
    font-weight: 600;
    letter-spacing: 0.01em;
  }
  .page-header p {
    font-size: 0.85rem;
    opacity: 0.7;
    margin-top: 4px;
    font-weight: 300;
  }
  .header-data {
    font-size: 0.8rem;
    opacity: 0.6;
    margin-top: 8px;
  }

  /* Container */
  .container {
    max-width: 700px;
    margin: -1.5rem auto 0;
    padding: 0 1rem;
    position: relative;
    z-index: 1;
  }

  /* Cards resumo */
  .resumo-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
    margin-bottom: 1.5rem;
  }
  .resumo-card {
    background: var(--cinza-card);
    border-radius: var(--radius);
    padding: 1rem;
    border: 1px solid var(--cinza-borda);
    box-shadow: 0 2px 8px rgba(0,0,0,0.06);
    text-align: center;
  }
  .resumo-card .label {
    font-size: 0.7rem;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--cinza-texto);
    margin-bottom: 6px;
    font-weight: 500;
  }
  .resumo-card .valor {
    font-family: 'Lora', serif;
    font-size: 1.2rem;
    font-weight: 600;
  }
  .resumo-card.saldo .valor { color: var(--texto); }
  .resumo-card.entrada .valor { color: var(--verde); }
  .resumo-card.saida .valor { color: var(--vermelho); }
  .resumo-card .sub {
    font-size: 0.68rem;
    color: var(--cinza-texto);
    margin-top: 3px;
  }

  /* Seção */
  .secao {
    background: var(--cinza-card);
    border-radius: var(--radius);
    border: 1px solid var(--cinza-borda);
    margin-bottom: 1rem;
    overflow: hidden;
    box-shadow: 0 2px 8px rgba(0,0,0,0.04);
  }
  .secao-header {
    padding: 1rem 1.25rem 0.75rem;
    border-bottom: 1px solid var(--cinza-borda);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .secao-titulo {
    font-family: 'Lora', serif;
    font-size: 1rem;
    font-weight: 600;
    color: var(--texto);
    display: flex;
    align-items: center;
    gap: 8px;
  }
  .secao-titulo .icon { font-size: 1rem; }
  .secao-body { padding: 1rem 1.25rem; }

  /* Tabela entradas do culto */
  .tabela {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.85rem;
  }
  .tabela th {
    text-align: left;
    padding: 6px 10px;
    font-size: 0.7rem;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    color: var(--cinza-texto);
    font-weight: 500;
    border-bottom: 1px solid var(--cinza-borda);
  }
  .tabela td {
    padding: 9px 10px;
    border-bottom: 1px solid #F0EDE8;
    color: var(--texto);
  }
  .tabela tr:last-child td { border-bottom: none; }
  .tabela tr:hover td { background: #FAFAF8; }
  .tabela .td-valor { text-align: right; font-weight: 500; }
  .tabela .td-verde { color: var(--verde); text-align: right; font-weight: 500; }
  .tabela .td-vermelho { color: var(--vermelho); text-align: right; font-weight: 500; }
  .tabela .total-row td {
    font-weight: 600;
    background: var(--cinza-bg);
    border-top: 2px solid var(--cinza-borda);
    border-bottom: none;
    font-family: 'Lora', serif;
  }
  .badge {
    display: inline-block;
    padding: 2px 8px;
    border-radius: 20px;
    font-size: 0.72rem;
    font-weight: 500;
  }
  .badge-verde { background: var(--verde-claro); color: var(--verde-escuro); }
  .badge-vermelho { background: var(--vermelho-claro); color: #71280F; }
  .badge-dourado { background: var(--dourado-claro); color: #633806; }

  /* Caixa geral */
  .caixa-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 0;
    border-bottom: 1px solid #F0EDE8;
    font-size: 0.9rem;
  }
  .caixa-row:last-child { border-bottom: none; }
  .caixa-row .desc { color: var(--cinza-texto); font-size: 0.82rem; }
  .caixa-row .val { font-family: 'Lora', serif; font-weight: 600; font-size: 1.05rem; }

  /* Fiados */
  .fiado-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 8px 0;
    border-bottom: 1px solid #F0EDE8;
    font-size: 0.88rem;
  }
  .fiado-item:last-child { border-bottom: none; }
  .fiado-nome { color: var(--texto); }
  .fiado-val { color: var(--dourado); font-weight: 600; font-family: 'Lora', serif; }
  .fiado-total {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 0 0;
    border-top: 2px solid var(--cinza-borda);
    margin-top: 4px;
    font-size: 0.88rem;
  }
  .fiado-total .fl { color: var(--cinza-texto); font-weight: 500; font-size: 0.8rem; text-transform: uppercase; letter-spacing: 0.06em; }
  .fiado-total .fv { color: var(--dourado); font-weight: 700; font-family: 'Lora', serif; font-size: 1.05rem; }

  /* Destaque saldo final */
  .saldo-destaque {
    background: var(--verde-escuro);
    color: #fff;
    border-radius: var(--radius);
    padding: 1.25rem 1.5rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 1rem;
    box-shadow: 0 4px 16px rgba(8,80,65,0.25);
  }
  .saldo-destaque .sd-label {
    font-size: 0.78rem;
    opacity: 0.75;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    margin-bottom: 4px;
  }
  .saldo-destaque .sd-val {
    font-family: 'Lora', serif;
    font-size: 1.8rem;
    font-weight: 600;
  }
  .saldo-destaque .sd-icon { font-size: 2.2rem; opacity: 0.4; }

  /* Footer */
  .rodape {
    text-align: center;
    font-size: 0.75rem;
    color: var(--cinza-texto);
    margin-top: 2rem;
    opacity: 0.7;
  }

  /* Responsivo */
  @media (max-width: 480px) {
    .resumo-grid { grid-template-columns: 1fr 1fr; }
    .resumo-card.saldo { grid-column: 1 / -1; }
    .page-header h1 { font-size: 1.3rem; }
    .saldo-destaque .sd-val { font-size: 1.4rem; }
  }
</style>
</head>
<body>

<div class="page-header">
  <div class="header-icon">✝</div>
  <h1>Círculo de Oração</h1>
  <p>Controle de Caixa</p>
  <div class="header-data">Período: maio / junho 2026</div>
</div>

<div class="container">

  <!-- Resumo -->
  <div class="resumo-grid">
    <div class="resumo-card saldo">
      <div class="label">Total em Caixa</div>
      <div class="valor">R$ 6.034,36</div>
      <div class="sub">conta + dinheiro</div>
    </div>
    <div class="resumo-card entrada">
      <div class="label">Entradas Culto</div>
      <div class="valor">R$ 464,00</div>
      <div class="sub">4 cultos</div>
    </div>
    <div class="resumo-card saida">
      <div class="label">Saídas</div>
      <div class="valor">R$ 484,80</div>
      <div class="sub">5 lançamentos</div>
    </div>
  </div>

  <!-- Saldo total destacado -->
  <div class="saldo-destaque">
    <div>
      <div class="sd-label">Saldo disponível</div>
      <div class="sd-val">R$ 6.034,36</div>
    </div>
    <div class="sd-icon">🏦</div>
  </div>

  <!-- Entradas do culto -->
  <div class="secao">
    <div class="secao-header">
      <div class="secao-titulo">
        <span class="icon">📥</span> Entradas — Ofertas do Culto
      </div>
      <span class="badge badge-verde">+R$ 464,00</span>
    </div>
    <div class="secao-body">
      <table class="tabela">
        <thead>
          <tr>
            <th>Data</th>
            <th>Tipo</th>
            <th style="text-align:right">Valor</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>07/05/2026</td>
            <td><span class="badge badge-verde">Culto</span></td>
            <td class="td-verde">R$ 65,70</td>
          </tr>
          <tr>
            <td>14/05/2026</td>
            <td><span class="badge badge-verde">Culto</span></td>
            <td class="td-verde">R$ 156,50</td>
          </tr>
          <tr>
            <td>21/05/2026</td>
            <td><span class="badge badge-verde">Culto</span></td>
            <td class="td-verde">R$ 112,00</td>
          </tr>
          <tr>
            <td>28/05/2026</td>
            <td><span class="badge badge-verde">Culto</span></td>
            <td class="td-verde">R$ 129,80</td>
          </tr>
        </tbody>
        <tfoot>
          <tr class="total-row">
            <td colspan="2">Total entradas culto</td>
            <td class="td-verde">R$ 464,00</td>
          </tr>
        </tfoot>
      </table>
    </div>
  </div>

  <!-- Saídas -->
  <div class="secao">
    <div class="secao-header">
      <div class="secao-titulo">
        <span class="icon">📤</span> Saídas
      </div>
      <span class="badge badge-vermelho">−R$ 484,80</span>
    </div>
    <div class="secao-body">
      <table class="tabela">
        <thead>
          <tr>
            <th>Data</th>
            <th>Descrição</th>
            <th style="text-align:right">Valor</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>08/05</td>
            <td>Pregadora Elaine</td>
            <td class="td-vermelho">R$ 150,00</td>
          </tr>
          <tr>
            <td>21/05</td>
            <td>Pregadora Maria de Lurdes</td>
            <td class="td-vermelho">R$ 150,00</td>
          </tr>
          <tr>
            <td>28/05</td>
            <td>Pregadora Regina</td>
            <td class="td-vermelho">R$ 150,00</td>
          </tr>
          <tr>
            <td>08/05</td>
            <td>Papel pão</td>
            <td class="td-vermelho">R$ 21,90</td>
          </tr>
          <tr>
            <td>27/05</td>
            <td>Envelopes</td>
            <td class="td-vermelho">R$ 12,90</td>
          </tr>
        </tbody>
        <tfoot>
          <tr class="total-row">
            <td colspan="2">Total saídas</td>
            <td class="td-vermelho">R$ 484,80</td>
          </tr>
        </tfoot>
      </table>
    </div>
  </div>

  <!-- Caixa geral -->
  <div class="secao">
    <div class="secao-header">
      <div class="secao-titulo">
        <span class="icon">💰</span> Caixa Geral (06/06/2026)
      </div>
    </div>
    <div class="secao-body">
      <div class="caixa-row">
        <div>
          <div>Em conta</div>
          <div class="desc">Saldo bancário</div>
        </div>
        <div class="val" style="color:var(--verde)">R$ 3.935,36</div>
      </div>
      <div class="caixa-row">
        <div>
          <div>Em dinheiro</div>
          <div class="desc">Caixa físico</div>
        </div>
        <div class="val" style="color:var(--verde)">R$ 2.099,00</div>
      </div>
      <div class="caixa-row" style="padding-top:12px">
        <div style="font-weight:600; font-family:'Lora',serif">Total em caixa</div>
        <div class="val" style="font-size:1.2rem">R$ 6.034,36</div>
      </div>
    </div>
  </div>

  <!-- Fiados pão 08/05 -->
  <div class="secao">
    <div class="secao-header">
      <div class="secao-titulo">
        <span class="icon">📋</span> Fiados — Pão (08/05)
      </div>
      <span class="badge badge-dourado">R$ 120,00 a receber</span>
    </div>
    <div class="secao-body">
      <div class="fiado-item">
        <span class="fiado-nome">Juninho</span>
        <span class="fiado-val">R$ 15,00</span>
      </div>
      <div class="fiado-item">
        <span class="fiado-nome">Claúdia (Vanessa)</span>
        <span class="fiado-val">R$ 15,00</span>
      </div>
      <div class="fiado-item">
        <span class="fiado-nome">Hélida</span>
        <span class="fiado-val">R$ 15,00</span>
      </div>
      <div class="fiado-item">
        <span class="fiado-nome">Mirian Mazali</span>
        <span class="fiado-val">R$ 15,00</span>
      </div>
      <div class="fiado-item">
        <span class="fiado-nome">Leila</span>
        <span class="fiado-val">R$ 30,00</span>
      </div>
      <div class="fiado-item">
        <span class="fiado-nome">Angélica</span>
        <span class="fiado-val">R$ 30,00</span>
      </div>
      <div class="fiado-total">
        <span class="fl">Total a receber</span>
        <span class="fv">R$ 120,00</span>
      </div>
    </div>
  </div>

  <div class="rodape">
    Círculo de Oração · Atualizado em junho 2026
  </div>

</div>
</body>
</html>
