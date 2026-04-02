# PowerBase ⚡ — Electric Power Converter on Base

> Convert electric power between any unit ↔ Horsepower.  
> Calculate current (Amps) for DC, AC single-phase & 3-phase circuits.  
> Every calculation triggers a Base transaction, logged permanently on-chain.  
> Owner: `0x07b43A7546201720f888989C9c3472B228aae505`

---

## Files

| File | Purpose |
|------|---------|
| `PowerBase.sol` | Smart contract — deploy on Base via Remix |
| `index.html` | Full DApp frontend |
| `vercel.json` | Vercel static deployment config |
| `icon.png` | 1024×1024 Base app icon |
| `splash.png` | 200×200 splash screen |
| `og.png` | 1200×630 social preview |
| `.well-known/farcaster.json` | Base Mini App manifest |

---

## Step 1 — Deploy on Base via Remix

1. Go to **https://remix.ethereum.org**
2. New file → paste `PowerBase.sol`
3. Compile: Solidity `^0.8.20`
4. Deploy:
   - Environment: **Injected Provider — MetaMask**
   - Network: **Base Mainnet** (Chain ID 8453)
5. Copy deployed address

---

## Step 2 — Verify on Basescan

1. **https://basescan.org/verifyContract**
2. Paste address · Compiler `0.8.20` · Paste source · Submit ✓

---

## Step 3 — Update Frontend

In `index.html` find line ~230:
```js
const CONTRACT_ADDRESS = "0x0000000000000000000000000000000000000000";
```
Replace with your deployed address.

Also replace all `DOMAIN_PLACEHOLDER` in:
- `index.html` (OG meta tags)
- `.well-known/farcaster.json`

With your Vercel domain (e.g. `powerbase.vercel.app`).

---

## Step 4 — Push to GitHub & Deploy on Vercel

Repo structure:
```
/
├── index.html
├── vercel.json
├── icon.png
├── splash.png
├── og.png
├── README.md
└── .well-known/
    └── farcaster.json
```

**https://vercel.com/new** → Import repo → Framework: Other → Deploy

---

## Step 5 — Register on Base.dev

1. **https://base.dev** → Connect wallet `0x07b4…`
2. Create project → enter Vercel URL
3. Copy the `<meta name="base:app_id" content="..."/>` tag
4. Paste into `index.html` `<head>` (replace `BASEID_PLACEHOLDER`)
5. Push to GitHub → Vercel auto-redeploys → Verify on base.dev ✓

---

## Contract: PowerBase.sol

### Power Units Supported (11 total)
| Enum | Symbol | = Watts |
|------|--------|---------|
| 0 | W | 1.000000 |
| 1 | kW | 1,000.000000 |
| 2 | MW | 1,000,000.000000 |
| 3 | GW | 1,000,000,000.000000 |
| 4 | hp | 745.699870 |
| 5 | PS | 735.498750 |
| 6 | BTU/h | 0.293071 |
| 7 | cal/s | 4.186800 |
| 8 | ft·lbf/s | 1.355818 |
| 9 | mW | 0.001000 |
| 10 | kcal/h | 1.163000 |

### Current Formulas
| Circuit | Formula |
|---------|---------|
| DC | I = P / V |
| AC Single Phase | I = P / (V × PF) |
| AC 3Φ Delta | I = P / (√3 × V × PF) |
| AC 3Φ Wye | I = P / (√3 × VL × PF) |

### Key Functions
```
convertPower(fromUnit, amount×1000, toUnit, note)
  → (outputAmount, hpMilliUnits)

calculateCurrent(powerMW, voltageMV, circuitType, pfMilli, note)
  → currentMilliAmps

deployMiniApp(name, config) → appId
```

---

*Built for `0x07b43A7546201720f888989C9c3472B228aae505`*
