# Trade8 - Professional Trading Desk Platform

**Secure Post-Quantum-Safe Trading Platform That Heals and Scales Itself.**

Trade8 is the professional trading desk vertical of the Sentin8 platform — a complete proprietary trading suite: keyboard-class order entry, pre-trade risk gating, broker connectivity via FIX/OUCH, consolidated market data, OHLCV bars, and real-time P&L. Built for proprietary desks and introducing brokers with complete regulatory traceability.

## Services

| Service | Domain | What it does |
|---|---|---|
| **Trade8:Desk** | Trading Desk | Order entry (limit/market/baskets/flatten), session lifecycle, instrument/routing catalogs, short-sale locate pool |
| **Trade8:Risk** | Pre-Trade Risk | Buying power checks, limits enforcement, restrictions, trader states, loss ladder (day-loss thresholds → close-only/disable) |
| **Trade8:Router** | Broker Connectivity | FIX 4.2/4.4 + OUCH 3.1 sessions, routing to any broker, fee calculation, fill normalization |
| **Trade8:Feed** | Market Data | Vendor adapters, consolidated quotes/ladders/tape, SSE streaming, price alerts (declarative + tenant-authored) |
| **Trade8:Bars** | Historical Data | OHLCV bars (1s-1D), intraday candles, history windows, EOD finalization |
| **Trade8:Pnl** | Performance & Reconciliation | Day P&L: positions, realized/unrealized, fees, LFT, office roll-ups; overnight carry + reconciliation |

## Flutter Apps

| Repository | Description |
|---|---|
| `trade8-etrader` | Professional trading keyboard (F-key chain), ladder/tape/charts, P&L board |
| `trade8-desk` | Desk management console |
| `trade8-admin` | Vertical admin console (RFW) |

## Platform Dependencies

Trade8 depends on these Sentin8 platform services for cross-cutting concerns:

| Platform Service | What Trade8 gets from it | Dependency direction |
|---|---|---|
| **Sentin8:Auth** | Identity, sign-in, credentials, tokens to clients | trade8 → Auth (verification + M2M identity) |
| **Sentin8:BFF** | Authorization decision engine (Shield RBAC/ABAC/ReBAC), proxying | trade8 ← BFF (user tokens proxied to services) |
| **Sentin8:Bus** | Durable event transport & audit store | trade8 → Bus (produce + consume domain events) |
| **Sentin8:Cron** | Scheduling (session times, purge, EOD, carry-outs) | trade8 → Cron (schedule registration) |
| **Sentin8:Func** | User-authored strategy execution | trade8 ← Func (proxy-back handlers for hooks) |
| **Sentin8:Sys** | Audit ingest + storage | trade8 → Sys (audit events) |
| **Sentin8:Storage** | Object storage / secret vault | trade8 → Storage (document PUT/GET) |
| **Sentin8:Stat** | Business metrics aggregation and telemetry | trade8 → Stat (event ingestion) |
| **Exchange8** | Venue-side matching, auctions, clearing, regulatory feeds | trade8 → Exchange8 (sibling vertical integration) |

## Key Invariants

- **Keyboard-class speed** — F-key chain (buy/sell limit & market, cancel-all, flatten) with profile-synced muscle memory
- **Fail-closed authorization** — no Risk verdict means no acceptance; denies carry the itemized check trace into the blotter
- **Instant supervision** — closing-only/disable flips a trader within a second, without touching credentials
- **One source of money** — fill-derived, exactly-once P&L application; office rolls up from trader numbers by construction
- **Full reconstruction** — any day replays to identical numbers from journal + opening balances; every wire message preserved

---

**Architecture & Design:** trade8 and its underlying concepts were designed by [Hamid Jahanzad](https://www.linkedin.com/in/hamidjahanzad/).
