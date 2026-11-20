# Criterio per passare ai soldi veri (GO LIVE)

**Stato attuale: SOLO PAPER. Nessun soldo vero, nessun exchange collegato, nessuna API key.**
I soldi veri si useranno solo dopo che **Nikolas lo approva esplicitamente**, e solo se TUTTI i criteri sotto sono soddisfatti.

## Criteri (tutti obbligatori, calcolati netti di commissioni, spread e slippage)
1. **Durata:** almeno **4 settimane** (28 giorni) di paper trading continuo con le regole di `RULES.md` invariate (minimo assoluto 2 settimane solo se si superano 150 trade).
2. **Numero di trade:** almeno **100 trade chiusi**.
3. **Profit factor ≥ 1,3** (somma guadagni / somma perdite, netto costi).
4. **Rendimento netto positivo** e superiore a quello del semplice "compra e tieni" DOGE nello stesso periodo.
5. **Max drawdown ≤ 10%** del capitale nel periodo paper.
6. **Nessun giorno peggiore di −5%** (il limite giornaliero deve aver funzionato).
7. **Robustezza:** il risultato resta positivo togliendo i 3 trade migliori, e almeno 3 settimane su 4 sono in positivo o in pari.
8. **Coerenza con il backtest:** costi reali stimati (spread misurati live) non peggiori di quelli ipotizzati.
9. **Affidabilità tecnica:** nessun crash non recuperato, nessun buco nei dati > 30 minuti.

## Se si va live (solo dopo approvazione)
- Capitale iniziale reale massimo **100 €**, solo soldi che si è disposti a perdere del tutto.
- API key Binance (o altro exchange disponibile in Italia/UE) **solo trading, mai prelievo**, con whitelist IP.
- Prime 2 settimane live a metà dimensione; stop totale se il drawdown reale supera il 15%.
- Ogni modifica alle regole = ritorno in paper.

## Nota onesta
Il backtest su 8 giorni NON ha mostrato un vantaggio statistico (vedi `RULES.md`). È probabile che questo test paper non superi i criteri: in quel caso la risposta corretta è **non usare soldi veri**.
