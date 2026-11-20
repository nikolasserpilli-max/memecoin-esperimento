# REGOLE PRE-REGISTRATE — Memecoin Esperimento (paper trading)

Registrate il **20/11/2026 alle 15:52 (ora di Roma)**, PRIMA dell'avvio del run live in simulazione.
Non verranno modificate durante il test. Ogni cambiamento futuro = nuovo esperimento con nuova data e saldo azzerato.

## Modalità
- **SOLO PAPER (soldi finti).** Nessun ordine reale, nessuna API key, nessun exchange collegato.
- Saldo iniziale: **100 €** simulati. Semplificazione: **1 EUR = 1 USDT** (non si considera il cambio EUR/USD).
- Prezzi: reali, pubblici, da Binance spot (`data-api.binance.vision`, endpoint di soli dati di mercato).

## Universo (14 coppie spot USDT, verificate attive su Binance)
DOGE, PEPE, TRUMP, PENGU, BONK, SHIB, WIF, FLOKI, BOME, NEIRO, PNUT, MEME, PEOPLE, TURBO.

## Pipeline (i 6 agenti della dashboard)
| Agente | Ruolo | Regola |
|---|---|---|
| 01 SCAN · ZUNO | cerca candidati | ogni minuto, sulla candela 1m **chiusa**: rendimento ultimi 5 min **> +1,0%** E volume ultimi 5 min **> 2×** la media (finestra 240 min) |
| 02 VET · PELL | filtro liquidità | spread bid/ask (bookTicker) **≤ 0,15%** e liquidità sull'ask ≥ 2× l'ordine. (Esclude di fatto PEPE/SHIB/BONK & co., il cui spread "a tick" è 0,2–0,5%) |
| 03 SIZE · KAVO | dimensione | rischio 1% del capitale / stop 2% → ~45% del capitale per trade (tetto 45%), minimo 5 € |
| 04 RISK · RIMA | rischio | stop loss **−2%**, take profit **+4%**, time stop **30 min**, max **2** posizioni aperte, cooldown 15 min per token, **limite perdita giornaliera −5%** (stop ingressi fino a mezzanotte, ora di Roma) |
| 05 FILLS · TOSK | esecuzione simulata | acquisto all'**ask** +0,03% slippage, vendita al **bid** −0,03%, **commissione 0,1% per lato** |
| 06 BOOK · VEYA | contabilità | `state.json`, `trades.csv`, `equity.csv`, `summary.json`, `site/data/live.json` |

Controllo uscite ogni ~5 secondi sul bid reale.

## Come sono stati scelti i parametri (backtest)
- Dati: klines 1m Binance di 13 coppie (TURBO escluso per limite di richieste API), dal 12/11/2026 15:46 al 20/11/2026 15:46 (ora di Roma), ~8 giorni.
- Costi nel backtest: fee 0,1%/lato + metà dello spread misurato per coppia + slippage 0,03%/lato; ingresso all'apertura della candela successiva; se TP e SL toccati nella stessa candela si assume lo SL.
- Griglia di 3.456 combinazioni (momentum e mean-reversion). Selezione su 70% iniziale (train), verifica sul 30% finale (test).
- Scelta: la combinazione migliore in train (momentum 5m >1%, volume >2×, TP 4%, SL 2%, 30 min).

### Risultati onesti (netti di fee e spread)
| Periodo | Rendimento | Trade | Winrate | Profit factor | Max drawdown |
|---|---|---|---|---|---|
| Train (~5,6 giorni) | +1,77% | 28 | 53,6% | 1,40 | 3,2% |
| Test (~2,4 giorni) | −0,57% | 3 | 33,3% | 0,13 | 0,8% |
| Intero periodo | +1,19% | 31 | 51,6% | 1,24 | 3,2% |

- Solo il **9%** delle combinazioni (315/3.456) era positivo in train: compatibile con il puro caso.
- Le 50 migliori in train hanno fatto in media **−1,73%** nel test (solo 6 su 50 positive).
- La "rotazione veloce" stile video (soglia 0,6%, TP/SL 1%) ha perso **−27%** in 8 giorni dopo i costi.
- **Conclusione: nessuna prova di un vantaggio reale.** Con così pochi trade il risultato è indistinguibile dal caso. Il run paper serve a verificarlo in avanti, non a confermare un guadagno.

## Il video di riferimento
Il video (@0xnevsky, "$50 → $3.532 in 4 min 14 s, 99 fill, 82% winrate", token COIN-01…COIN-12) è quasi certamente un'animazione: nessun exchange o chain mostrati, rendimenti impossibili. Di quel video copiamo **solo il design**.
