# Bug Tracker

## Summary

| ID | Severity | File | Status |
|---|---|---|---|
| BUG-A01 | High | `analyze.ts` | ✅ Resolved |
| BUG-A02 | Medium | `analyze.ts` | ✅ Resolved (not a bug) |
| BUG-A03 | Medium | `watch.ts` | ✅ Resolved |
| BUG-A04 | Medium | `bot-config.ts` | ✅ Resolved |
| BUG-A05 | Low | `dispatch.ts` | ✅ Resolved |
| BUG-A06 | Critical | `kelly.ts` | ✅ Resolved |
| BUG-A07 | Medium | `analyze.ts` | ✅ Resolved |
| BUG-A08 | Medium | `parse-args.ts` | ✅ Resolved |
| BUG-A09 | Low | `parse-args.ts` | ✅ Resolved |
| BUG-A10 | Low | `bot-config.ts` | ✅ Resolved |
| BUG-A11 | Medium | `browse.ts` / `event-index.ts` | ✅ Resolved |
| BUG-A12 | Medium | `browse.ts` | ✅ Resolved |
| BUG-A13 | Low | `search-index.ts` | ✅ Resolved |
| BUG-A14 | Low | `cli.ts` | ✅ Resolved |
| BUG-A15 | Medium | `browse.ts` / `edge-computer.ts` | ✅ Resolved |
| BUG-A16 | Medium | `paths.ts` | ✅ Resolved (by design) |
| BUG-A17 | High | `wizard.ts` | ✅ Resolved |
| BUG-NEW-01 | High | `edge-computer.ts:73` | ✅ Resolved |
| BUG-NEW-02 | Medium | `octagon-client.ts:25` | ✅ Resolved |
| BUG-NEW-03 | Low | `loop.ts:127` | ✅ Resolved |
| BUG-NEW-04 | Critical | `index.ts:99` | ✅ Resolved |
| BUG-NEW-05 | High | `index.ts:89` | ✅ Resolved |
| BUG-NEW-06 | Low | `wizard.ts:205` | ✅ Resolved |
| BUG-NEW-07 | Low | `search-index.ts:149` | ✅ Resolved |
| BUG-NEW-08 | High | `watch.ts:231` | ✅ Resolved |
| BUG-NEW-09 | Medium | `index.ts:216` | ✅ Resolved |
| BUG-NEW-10 | Low | `watch.ts:48,228` | ✅ Resolved |
| BUG-NEW-11 | Low | `bot-config.ts:97` | ✅ Resolved |
| BUG-NEW-12 | Low | `loop.ts:173-174` | ✅ Resolved |
| BUG-NEW-13 | Medium | `loop.ts:150` | ✅ Resolved |
| BUG-NEW-14 | Low | `watch.ts:121` | ✅ Resolved |
| BUG-NEW-15 | Low | `watch.ts:132` | ✅ Resolved |
| BUG-NEW-16 | Medium | `edge.ts:34` | ✅ Resolved |
| BUG-NEW-17 | Low | `event-index.ts:167,196` | ✅ Resolved |
| BUG-NEW-18 | High | `search-index.ts:175` | ✅ Resolved |
| BUG-NEW-19 | Medium | `browse-list.ts:88` | ✅ Resolved |
| BUG-NEW-20 | Medium | `edge-computer.ts:63` | ✅ Resolved |
| BUG-B01 | Low | `help.ts` | ✅ Resolved |
| BUG-B02 | Medium | `help.ts` | ✅ Resolved |
| BUG-B03 | Low | `help.ts` | ✅ Resolved |
| BUG-B04 | Critical | `paths.ts` | ✅ Resolved |
| BUG-B05 | Medium | `watch.ts:132` | ✅ Resolved |
| BUG-B06 | Low | `types.ts` / `watch.ts` | ✅ Resolved |
| BUG-B07 | Low | `edge-computer.ts:114` | ✅ Resolved |
| BUG-B08 | High | `browse.ts:460` | ✅ Resolved |
| BUG-B09 | Critical | `wizard.ts:576` | ✅ Resolved |
| BUG-B10 | High | `octagon-client.ts` | ✅ Resolved |
| BUG-B11 | Medium | `octagon-client.ts` | ✅ Resolved |
| BUG-B12 | High | `wizard.ts` | ✅ Resolved |
| BUG-B13 | Medium | `invoker.ts:139` | ✅ Resolved |
| BUG-B14 | High | `theme-resolver.ts` | ✅ Resolved |

---

## Known Bugs (BUG-A01 — BUG-A17)

### BUG-A01 — `logTrade` has `position_id: null`; trade and position never linked
**File:** `src/commands/analyze.ts`
**Status:** ✅ Resolved — `positionId` from `openPosition` (line 458) is now passed to `logTrade` (line 477). Trade and position properly linked.

### BUG-A02 — `logTrade` action always `'buy'` even for NO-side trades
**File:** `src/commands/analyze.ts`
**Status:** ✅ Resolved — Kalshi API uses `action: 'buy', side: 'no'` for NO-side purchases. The `action: 'buy'` is correct API semantics.

### BUG-A03 — `handleWatchTicker` setInterval calls `runTick()` with no `.catch()`
**File:** `src/commands/watch.ts:264`
**Status:** ✅ Resolved — `setInterval` callback at lines 264-269 properly calls `runTick().catch(...)`. Same pattern at lines 91-96.

### BUG-A04 — `JSON.parse(rawValue)` for array type not wrapped in try/catch
**File:** `src/utils/bot-config.ts:142`
**Status:** ✅ Resolved — Lines 146-149 wrap `JSON.parse` in try/catch with descriptive error message.

### BUG-A05 — `JSON.parse(ev.markets_json)` in search not guarded
**File:** `src/commands/dispatch.ts:96`
**Status:** ✅ Resolved — `markets_json` comes from trusted SQLite index populated by `clearAndPopulateIndex` using `JSON.stringify`.

### BUG-A06 — Division by zero if `pricingProb === 0` or `1`
**File:** `src/risk/kelly.ts:169`
**Status:** ✅ Resolved — Guard at lines 166-168: `if (pricingProb <= 0 || pricingProb >= 1) return makeResult(...)`.

### BUG-A07 — `readline` blocks stdin indefinitely when not in a TTY
**File:** `src/commands/analyze.ts`
**Status:** ✅ Resolved — Line 383: `if (!process.stdin.isTTY) return;` skips interactive menu for non-TTY sessions.

### BUG-A08 — `--theme`/`--ticker`/`--interval`/`--since` do no bounds check on `argv[++i]`
**File:** `src/commands/parse-args.ts`
**Status:** ✅ Resolved — Lines 56-117: All flags check `val != null` before use; missing values push to `parseErrors` array.

### BUG-A09 — `--interval 0` or negative accepted with no validation
**File:** `src/commands/parse-args.ts`
**Status:** ✅ Resolved — Line 73: Validates `Number.isFinite(numeric) && numeric > 0`.

### BUG-A10 — Boolean config only accepts lowercase `'true'`
**File:** `src/utils/bot-config.ts:140`
**Status:** ✅ Resolved — Lines 140-144: Calls `rawValue.toLowerCase()` for case-insensitive comparison.

### BUG-A11 — `Mkt %` uses bid/ask mid; `last_price` never stored in `markets_json`
**File:** `src/controllers/browse.ts` + `src/db/event-index.ts`
**Status:** ✅ Resolved — `event-index.ts:107` now stores `last_price` and `dollar_last_price` in compact markets. `parseMarketProb` prefers last_price.

### BUG-A12 — `parseMarketProb` uses bid/ask mid instead of `last_price`
**File:** `src/controllers/browse.ts:58`
**Status:** ✅ Resolved — `parseMarketProb` (lines 65-79) prefers `dollar_last_price` / `last_price`, falls back to bid/ask mid only when unavailable.

### BUG-A13 — No `--refresh` flag to force immediate index rebuild
**File:** `src/tools/kalshi/search-index.ts`
**Status:** ✅ Resolved — `forceRefreshIndex()` at lines 148-157, invoked from `dispatch.ts:98` when `--refresh` flag is set.

### BUG-A14 — `/browse` still accepted as silent alias for `/search`
**File:** `src/cli.ts:410`
**Status:** ✅ Resolved — Commit `36a529c` removed the `/browse` alias. Only `/search` is accepted now.

### BUG-A15 — `isMarketOpen` lets through untraded/resolved markets; no `last_price` guard
**File:** `src/controllers/browse.ts` + `src/scan/edge-computer.ts`
**Status:** ✅ Resolved — `isMarketActive` (lines 83-99) checks status, result, and `last_price > 0` with transition fallback for old index rows.

### BUG-A16 — `appPath()` resolves `config.json` relative to CWD not package root
**File:** `src/utils/paths.ts`
**Status:** ✅ Resolved (by design) — Intentionally CWD-relative per commit `eca8478`. CLI state stays in user workspace. `.env` (package root) and `config.json` (CWD) resolve separately by design.

### BUG-A17 — Never creates `config.json` or shows threshold defaults after onboarding
**File:** `src/setup/wizard.ts`
**Status:** ✅ Resolved — Lines 648-651: Creates `config.json` with defaults after tests if it doesn't exist. Shows threshold customization examples in completion screen.

---

## New Bugs

### BUG-NEW-01 — `computeAll` bypasses `parseMarketProb`, breaks on dollar-string API fields

**File:** `src/scan/edge-computer.ts:73`
**Severity:** High
**Status:** ✅ Resolved — `computeAll` now uses `parseMarketProb(market)` from `browse.ts`.

---

### BUG-NEW-02 — OctagonClient daily credit ceiling ignores config setting

**File:** `src/scan/octagon-client.ts:25`
**Severity:** Medium
**Status:** ✅ Resolved — Constructor now reads `getBotSetting('octagon.daily_credit_ceiling')` as fallback.

---

### BUG-NEW-03 — Scan audit log records UUID instead of theme name

**File:** `src/scan/loop.ts:127`
**Severity:** Low
**Status:** ✅ Resolved — Audit log now uses `theme: opts.theme` and `scan_id: scanId` as separate fields.

---

### BUG-NEW-04 — `executePendingTrade` always sends `yes_price` even for NO-side trades

**File:** `src/commands/index.ts:99`
**Severity:** Critical

**Code:**
```typescript
const body: Record<string, unknown> = {
  ticker: trade.ticker,
  action: trade.action,
  side: trade.side,
  type: 'limit',
  count: trade.count,
  yes_price: effectivePrice, // ← always yes_price regardless of side
};
```

**What is wrong:** When the user places a NO-side trade via the TUI (e.g., `/buy TICKER 10 no`), the order payload always sends `yes_price` instead of `no_price`. Compare with `dispatch.ts:284-286` which correctly uses `no_price` for no-side trades.

**Impact:** NO-side trades placed via the TUI slash command are sent with the wrong price field. The Kalshi API may reject the order, fill at the wrong price, or interpret the price as a YES-side price — potentially costing real money.

**Fix:** Use the same side-conditional logic as dispatch.ts:
```typescript
...(trade.side === 'no'
  ? { no_price: effectivePrice }
  : { yes_price: effectivePrice }),
```

---

### BUG-NEW-05 — `executePendingTrade` fetches quote for wrong side

**File:** `src/commands/index.ts:89`
**Severity:** High

**Code:**
```typescript
const quoteResult = await fetchMarketQuote(trade.ticker, trade.action);
```

**What is wrong:** `fetchMarketQuote` accepts a `side` parameter (default `'yes'`) but `executePendingTrade` doesn't pass `trade.side`. When a user places a market-price NO trade (no explicit price), the function fetches the YES ask instead of the NO ask.

**Impact:** NO-side market orders without an explicit price get the wrong quote — the YES side price is used as the NO side limit price, resulting in incorrect fill prices and potential financial loss.

**Fix:** Pass the trade side: `await fetchMarketQuote(trade.ticker, trade.action, trade.side)`

---

### BUG-NEW-06 — Wizard shows incorrect `config` command syntax

**File:** `src/setup/wizard.ts:205-209`
**Severity:** Low

**Code:**
```typescript
lines.push(`    min_edge_threshold  = 5%     ${theme.muted('e.g. bun start config set risk.min_edge_threshold 0.10')}`);
```

**What is wrong:** The completion screen shows `config set <key> <value>` but `handleConfig` in `config.ts` treats positional[0] as the key directly (no `set` subcommand). The word "set" becomes the key, causing `Unknown config key: set`.

**Impact:** Users following the wizard's instructions get an error when trying to customize thresholds after onboarding.

**Fix:** Change examples from `config set risk.min_edge_threshold 0.10` to `config risk.min_edge_threshold 0.10`.

---

### BUG-NEW-07 — `forceRefreshIndex` returns stale data instead of forcing new refresh

**File:** `src/tools/kalshi/search-index.ts:148-152`
**Severity:** Low

**Code:**
```typescript
export async function forceRefreshIndex(): Promise<void> {
  if (_refreshPromise) {
    await _refreshPromise;
    return; // ← exits without starting new refresh
  }
```

**What is wrong:** The doc comment says "waits for it to complete first, then starts a new one" but the code returns immediately after awaiting the in-flight refresh. When a user runs `--refresh` while a background refresh is already in progress, no forced re-fetch occurs.

**Impact:** `search --refresh` and `watch --refresh` don't guarantee fresh data when a background refresh is already running. The user's explicit refresh intent is silently ignored.

**Fix:** Remove the early `return` so a new refresh starts after the in-flight one completes.

**Status:** ✅ Resolved — Removed early `return` on line 151. Now waits for in-flight refresh then starts a new one as documented.

---

### BUG-NEW-08 — `handleWatchTicker` uses `getBotSetting` result without NaN guard, causing infinite setInterval

**File:** `src/commands/watch.ts:231`
**Severity:** High

**Code:**
```typescript
const tickerIntervalMs = (getBotSetting('watch.ticker_interval_seconds') as number) * 1000;
const intervalMs = args.interval ? args.interval * 1000 : tickerIntervalMs;
```

**What is wrong:** `getBotSetting` returns `unknown`. If the config file is malformed or the key is missing from a user-edited config, the cast `as number` produces `undefined * 1000 = NaN`. `setInterval(..., NaN)` fires immediately and continuously, hammering the Kalshi API with infinite requests per second.

**Impact:** A corrupted or hand-edited `config.json` with a missing `watch.ticker_interval_seconds` key causes infinite API calls, potential rate-limiting or ban from Kalshi.

**Fix:** Add a NaN guard:
```typescript
const rawInterval = Number(getBotSetting('watch.ticker_interval_seconds'));
const tickerIntervalMs = (Number.isFinite(rawInterval) && rawInterval > 0 ? rawInterval : 5) * 1000;
```

**Status:** ✅ Resolved — Both `watch.ticker_interval_seconds` (line 231) and `watch.min_interval_minutes` (line 17) now use `Number()` + `Number.isFinite()` guards with safe defaults (5s and 15m respectively).

---

### BUG-NEW-09 — `/cancel` in TUI has no try/catch — API errors crash the TUI

**File:** `src/commands/index.ts:216-221`
**Severity:** Medium

**Code:**
```typescript
async function handleCancel(orderId: string | undefined): Promise<CommandResult> {
  if (!orderId) return { output: 'Usage: /cancel <order_id>' };
  await callKalshiApi('DELETE', `/portfolio/orders/${orderId}`);
  return { output: `Order ${orderId} canceled.` };
}
```

**What is wrong:** No try/catch around the API call. If the order is already filled, doesn't exist, or the API returns a 404/500, the error propagates unhandled. Compare with `dispatch.ts:312-326` which properly catches and provides helpful hints.

**Impact:** Attempting to cancel a non-existent or already-filled order in the TUI causes an unhandled error, showing a raw error stack trace instead of a user-friendly message.

**Fix:** Wrap in try/catch matching dispatch.ts pattern:
```typescript
async function handleCancel(orderId: string | undefined): Promise<CommandResult> {
  if (!orderId) return { output: 'Usage: /cancel <order_id>' };
  try {
    await callKalshiApi('DELETE', `/portfolio/orders/${orderId}`);
  } catch (err) {
    const msg = err instanceof Error ? err.message : String(err);
    const hint = msg.includes('404') ? ' (order not found or already filled)' : '';
    return { output: `Cancel failed: ${msg}${hint}` };
  }
  return { output: `Order ${orderId} canceled.` };
}
```

**Status:** ✅ Resolved — Added try/catch with 404 hint, matching the dispatch.ts cancel pattern.

---

### BUG-NEW-10 — Signal handlers accumulate without cleanup in watch commands

**File:** `src/commands/watch.ts:48-49, 228-229`
**Severity:** Low

**Code:**
```typescript
process.on('SIGINT', shutdown);
process.on('SIGTERM', shutdown);
```

**What is wrong:** `process.on` adds a new listener each time `handleWatch` or `handleWatchTicker` is called. If a watch command is stopped and restarted, duplicate handlers accumulate. The `setInterval` timer in `handleWatchTicker` (line 264) is also never cleared — `shutdown()` calls `process.exit(0)` directly.

**Impact:** Minor memory leak on repeated watch invocations. In embedded/test contexts where `process.exit` is mocked, the interval continues firing after "shutdown".

**Fix:** Use `process.once` instead of `process.on`; store and clear the interval timer in the shutdown handler.

**Status:** ✅ Resolved — Both `handleWatch` and `handleWatchTicker` now use `process.once`, hoist the timer variable, and call `clearInterval(timer)` in shutdown.

---

### BUG-NEW-11 — `loadBotConfig` reads config file synchronously on every `getBotSetting` call

**File:** `src/utils/bot-config.ts:97-101`
**Severity:** Low

**Code:**
```typescript
export function getBotSetting(dotKey: string): unknown {
  const config = loadBotConfig();  // reads from disk every time
  const keys = dotKey.split('.');
  return walkGet(config as unknown as Record<string, unknown>, keys);
}
```

**What is wrong:** `getBotSetting` is called many times per scan cycle (kelly.ts, gate.ts, octagon-client.ts, watch.ts, etc.). Each call triggers a synchronous `readFileSync` + `JSON.parse` of `config.json`. During a scan with 30 events, this results in 100+ synchronous file reads.

**Impact:** Performance degradation during scan cycles. On slower filesystems or under high load, this adds measurable latency.

**Fix:** Cache the parsed config in-memory and invalidate on `setBotSetting` or with a short TTL.

**Status:** ✅ Resolved — Added `_cachedConfig` module-level cache. `loadBotConfig` returns cached value on subsequent calls; `saveBotConfig` updates the cache directly. Eliminates 100+ synchronous disk reads per scan cycle.

---

### BUG-NEW-12 — ScanLoop.start() signal handlers leak: uses `process.on` and never removes in stop()

**File:** `src/scan/loop.ts:173-174`
**Severity:** Low

**Code:**
```typescript
process.on('SIGINT', shutdown);
process.on('SIGTERM', shutdown);
```

**What is wrong:** `process.on` adds a new listener each call. `stop()` clears the interval timer but never removes these signal handlers. In test/programmatic contexts where `start()`/`stop()` cycles occur, duplicate handlers accumulate. `watch.ts` was fixed in BUG-NEW-10 to use `process.once`, but `loop.ts` was not updated.

**Impact:** Memory leak and Node.js MaxListeners warning in long-running or test contexts. Old handlers reference stale closures.

**Fix:** Use `process.once` instead of `process.on`.

**Status:** ✅ Resolved — Changed `process.on` to `process.once` for both SIGINT and SIGTERM handlers, consistent with the watch.ts fix.

---

### BUG-NEW-13 — ScanLoop.start() allows minIntervalMinutes=0, enabling infinite setInterval

**File:** `src/scan/loop.ts:150`
**Severity:** Medium

**Code:**
```typescript
const minIntervalMinutes = Number.isFinite(rawMinInterval) && rawMinInterval >= 0
  ? rawMinInterval
  : DEFAULT_INTERVAL_MINUTES;
```

**What is wrong:** The guard uses `>= 0` instead of `> 0`, allowing a zero-minute minimum interval. The equivalent code in `watch.ts:18` correctly uses `> 0`. If config.json is hand-edited to set `watch.min_interval_minutes: 0`, then `setInterval(..., 0)` fires continuously.

**Impact:** Continuous scan loop with no delay, hammering the Octagon and Kalshi APIs. Potential rate-limiting or banning.

**Fix:** Change `>= 0` to `> 0`.

**Status:** ✅ Resolved — Changed guard from `rawMinInterval >= 0` to `rawMinInterval > 0`, consistent with watch.ts.

---

### BUG-NEW-14 — `parseDollarField` in watch.ts doesn't convert cent values to dollars, causing incorrect spread display

**File:** `src/commands/watch.ts:121-125, 147-150`
**Severity:** Low

**Code:**
```typescript
function parseDollarField(val: string | number | undefined | null): number {
  if (val === undefined || val === null) return 0;
  const n = typeof val === 'number' ? val : parseFloat(val as string);
  return isNaN(n) ? 0 : n;
}
// ...
const yesAsk = parseDollarField(m.yes_ask_dollars ?? m.dollar_yes_ask ?? m.yes_ask);
const spread = yesAsk - yesBid;
spread: `$${spread.toFixed(4)}`,
```

**What is wrong:** `parseDollarField` returns raw values without normalizing units. When the API response uses legacy cent-based fields (e.g., `yes_ask: 55` instead of `yes_ask_dollars: "0.55"`), the function returns `55` (cents) where dollars are expected. The spread calculation then produces `5` (cents) but is displayed as `$5.0000` instead of `$0.0500`. Compare with `parsePriceField` in `browse.ts:51-62` which properly converts cent values by dividing by 100.

**Impact:** Ticker watch dashboard (`watch <TICKER>`) shows an inflated spread value when Kalshi API returns cent-based fields. Display-only; does not affect trading logic.

**Fix:** Add `isCentField` parameter to `parseDollarField` and pass `true` when falling back to cent-based fields, dividing by 100 to normalize to dollars.

**Status:** ✅ Resolved — Added `isCentField` parameter to `parseDollarField` that divides by 100 when the value comes from a cent field. Call sites detect whether dollar fields exist and pass the flag accordingly.

---

### BUG-NEW-15 — `fmtPrice` shows 4 decimal places for dollar-denominated prices

**File:** `src/commands/watch.ts:132`
**Severity:** Low

**Code:**
```typescript
return `$${n > 1 ? (n / 100).toFixed(2) : n.toFixed(4)}`;
```

**What is wrong:** After BUG-NEW-14 fixed `parseDollarField` to always output dollar values (0-1 range), the `fmtPrice` function's `n > 1` heuristic no longer triggers for parsed bid/ask values. The dollar branch uses `.toFixed(4)`, displaying prices like `$0.5500` instead of `$0.55`. The `lastPrice` field also shows 4 decimal places when the API returns dollar-format strings (e.g., `dollar_last_price: "0.55"`).

**Impact:** Ticker watch dashboard displays prices with unnecessary precision (`$0.5500` instead of `$0.55`), creating visual noise and inconsistent formatting between cent-sourced and dollar-sourced values.

**Fix:** Normalize to dollars first (using the existing `n > 1` cent detection), then always format with `.toFixed(2)`.

**Status:** ✅ Resolved — Changed `fmtPrice` to convert to dollars first, then format consistently with 2 decimal places.

---

### BUG-NEW-16 — `edge --theme` query references non-existent column in `events` table

**File:** `src/commands/edge.ts:34`
**Severity:** Medium

**Code:**
```typescript
const themeRows = db.query(
  `SELECT DISTINCT ticker FROM edge_history
   WHERE event_ticker IN (SELECT event_ticker FROM events WHERE theme_id = $theme)`
).all({ $theme: args.theme }) as { ticker: string }[];
```

**What is wrong:** The `events` table (schema.ts:17-25) has a `ticker` column as its primary key, not `event_ticker`. The subquery `SELECT event_ticker FROM events` references a non-existent column, causing an SQLite error.

**Impact:** `edge --theme <theme>` command crashes with "no such column: event_ticker" error. Theme-filtered edge viewing is completely broken.

**Fix:** Change `SELECT event_ticker FROM events` to `SELECT ticker FROM events`.

**Status:** ✅ Resolved — Fixed column name from `event_ticker` to `ticker` in the events table subquery.

---

### BUG-NEW-17 — Unguarded `JSON.parse(r.markets_json)` in `getEventsFromIndex` and `getTopEventsByVolume`

**File:** `src/db/event-index.ts:167, 196`
**Severity:** Low

**Code:**
```typescript
// Line 167 (getEventsFromIndex)
const markets = r.markets_json ? JSON.parse(r.markets_json) : [];
// Line 196 (getTopEventsByVolume)
const markets = r.markets_json ? JSON.parse(r.markets_json) : [];
```

**What is wrong:** If `markets_json` contains malformed JSON (from DB corruption, interrupted writes, or manual edits), these calls throw an unhandled error that propagates up and crashes the entire browse or search flow.

**Impact:** A single corrupted index row crashes all event retrieval for browse and search commands.

**Fix:** Wrap both `JSON.parse` calls in try/catch, defaulting to an empty array on parse failure so other events still load.

**Status:** ✅ Resolved — Added try/catch around both JSON.parse calls with empty array fallback.

---

### BUG-NEW-18 — Unhandled promise rejection in ensureIndex background refresh

**File:** `src/tools/kalshi/search-index.ts:175`
**Severity:** High

**Code:**
```typescript
_refreshPromise = refreshIndex().finally(() => {
  _refreshPromise = null;
});
```

**What is wrong:** `ensureIndex()` fires `refreshIndex()` as a background (fire-and-forget) promise. If `refreshIndex()` throws (line 139 re-throws), the rejection is never caught — only `.finally()` is chained, which does not handle rejections. This results in an unhandled promise rejection.

**Impact:** Node/Bun will emit an `unhandledRejection` warning (or crash in strict mode) whenever the background index refresh fails due to network errors, API failures, or DB issues.

**Fix:** Add `.catch()` before `.finally()` to log the error and suppress the unhandled rejection.

**Status:** ✅ Resolved — Added `.catch()` handler that logs the error via logger.error before the `.finally()` block.

---

### BUG-NEW-19 — JSON.parse without try/catch in browse list onSelect

**File:** `src/components/browse-list.ts:88`
**Severity:** Medium

**Code:**
```typescript
const parsed = JSON.parse(item.value);
onSelect(parsed.eventTicker, parsed.marketTicker);
```

**What is wrong:** `JSON.parse(item.value)` is called without a try/catch. While `item.value` is constructed via `JSON.stringify()` during list building, if the value becomes corrupted or the item structure changes, this will throw an unhandled error that crashes the browse flow.

**Impact:** A single malformed item value crashes the entire browse selector, preventing users from selecting any market.

**Fix:** Wrap `JSON.parse` in try/catch and return early on failure.

**Status:** ✅ Resolved — Added try/catch around JSON.parse with early return on parse failure.

---

### BUG-NEW-20 — `computeAll` per-event API fetch not wrapped in try-catch; single bad event breaks entire scan

**File:** `src/scan/edge-computer.ts:63`
**Severity:** Medium

**Code:**
```typescript
for (const eventTicker of tickers) {
  const response = await callKalshiApi('GET', `/events/${eventTicker}`, {
    params: { with_nested_markets: true },
  });
  // ... process markets
}
```

**What is wrong:** The event fetch on line 64 has no try-catch. If any single event ticker returns an error (404, 500, rate limit), the entire `computeAll` throws with zero results. The `Promise.allSettled` on line 91 only covers the Octagon report fetches (Phase B), not the Kalshi event fetches (Phase A).

**Impact:** A single stale or deleted event ticker from the theme resolver breaks the entire scan cycle. The scan loop repeatedly fails until the next index refresh removes the bad ticker. During this window (up to 2 hours), all edge monitoring is non-functional.

**Fix:** Wrap the per-event API call in try-catch and continue with remaining events, logging the error via audit trail.

**Status:** ✅ Resolved — Added try-catch around per-event Kalshi API call with audit trail logging and continue.

---

## Bug Report v3 (BUG-B01 — BUG-B14)

### BUG-B01 — `/help` slash overview doesn't list `clear-cache`
**File:** `src/commands/help.ts`
**Severity:** Low
**Status:** ✅ Resolved — `clear-cache` is a CLI-only command already listed in CLI overview (line 125). Not applicable to slash commands since `/clear-cache` is not a TUI command.

---

### BUG-B02 — `buildTopics` has no entry for `clear-cache`
**File:** `src/commands/help.ts`
**Severity:** Medium
**Status:** ✅ Resolved — Added `clear-cache` topic to `buildTopics` with description of what it does and the DB path.

---

### BUG-B03 — Help error message hardcodes partial topic list
**File:** `src/commands/help.ts`
**Severity:** Low
**Status:** ✅ Resolved — Error message at line 185 already uses dynamic `Object.keys(topics).join(', ')`. Adding `clear-cache` to topics automatically includes it. Removed hardcoded list from the `help` topic description.

---

### BUG-B04 — `clear-cache` deletes the wrong directory / path inconsistency
**File:** `src/utils/paths.ts` · `src/db/index.ts` · `src/commands/clear-cache.ts`
**Severity:** Critical
**Status:** ✅ Resolved — Changed `paths.ts` to use `join(homedir(), '.kalshi-bot')` matching the DB location in `db/index.ts`. All app data now under `~/.kalshi-bot/`.

---

### BUG-B05 — `fmtPrice` `n > 1` heuristic fails at exactly 1 cent
**File:** `src/commands/watch.ts:132`
**Severity:** Medium
**Status:** ✅ Resolved — Changed `n > 1` to `n >= 1`. Dollar values are always < 1 (0.01–0.99), cent values are >= 1 (1–99).

---

### BUG-B06 — `last_price_dollars` checked in watch.ts but not in KalshiMarket type
**File:** `src/tools/kalshi/types.ts` · `src/commands/watch.ts`
**Severity:** Low
**Status:** ✅ Resolved — Added `last_price_dollars?: string` to KalshiMarket type definition.

---

### BUG-B07 — `edge-computer.ts` uses `indexOf` to find failed task
**File:** `src/scan/edge-computer.ts:114`
**Severity:** Low
**Status:** ✅ Resolved — Replaced `for...of` + `indexOf` with standard indexed `for` loop.

---

### BUG-B08 — `ensureIndex()` error silently swallowed in browse controller
**File:** `src/controllers/browse.ts:460`
**Severity:** High
**Status:** ✅ Resolved — Added `console.warn` in catch handler to log refresh failures.

---

### BUG-B09 — Wizard hardcodes `claude-haiku-4-5-20251001` for Anthropic key test
**File:** `src/setup/wizard.ts:576`
**Severity:** Critical
**Status:** ✅ Resolved — Model ID now reads from `process.env.ANTHROPIC_TEST_MODEL` with fallback to the hardcoded value.

---

### BUG-B10 — `octagon-client.ts` doesn't validate parsed catalysts is an array
**File:** `src/scan/octagon-client.ts`
**Severity:** High
**Status:** ✅ Resolved — Added `Array.isArray(parsed)` check after JSON.parse with empty array fallback.

---

### BUG-B11 — `octagon-client.ts` TTL calculation uses negative delta for closed markets
**File:** `src/scan/octagon-client.ts`
**Severity:** Medium
**Status:** ✅ Resolved — Added `Math.max(0, ...)` to clamp negative deltas to zero.

---

### BUG-B12 — Wizard `saveBotConfig()` failure is silent
**File:** `src/setup/wizard.ts`
**Severity:** High
**Status:** ✅ Resolved — When `saveBotConfig` returns false, a FAIL test result is now added to inform the user that config.json could not be written.

---

### BUG-B13 — Octagon API error dumps raw HTML body into terminal
**File:** `src/scan/invoker.ts:139`
**Severity:** Medium
**Status:** ✅ Resolved — HTML responses are detected and stripped. Plain-text bodies capped at 200 chars.

---

### BUG-B14 — `theme-resolver.ts` fetches entire Kalshi dataset with no server-side filter
**File:** `src/scan/theme-resolver.ts`
**Severity:** High
**Status:** ✅ Resolved — Added `category: categoryLabel` param to `/events` and `/series` API calls in `resolveCategory` and `resolveSubcategory`.
