
## 📖 Overview

**StackerVault** is a passive yield-generating smart contract where users stake STX and earn compounding returns based on time held. The longer you hold and the more you upgrade, the higher your yield multiplier becomes!

### ✨ Key Features

- 🎯 **Passive Yield**: Earn STX automatically based on blocks elapsed
- 📈 **Compounding**: Reinvest yields to increase your stake
- ⚡ **Upgrades**: Purchase multiplier upgrades to boost earnings
- 🔄 **Flexible**: Add more stake or withdraw anytime
- 📊 **Stats Tracking**: Monitor your total stakes, claims, and upgrades

---

## 🚀 Usage Instructions

### For Players

#### 1️⃣ Start Your Idle Journey

```clarity
(contract-call? .stacker-vault start-idle u10000000)
```

Stakes 10 STX and begins earning passive yield.

#### 2️⃣ Check Your Pending Yield

```clarity
(contract-call? .stacker-vault calculate-pending-yield tx-sender)
```

Returns the amount of STX you've earned but haven't claimed yet.

#### 3️⃣ Claim Your Yield

```clarity
(contract-call? .stacker-vault claim-yield)
```

Withdraws your earned yield to your wallet.

#### 4️⃣ Compound Your Yield (Recommended!)

```clarity
(contract-call? .stacker-vault compound-yield)
```

Automatically adds your pending yield to your stake for exponential growth! 📈

#### 5️⃣ Upgrade Your Multiplier

```clarity
(contract-call? .stacker-vault upgrade-multiplier)
```

Purchase the next upgrade level to boost your earnings:
- Level 1: 1.5x multiplier (Cost: 1 STX)
- Level 2: 2x multiplier (Cost: 5 STX)
- Level 3: 3x multiplier (Cost: 10 STX)
- Level 4: 5x multiplier (Cost: 25 STX)
- Level 5: 10x multiplier (Cost: 50 STX)

#### 6️⃣ Add More Stake

```clarity
(contract-call? .stacker-vault add-stake u5000000)
```

Increases your stake by 5 STX (auto-claims pending yield first).

#### 7️⃣ View Your Stats

```clarity
(contract-call? .stacker-vault get-player-info tx-sender)
```

Shows your complete player data and pending yield.

#### 8️⃣ Unstake Everything

```clarity
(contract-call? .stacker-vault unstake-all)
```

Withdraws your entire stake plus all pending yield and deactivates your account.

---

## 🎮 How It Works

### Yield Calculation Formula

```
Yield = (Stake × Blocks Elapsed × Base Rate × Multiplier) / (Global Multiplier × 1,000,000)
```

**Default Settings:**
- Base Yield Rate: 100 (micro-STX per block per STX staked)
- Global Multiplier: 1,000,000 (for precision)
- Personal Multiplier: Starts at 1x, upgradeable to 10x

### Example Scenario

You stake **10 STX** with a **2x multiplier**:
- After 100 blocks: ~0.002 STX earned
- After 1,000 blocks: ~0.02 STX earned
- After 10,000 blocks: ~0.2 STX earned

**With compounding**, your earnings accelerate exponentially! 🚀

---

## 🏗️ Architecture

### Data Structures

- **`player-data`**: Stores stake, multiplier, claim history per user
- **`player-stats`**: Tracks lifetime statistics (stakes, claims, upgrades)
- **`upgrade-costs`**: Maps upgrade levels to their STX cost
- **`upgrade-multipliers`**: Maps upgrade levels to yield multipliers

### Core Mechanics

1. **Time-based Accrual**: Yield accumulates every block based on your stake
2. **Compounding Loop**: Reinvesting yields increases future earnings exponentially
3. **Upgrade System**: Purchase permanent multiplier boosts
4. **Flexible Management**: Claim, compound, or unstake at any time

---

## 🧪 Testing Example

```bash
# Deploy the contract
clarinet contract deploy stacker-vault

# Start idling with 10 STX
clarinet contract call stacker-vault start-idle u10000000 --sender wallet-1

# Wait some blocks (simulated by advancing chain)
clarinet mine-blocks 1000

# Check pending yield
clarinet contract call stacker-vault calculate-pending-yield 'ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM

# Compound the yield
clarinet contract call stacker-vault compound-yield --sender wallet-1

# Upgrade multiplier
clarinet contract call stacker-vault upgrade-multiplier --sender wallet-1

# Check updated stats
clarinet contract call stacker-vault get-player-info 'ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM

# Unstake everything
clarinet contract call stacker-vault unstake-all --sender wallet-1
```

---

## ⚙️ Admin Functions

### Set Base Yield Rate

```clarity
(contract-call? .stacker-vault set-base-yield-rate u200)
```

Adjusts global yield generation rate.

### Set Global Multiplier

```clarity
(contract-call? .stacker-vault set-global-multiplier u1000000)
```

Fine-tunes precision and yield scaling.

### Configure Upgrades

```clarity
(contract-call? .stacker-vault set-upgrade-config u6 u100000000 u20000000)
```

Adds a new upgrade level (Level 6: 20x multiplier for 100 STX).

---

## 💡 Strategy Tips

1. **Compound Early and Often** - Maximize exponential growth
2. **Upgrade ASAP** - Higher multipliers = faster accumulation
3. **Stake More** - Larger stakes generate more yield
4. **Be Patient** - Time is your friend in idle games!

---

## 📝 Git Commit Message

```
feat: implement StackerVault with compounding yield mechanism
```

---

## 🔀 GitHub Pull Request

**Title:**
```
🔐 Add StackerVault MVP with Time-based Compounding
```

**Description:**
```markdown
## Summary
Implements a passive yield-generating vault where players stake STX and earn compounding returns based on blocks held.

## What's Added
- 🎯 Passive yield accumulation system based on block height
- 📈 Compounding mechanism to reinvest earnings
- ⚡ 5-level upgrade system with multiplier boosts (1.5x → 10x)
- 🔄 Flexible stake management (add, claim, compound, unstake)
- 📊 Player statistics tracking (lifetime stakes, claims, upgrades)
- 🎮 Idle game mechanics with exponential growth potential

## Core Functions
- `start-idle`: Begin earning with initial stake
- `claim-yield`: Withdraw earned STX
- `compound-yield`: Reinvest yields for exponential growth
- `upgrade-multiplier`: Boost earnings with permanent upgrades
- `add-stake`: Increase position size
- `unstake-all`: Exit with full balance

## Technical Highlights
- Time-based yield calculation using block heights
- Compounding loops demonstrating caller epoch patterns
- Precision handling with 1,000,000 multiplier base
- Upgrade cost/multiplier mapping system
- 180+ lines of clean, production-ready Clarity code

## Game Economics
- Base yield: 100 micro-STX per block per STX
- 5 upgrade tiers with increasing costs and multipliers
- Fully customizable by contract owner
- Emergency withdrawal for security

Ready to start earning passively! 🚀
```

---

## 📄 License

MIT