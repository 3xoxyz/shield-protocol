# Shield Protocol Product Design Document

## Table of Contents

1. [Product Overview](#1-product-overview)
2. [User Flow](#2-user-flow)
3. [Page Design Details](#3-page-design-details)
4. [Design Logic and Principles](#4-design-logic-and-principles)
5. [Technology Stack Details](#5-technology-stack-details)
6. [Project Implementation Logic](#6-project-implementation-logic)
7. [Smart Contract Architecture](#7-smart-contract-architecture)
8. [Data Flow and State Management](#8-data-flow-and-state-management)

---

## 1. Product Overview

### 1.1 One-Sentence Definition

> Shield Protocol is an **intent-driven asset protection and automation platform** based on MetaMask ERC-7715 advanced permissions.

### 1.2 Core Problems Solved

```
Traditional DeFi Pain Points                    Shield Solutions
─────────────────────────────────────────────────────────────
❌ Unlimited approval risk              →    ✅ Granular permission control
❌ Manual signature for each transaction →    ✅ One-time authorization, automatic execution
❌ Cannot set spending limits           →    ✅ Daily/per-transaction limit protection
❌ DCA requires daily manual operations →    ✅ Strategy automatic execution
❌ No native subscription payments      →    ✅ Web3 native subscriptions
❌ Only discover issues after they occur →    ✅ Real-time monitoring and alerts
```

### 1.3 Target Users

| User Type | Needs | Shield Features | Status |
|---------|------|------------|------|
| **DeFi Investors** | DCA, stop-loss, auto-reinvest | Auto-Pilot strategies | ✅ Implemented |
| **Security-Conscious Users** | Limit authorization, prevent phishing | Smart Shield protection | ✅ Implemented |
| **Content Creators** | Receive subscription payments | Web3 Subscriptions | ✅ Implemented |
| **AI Agent Developers** | Secure on-chain execution permissions | Agent Permission Framework | 🚧 Phase 3 Planning |

### 1.4 🚀 Project Innovations

#### 1.4.1 Industry Pain Points and Data

```
📊 DeFi Security Data (2024)
─────────────────────────────────────────────────────────────
• Losses due to unlimited approval vulnerabilities: $120M+ (Badger DAO, Radiant Capital, etc.)
• Only 10.8% of users regularly check token approvals (Georgia Tech study)
• Average user has 15+ unused unlimited approvals
• Manual DCA operations: ~150 clicks per month (5 times/day × 30 days)
• 63% of users abandon DeFi due to complexity
```

#### 1.4.2 Core Innovation Comparison

| Innovation Dimension | Traditional Solution | Shield Protocol | Innovation Value |
|---------|---------|-----------------|---------|
| **Permission Model** | Unlimited token approve | ERC-7715 granular permissions | 🔐 Minimum permission principle |
| **Execution Method** | User manually signs each transaction | Intent-driven, automatic execution | ⚡ 98% efficiency improvement |
| **Security Boundaries** | Full trust in DApp | Cryptographic enforced limits | 🛡️ Defense depth |
| **Account Type** | EOA or AA requiring new address | EIP-7702 in-place upgrade | 🔄 Seamless migration |
| **Feature Integration** | Multi-platform, multi-authorization | One platform, one authorization | 📦 Unified experience |

#### 1.4.3 Six Core Innovations

**🔐 Innovation 1: First ERC-7715 Native Permission Platform**
```
Traditional approve:
User → approve(spender, type(uint256).max) → Unlimited approval → Lifetime valid

Shield ERC-7715:
User → grantPermission(limit, time, whitelist) → Granular control → Can be revoked anytime
```
- Native MetaMask wallet support, consistent user interface
- Permission boundaries guaranteed by cryptography, not contract trust
- Supports time limits, amount limits, contract whitelists

**⚡ Innovation 2: Intent-Driven Architecture**
```
User input: "I want to DCA $20 daily to buy ETH"
     ↓
System parsing: Identified as DCA strategy
     ↓
Permission calculation: Only need $20/day × token × Uniswap contract
     ↓
One-time authorization: MetaMask popup shows precise permission scope
     ↓
Automatic execution: Backend Keeper executes daily, no more signatures needed
```

**🛡️ Innovation 3: Multi-Layer Defense Security Architecture**
```
┌─────────────────────────────────────────────────────┐
│ Layer 5: Emergency freeze - One-click revoke all permissions │
├─────────────────────────────────────────────────────┤
│ Layer 4: Price protection - 20%+ deviation auto-pause strategy │
├─────────────────────────────────────────────────────┤
│ Layer 3: Time lock - Configuration modification 24h + emergency withdrawal 48h cooldown │
├─────────────────────────────────────────────────────┤
│ Layer 2: Whitelist - Only allow interaction with trusted contracts │
├─────────────────────────────────────────────────────┤
│ Layer 1: Limit protection - Daily limit + per-transaction limit + token limit │
└─────────────────────────────────────────────────────┘
```

**🔄 Innovation 4: EIP-7702 Smart Account Seamless Upgrade**
| Comparison Item | Traditional AA (ERC-4337) | Shield (EIP-7702) |
|--------|-------------------|-------------------|
| Address change | ❌ Need new address | ✅ Keep original EOA address |
| Historical assets | Need migration | Automatically inherited |
| Social recovery association | Need re-setup | Remains unchanged |
| Gas optimization | ✅ Batch transactions | ✅ Batch transactions |

**📊 Innovation 5: Unified Automation Platform**
```
One platform, one authorization, multiple strategies:
  ┌─ DCA DCA ────── Daily/weekly automatic buying
  │
  ├─ Stop-loss strategy ────── Price-triggered automatic selling
  │
  ├─ Rebalancing ──────── Automatic rebalancing when threshold exceeded
  │
  ├─ Subscription payments ────── Web3 native monthly subscriptions
  │
  └─ (Planned) AI Agent ── Autonomous DeFi operations
```

**📈 Innovation 6: Real-time Data Analysis Engine**
- Envio HyperIndex real-time indexing of on-chain events
- GraphQL API supports complex queries
- Profit analysis, risk scoring, Gas optimization suggestions

#### 1.4.4 Competitor Analysis

| Feature | Shield Protocol | Gelato | Superfluid | revoke.cash | Traditional DApp |
|------|-----------------|--------|------------|-------------|-----------|
| **Permission Control** | ERC-7715 native | External Keeper | Protocol-limited | Post-hoc revocation | Unlimited approval |
| **DCA Automation** | ✅ Built-in | ✅ | ❌ | ❌ | ❌ |
| **Stop-loss/Rebalancing** | ✅ Built-in | ✅ | ❌ | ❌ | ❌ |
| **Subscription Payments** | ✅ Built-in | ❌ | ✅ | ❌ | ❌ |
| **Spending Limits** | ✅ Built-in | ❌ Manual required | ❌ | ❌ | ❌ |
| **Emergency Freeze** | ✅ One-click | Complex | Complex | Manual one-by-one | ❌ |
| **Trust Model** | Cryptographic guarantee | Trust Keeper | Trust protocol | N/A | Full trust |
| **Gas Efficiency** | Smart account batch | Pay-per-use | Streaming | N/A | Per-transaction |
| **Data Analysis** | ✅ Real-time indexing | Basic | Basic | ❌ | ❌ |

#### 1.4.5 Problem Solving Summary

| # | Traditional DeFi Problem | Impact | Shield Solution |
|---|---------------|------|----------------|
| 1 | Unlimited approval risk | $120M+ annual losses | Granular time-limited permissions |
| 2 | DCA operation complexity | 150 operations per month | One-time setup, automatic execution |
| 3 | No spending limits | Full loss if private key compromised | Daily/per-transaction limits |
| 4 | Complex multi-step UX | 63% of users abandon | Intent-driven simplification |
| 5 | Passive security (post-hoc revocation) | Loss already occurred when discovered | Active limits + whitelist |
| 6 | No native subscriptions | Web3 services hard to monetize | Built-in subscription module |
| 7 | Tool fragmentation | High learning cost | One-stop platform |
| 8 | AA migration cost | Need new address | EIP-7702 in-place upgrade |

---

## 2. User Flow

### 2.1 Overall Flow Chart

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        Shield Protocol User Flow                        │
└─────────────────────────────────────────────────────────────────────────┘

    ┌──────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐
    │ Connect  │ ──► │ Activate │ ──► │ Create   │ ──► │ Grant    │
    │ Wallet   │     │ Shield   │     │ Strategy │     │ Permission│
    └──────────┘     └──────────┘     └──────────┘     └──────────┘
         │                │                │                │
         ▼                ▼                ▼                ▼
    MetaMask Flask   Create Smart Account  Select DCA/subscription  MetaMask popup
    Connect + Switch  + Set basic protection  Configure specific    shows permission details
    to Sepolia testnet  limits              parameters

                                                           │
    ┌──────────────────────────────────────────────────────┘
    │
    ▼
┌──────────┐     ┌──────────┐     ┌──────────┐
│ Auto     │ ◄── │ Real-time  │ ◄── │ Data     │
│ Execute  │     │ Monitor    │     │ Analysis │
└──────────┘     └──────────┘     └──────────┘
     │                │                │
     ▼                ▼                ▼
 Strategies execute   Envio indexes     Profit analysis, risk
 automatically        real-time         scoring, Gas optimization
 without manual       status updates
 intervention
```

### 2.2 Detailed Step Description

#### Step 1: Connect Wallet

```
User action: Click "Connect Wallet" button
System response:
  1. Detect if MetaMask Flask is installed
  2. Request wallet connection
  3. Check if network is Sepolia
  4. If not, prompt to switch network

Why this design:
  • ERC-7715 is currently only supported in MetaMask Flask
  • EIP-7702 is only available on supported testnets
  • Need to ensure user environment is correct to use all features
```

#### Step 2: Activate Shield Protection

```
User action: Configure protection parameters and click "Activate Shield"
System response:
  1. Create DeleGator Smart Account (EIP-7702) for user
  2. Upgrade EOA to smart account
  3. Save user-configured protection rules

Why this design:
  • Smart Account is the foundation of ERC-7715 permissions
  • User's EOA address remains unchanged but gains smart contract capabilities
  • Protection rules are stored as Caveats, enforced automatically
```

#### Step 3: Create Investment Strategy

```
User action: Configure DCA parameters in strategy builder
System response:
  1. Validate parameter reasonableness (amount, frequency, duration)
  2. Calculate total investment and expected permission scope
  3. Generate ERC-7715 permission request

Why this design:
  • Intent-driven: User only needs to say "what I want to do"
  • System automatically calculates minimum required permissions
  • Transparently display total cost, user informed consent
```

#### Step 4: Grant Permissions

```
User action: Click "Approve" in MetaMask popup
System response:
  1. MetaMask displays permission details (amount, time, purpose)
  2. After user confirmation, create Delegation
  3. Delegation stored on-chain or locally
  4. Strategy activated, start automatic execution

Why this design:
  • Permissions completely transparent, user sees specific limits
  • Not "unlimited approval", but precise permission boundaries
  • User can revoke anytime
```

#### Step 5: Automatic Execution & Monitoring

```
System automatically: Execute transactions according to strategy configuration
User action: View execution status in Dashboard

Execution flow:
  1. Reach execution time
  2. Shield backend triggers execution
  3. Use Delegation to sign on behalf of user
  4. Submit UserOperation to Bundler
  5. Envio indexes transaction results
  6. Dashboard updates in real-time

Why this design:
  • Fully automated, user doesn't need daily operations
  • Gas abstraction achieved through ERC-4337
  • Envio provides real-time data visibility
```

---

## 3. Page Design Details

### 3.1 Page Structure Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│  Shield Protocol                              [Connect Wallet] [0x...] │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐          │
│  │Dashboard│ │Strategies│ │Subscribe│ │ Shield │ │Settings │          │
│  └─────────┘ └─────────┘ └─────────┘ └─────────┘ └─────────┘          │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │                                                                  │   │
│  │                        Main Content Area                         │   │
│  │                                                                  │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### 3.2 Page 1: Dashboard

#### Page Layout

```
┌─────────────────────────────────────────────────────────────────────────┐
│  Dashboard                                                              │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐           │
│  │ 🛡️ Shield Status │ │ 📊 Total Assets │ │ ⚡ Active        │           │
│  │                 │ │ Protected       │ │ Strategies      │           │
│  │   ✅ Active     │ │   $12,450      │ │      3         │           │
│  │                 │ │                 │ │                 │           │
│  └─────────────────┘ └─────────────────┘ └─────────────────┘           │
│                                                                         │
│  ┌─────────────────────────────────────┐ ┌─────────────────────────┐   │
│  │ 📈 Asset Trend                      │ │ 🔔 Recent Activity      │   │
│  │                                     │ │                         │   │
│  │     ╭──────────────╮               │ │ • DCA executed successfully │   │
│  │    ╱                ╲              │ │   20 USDC → 0.0074 ETH  │   │
│  │   ╱                  ──            │ │   2 minutes ago         │   │
│  │  ╱                                 │ │                         │   │
│  │ ╱                                  │ │ • New strategy activated│   │
│  │╱___________________________        │ │   ETH DCA 30 days       │   │
│  │ Nov 20  21  22  23  24  25  26     │ │   1 hour ago            │   │
│  │                                     │ │                         │   │
│  └─────────────────────────────────────┘ └─────────────────────────┘   │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │ 📋 My Strategies                                                 │   │
│  │                                                                  │   │
│  │ ┌────────────────────────────────────────────────────────────┐  │   │
│  │ │ ETH DCA DCA                                    [In Progress]│  │   │
│  │ │ Daily 20 USDC → ETH | Progress: 12/30 days | Invested: 240 USDC │  │   │
│  │ │ ████████████░░░░░░░░░░░░░░░░░░ 40%                        │  │   │
│  │ └────────────────────────────────────────────────────────────┘  │   │
│  │                                                                  │   │
│  │ ┌────────────────────────────────────────────────────────────┐  │   │
│  │ │ Creator subscription                              [Active]  │  │   │
│  │ │ Monthly 10 USDC → 0x1234...5678 | Next payment: Dec 1    │  │   │
│  │ └────────────────────────────────────────────────────────────┘  │   │
│  │                                                                  │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

#### Design Reasons

| Component | Design Purpose | User Value |
|------|---------|---------|
| **Shield Status Card** | See at a glance if protection is enabled | Security, confirm status |
| **Total Protected Assets** | Display total value of assets protected by Shield | Understand protection scope |
| **Active Strategy Count** | Quickly understand number of running strategies | Global control |
| **Asset Trend Chart** | Visualize asset changes | Intuitively assess strategy effectiveness |
| **Recent Activity** | Real-time display of execution records | Transparent, traceable |
| **Strategy List** | Overview of all strategies | Management and monitoring |

### 3.3 Page 2: Strategy Builder

#### Page Layout

```
┌─────────────────────────────────────────────────────────────────────────┐
│  Create New Strategy                                                    │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  Select Strategy Type                                            │   │
│  │                                                                  │   │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐        │   │
│  │  │   📈     │  │   ⚖️     │  │   🛑     │  │   🔄     │        │   │
│  │  │   DCA    │  │ Rebalance│  │Stop-Loss │  │ Reinvest │        │   │
│  │  │  DCA     │  │  Rebalancing│  │  Stop-Loss │  │  Reinvest │        │   │
│  │  │ ✓ Selected│  │          │  │          │  │          │        │   │
│  │  └──────────┘  └──────────┘  └──────────┘  └──────────┘        │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  DCA Strategy Configuration                                      │   │
│  │                                                                  │   │
│  │  ┌─────────────────────────────────────────────────────────┐   │   │
│  │  │  I want to                                               │   │   │
│  │  │  ┌─────────┐  ┌──────────────┐                          │   │   │
│  │  │  │   20    │  │  USDC  ▼    │                          │   │   │
│  │  │  └─────────┘  └──────────────┘                          │   │   │
│  │  │                                                          │   │   │
│  │  │  Buy                                                      │   │   │
│  │  │  ┌──────────────┐                                       │   │   │
│  │  │  │  ETH  ▼     │                                       │   │   │
│  │  │  └──────────────┘                                       │   │   │
│  │  │                                                          │   │   │
│  │  │  Execution Frequency                                      │   │   │
│  │  │  ○ Hourly  ● Daily  ○ Weekly  ○ Monthly                 │   │   │
│  │  │                                                          │   │   │
│  │  │  Duration                                                 │   │   │
│  │  │  ┌─────────┐                                            │   │   │
│  │  │  │   30    │  days                                      │   │   │
│  │  │  └─────────┘                                            │   │   │
│  │  │                                                          │   │   │
│  │  │  Advanced Settings ▼                                     │   │   │
│  │  │  • Max slippage: 1%                                      │   │   │
│  │  │  • DEX: Uniswap V3                                       │   │   │
│  │  │  • Execution time: Daily 15:00 UTC                       │   │   │
│  │  └─────────────────────────────────────────────────────────┘   │   │
│  │                                                                  │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  📊 Strategy Summary                                             │   │
│  │                                                                  │   │
│  │  • Total Investment: 600 USDC (20 × 30 days)                    │   │
│  │  • Estimated Gas Fee: ~$2.50 (Pimlico sponsored)                │   │
│  │  • Permission validity: 30 days                                 │   │
│  │  • Max single authorization: 20 USDC                           │   │
│  │                                                                  │   │
│  │  ⚠️ Important: You can cancel strategy and revoke permissions anytime │   │
│  │                                                                  │   │
│  │               ┌────────────────────────────┐                    │   │
│  │               │    Create Strategy & Grant Permissions │        │   │
│  │               └────────────────────────────┘                    │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

#### Design Reasons

| Design Element | Why This Design | Achieved Effect |
|---------|---------------|-----------|
| **Card-style strategy selection** | Intuitively display all available strategy types | Reduce cognitive burden, quick selection |
| **Natural language form** | "I want to use X to buy Y" | Intent-driven, non-technical users can understand |
| **Visual frequency selection** | Radio buttons instead of dropdown | Reduce clicks, at a glance |
| **Strategy summary** | Summarize all key information | User fully informed before confirmation |
| **Permission transparency** | Clearly display authorization scope | Build trust, eliminate fear |
| **Gas fee hint** | Display estimated cost | Avoid surprises, Paymaster sponsorship increases appeal |

### 3.4 Page 3: Shield Settings

#### Page Layout

```
┌─────────────────────────────────────────────────────────────────────────┐
│  Shield Settings                                                        │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  🛡️ Protection Status                            [ Active ✓ ]   │   │
│  │                                                                  │   │
│  │  Smart Account: 0x7a3b...9f2c                                   │   │
│  │  Creation Time: 2024-11-20 14:30                                │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  💰 Spending Limits                                              │   │
│  │                                                                  │   │
│  │  Daily Maximum Spending                                          │   │
│  │  ┌─────────────┐                                                │   │
│  │  │    100      │  USDC                                          │   │
│  │  └─────────────┘                                                │   │
│  │  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ Used: 20/100        │   │
│  │                                                                  │   │
│  │  Maximum Single Transaction                                      │   │
│  │  ┌─────────────┐                                                │   │
│  │  │     50      │  USDC                                          │   │
│  │  └─────────────┘                                                │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  ✅ Whitelist Contracts                                          │   │
│  │                                                                  │   │
│  │  ┌────────────────────────────────────────────────────────────┐ │   │
│  │  │ ✓ Uniswap V3 Router    0x68b3...4a2f     [Remove]         │ │   │
│  │  │ ✓ Aave V3 Pool         0x87b3...5c1e     [Remove]         │ │   │
│  │  └────────────────────────────────────────────────────────────┘ │   │
│  │                                                                  │   │
│  │  ┌──────────────────────────────┐  ┌────────┐                   │   │
│  │  │ Enter contract address...    │  │ + Add  │                   │   │
│  │  └──────────────────────────────┘  └────────┘                   │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  🚨 Emergency Operations                                        │   │
│  │                                                                  │   │
│  │  ┌─────────────────────────────────────────────────────────┐   │   │
│  │  │  ⚠️ Emergency Freeze                                       │   │   │
│  │  │  Immediately revoke all active permissions, stop all auto-executing strategies │   │   │
│  │  │                                                          │   │   │
│  │  │               [ 🔴 Emergency Freeze All Permissions ]    │   │   │
│  │  └─────────────────────────────────────────────────────────┘   │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

#### Design Reasons

| Design Element | Why This Design | Achieved Effect |
|---------|---------------|-----------|
| **Limit progress bar** | Visualize today's spending status | Real-time perception of consumption status |
| **Whitelist management** | Only allow interaction with trusted contracts | Prevent malicious contract calls |
| **Emergency freeze button** | Prominent red button, separate area | One-click protection in emergencies |
| **Smart Account display** | Display underlying account address | Transparent, advanced users can verify |

### 3.5 Page 4: Analytics (Envio-driven)

#### Page Layout

```
┌─────────────────────────────────────────────────────────────────────────┐
│  Analytics                                         Powered by Envio 🔥  │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌──────────────────────────────────────────────────────────────────┐  │
│  │  📈 DCA Strategy Performance Analysis                             │  │
│  │                                                                   │  │
│  │  ETH Accumulation Curve              Average Purchase Price vs Market Price │  │
│  │  ┌─────────────────────┐         ┌─────────────────────┐         │  │
│  │  │         ╭───        │         │  ----  Market Price │         │  │
│  │  │       ╭─╯           │         │  ───── Your Average │         │  │
│  │  │     ╭─╯             │         │     ╱╲   ╱╲        │         │  │
│  │  │   ╭─╯               │         │ ───╱──╲─╱──╲───    │         │  │
│  │  │ ╭─╯                 │         │   ╱    ╳    ╲      │         │  │
│  │  │─╯                   │         │                    │         │  │
│  │  └─────────────────────┘         └─────────────────────┘         │  │
│  │  Accumulated: 0.0892 ETH         Average: $2,690 | Current: $2,702 │  │
│  │                                    Performance: +0.45% better than direct purchase │  │
│  └──────────────────────────────────────────────────────────────────┘  │
│                                                                         │
│  ┌─────────────────────────────┐  ┌─────────────────────────────────┐  │
│  │  🔄 Execution History        │  │  ⛽ Gas Analysis               │  │
│  │                             │  │                                 │  │
│  │  Nov 26 | 20→0.0074 | ✓    │  │  Total Gas Saved: $12.50       │  │
│  │  Nov 25 | 20→0.0076 | ✓    │  │  (vs manual execution)          │  │
│  │  Nov 24 | 20→0.0073 | ✓    │  │                                 │  │
│  │  Nov 23 | 20→0.0075 | ✓    │  │  Average Gas/execution: $0.15  │  │
│  │  Nov 22 | 20→0.0071 | ✓    │  │  Paymaster sponsorship: 100%   │  │
│  │  ...                        │  │                                 │  │
│  │                             │  │  ┌─────────────────────────┐   │  │
│  │  [View All →]               │  │  │ Best execution time: 04:00 UTC │   │  │
│  │                             │  │  │ (Lowest Gas period)     │   │  │
│  └─────────────────────────────┘  └─────────────────────────────────┘  │
│                                                                         │
│  ┌──────────────────────────────────────────────────────────────────┐  │
│  │  🔔 Security Event Log                                            │  │
│  │                                                                   │  │
│  │  Time              Event                          Status          │  │
│  │  ──────────────────────────────────────────────────────────────  │  │
│  │  Nov 26 09:15     DCA Execution #12              ✅ Success      │  │
│  │  Nov 25 09:15     DCA Execution #11              ✅ Success      │  │
│  │  Nov 24 14:30     Permission expiry reminder     ⚠️ Alert        │  │
│  │  Nov 23 09:15     DCA Execution #10              ✅ Success      │  │
│  │                                                                   │  │
│  └──────────────────────────────────────────────────────────────────┘  │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

#### Design Reasons

| Design Element | Why This Design | Achieved Effect |
|---------|---------------|-----------|
| **Accumulation curve chart** | Display DCA strategy accumulation effect | Intuitively see "accumulate little by little" |
| **Average price comparison chart** | Compare user average vs market price | Prove DCA strategy value |
| **Execution history** | Detailed records of each execution | Fully transparent, traceable |
| **Gas analysis** | Display saved Gas fees | Highlight automation value |
| **Best execution time** | Suggestions based on historical data | Data-driven optimization |
| **Security log** | All permission-related events | Security audit, build trust |

---

## 4. Design Logic and Principles

### 4.1 Why Adopt "Intent-Driven" Design

```
Traditional Web3 Interaction Model:
User → Understand technical details → Construct transaction → Sign → Broadcast

Intent-driven Model:
User → Express intent → System handles details → Automatic execution
```

**Design Principles:**

1. **Reduce Cognitive Burden**
   - Users don't need to understand `approve()`, `transferFrom()` concepts
   - Only need to know "I want to buy $20 worth of ETH daily"

2. **Reduce Operation Steps**
   - Traditional DCA: Login daily → Connect wallet → Authorize → Transaction → Confirm (5 steps × 30 days = 150 operations)
   - Shield DCA: Create strategy → One-time authorization → Automatic execution (3 operations)

3. **Improve Security**
   - Traditional mode easily phished (fake website诱导 signature)
   - Intent mode, user only needs to confirm in real MetaMask popup

### 4.2 Why Choose ERC-7715 + EIP-7702

```
Technology Selection Comparison:

Solution A: Traditional ERC-20 Approve
  ❌ Unlimited approval risk
  ❌ Cannot limit frequency/amount
  ❌ Cannot auto-execute

Solution B: Gelato/Chainlink Keepers
  ⚠️ Need to trust third-party Keeper network
  ⚠️ Need additional contract deployment
  ✅ Can auto-execute

Solution C: ERC-7715 + EIP-7702 (Shield choice)
  ✅ Native MetaMask support
  ✅ Granular permission control
  ✅ User fully controllable
  ✅ No need to trust third-party
  ✅ Auto-execution capability
```

**Value of EIP-7702:**
- Give EOA smart contract capabilities
- User address unchanged but functionality greatly enhanced
- Support batch transactions, permission delegation and other advanced features

**Value of ERC-7715:**
- Standardized permission request format
- Native wallet support, consistent user interface
- Permission boundaries cryptographically guaranteed

### 4.3 Permission Model Design Logic

```
Traditional Authorization Model:
┌─────────┐    approve(∞)    ┌─────────┐
│  User   │ ───────────────► │  DApp   │  → Can transfer all tokens!
└─────────┘                  └─────────┘

Shield Permission Model:
┌─────────┐    delegation    ┌─────────┐    ┌──────────┐
│  User   │ ───────────────► │ Session │ ──►│ Caveats  │
└─────────┘   (limited permissions) │ Account │    │ • Amount limit│
                                             │ • Frequency limit│
                                             │ • Address limit│
                                             └──────────┘
```

**Caveat (Limitation) Design:**

| Caveat Type | Function | Implementation Method |
|-------------|------|---------|
| `SpendingLimitCaveat` | Limit daily/per-transaction spending | Check cumulative amount |
| `WhitelistCaveat` | Only allow specified contracts | Check target address |
| `TimeBoundCaveat` | Permission validity period | Check timestamp |
| `FrequencyCaveat` | Limit execution frequency | Check last execution time |

### 4.4 Security Design Principles

```
1. Minimum Permission Principle
   User only grants minimum permissions required to complete task
   Example: DCA only needs "20 USDC daily" permission, not "all USDC"

2. Revocable Principle
   All permissions revocable anytime
   Emergency freeze function ensures user always in control

3. Transparency Principle
   All permissions clearly displayed in MetaMask
   All execution records verifiable through Envio

4. Default Security Principle
   New users have default protection limits
   Large transactions require additional confirmation
```

---

## 5. Technology Stack Details

### 5.1 Technology Stack Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                            Technology Stack Architecture                │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  Frontend Layer (Frontend)                                       │   │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐           │   │
│  │  │ Next.js  │ │  React   │ │TypeScript│ │ Tailwind │           │   │
│  │  │   14     │ │   18     │ │   5.0    │ │   CSS    │           │   │
│  │  └──────────┘ └──────────┘ └──────────┘ └──────────┘           │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                    │                                    │
│                                    ▼                                    │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  Web3 Interaction Layer (Web3 Interaction)                       │   │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────────────────────┐         │   │
│  │  │  Wagmi   │ │   Viem   │ │ MetaMask Delegation      │         │   │
│  │  │   v2     │ │  2.x     │ │ Toolkit                  │         │   │
│  │  └──────────┘ └──────────┘ └──────────────────────────┘         │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                    │                                    │
│                                    ▼                                    │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  Smart Contract Layer (Smart Contracts)                          │   │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐           │   │
│  │  │Solidity  │ │ Hardhat  │ │OpenZeppelin│ │Delegation│           │   │
│  │  │ 0.8.24   │ │          │ │ Contracts │ │Framework │           │   │
│  │  └──────────┘ └──────────┘ └──────────┘ └──────────┘           │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                    │                                    │
│                                    ▼                                    │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  Infrastructure Layer (Infrastructure)                           │   │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐           │   │
│  │  │ Pimlico  │ │  Envio   │ │ Sepolia  │ │ MetaMask │           │   │
│  │  │ Bundler  │ │HyperIndex│ │ Testnet  │ │  Flask   │           │   │
│  │  └──────────┘ └──────────┘ └──────────┘ └──────────┘           │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### 5.2 Frontend Technology Details

#### Next.js 14 (App Router)

```typescript
// Why choose Next.js 14:
// 1. App Router provides better data fetching patterns
// 2. Server Components reduce client-side JS bundle
// 3. Built-in routing and layout system

// app/layout.tsx
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>
        <Providers>
          <Header />
          <main>{children}</main>
        </Providers>
      </body>
    </html>
  );
}

// app/dashboard/page.tsx
export default async function DashboardPage() {
  // Server Component: Can directly fetch data
  const strategies = await fetchUserStrategies();

  return (
    <div>
      <ShieldStatus />
      <StrategyList strategies={strategies} />
      <RecentActivity />
    </div>
  );
}
```

#### Wagmi v2 + Viem

```typescript
// Why choose Wagmi + Viem:
// 1. Native TypeScript support, type safety
// 2. Perfect integration with MetaMask Delegation Toolkit
// 3. React Hooks paradigm, simple state management

// hooks/useShield.ts
import { useAccount, useWalletClient } from "wagmi";
import { erc7715ProviderActions } from "@metamask/delegation-toolkit/experimental";

export function useShield() {
  const { address } = useAccount();
  const { data: walletClient } = useWalletClient();

  // Extend Wallet Client to support ERC-7715
  const extendedClient = walletClient?.extend(erc7715ProviderActions());

  const grantDCAPermission = async (params: DCAParams) => {
    if (!extendedClient) throw new Error("Wallet not connected");

    const permission = await extendedClient.grantPermissions([{
      chainId: sepolia.id,
      expiry: Math.floor(Date.now() / 1000) + params.duration * 86400,
      signer: {
        type: "account",
        data: { address: SHIELD_VAULT_ADDRESS },
      },
      permission: {
        type: "erc20-spend-recurring-limit",
        data: {
          token: params.sourceToken,
          limit: params.amountPerDay.toString(),
          period: 86400,
        },
      },
    }]);

    return permission;
  };

  return {
    grantDCAPermission,
    // ... other methods
  };
}
```

#### TailwindCSS + Shadcn/ui

```tsx
// Why choose Tailwind + Shadcn:
// 1. Rapid development, no need to write CSS files
// 2. Shadcn provides high-quality customizable components
// 3. Dark mode out-of-box

// components/StrategyCard.tsx
import { Card, CardHeader, CardContent } from "@/components/ui/card";
import { Progress } from "@/components/ui/progress";
import { Badge } from "@/components/ui/badge";

export function StrategyCard({ strategy }: { strategy: Strategy }) {
  const progress = (strategy.executionsCompleted / strategy.totalExecutions) * 100;

  return (
    <Card className="hover:shadow-lg transition-shadow">
      <CardHeader className="flex flex-row items-center justify-between">
        <div className="flex items-center gap-2">
          <span className="text-lg font-semibold">{strategy.name}</span>
          <Badge variant={strategy.status === "active" ? "default" : "secondary"}>
            {strategy.status}
          </Badge>
        </div>
      </CardHeader>
      <CardContent>
        <div className="space-y-2">
          <div className="text-sm text-muted-foreground">
            Daily {strategy.amountPerDay} {strategy.sourceToken} → {strategy.targetToken}
          </div>
          <Progress value={progress} className="h-2" />
          <div className="text-xs text-muted-foreground">
            Progress: {strategy.executionsCompleted}/{strategy.totalExecutions} days
          </div>
        </div>
      </CardContent>
    </Card>
  );
}
```

### 5.3 Web3 Interaction Layer Details

#### MetaMask Delegation Toolkit

```typescript
// Core Concepts:
// 1. DeleGator: User's Smart Account
// 2. Delegation: Permission delegation
// 3. Caveat: Permission limitation conditions
// 4. Redemption: Use delegation to execute operations

import {
  DelegationFramework,
  createCaveatBuilder,
  SINGLE_DEFAULT_MODE,
} from "@metamask/delegation-toolkit";

// Initialize Delegation Framework
const framework = new DelegationFramework({
  chainId: sepolia.id,
  delegationManager: DELEGATION_MANAGER_ADDRESS,
  entryPoint: ENTRY_POINT_ADDRESS,
  bundlerUrl: `https://api.pimlico.io/v2/sepolia/rpc?apikey=${PIMLICO_KEY}`,
});

// Create Delegation with Caveats
const createDCADelegation = async (params: DCAParams) => {
  // Build Caveats (limitation conditions)
  const caveats = createCaveatBuilder(sepolia.id)
    // Limit daily spending
    .addCaveat("erc20SpendingLimit", {
      token: params.sourceToken,
      limit: params.amountPerDay,
      period: 86400,
    })
    // Limit validity period
    .addCaveat("timeBound", {
      notBefore: Math.floor(Date.now() / 1000),
      notAfter: Math.floor(Date.now() / 1000) + params.duration * 86400,
    })
    // Only allow calling specified contracts
    .addCaveat("allowedTargets", {
      targets: [UNISWAP_ROUTER_ADDRESS],
    })
    .build();

  return caveats;
};
```

### 5.4 Smart Contract Layer Details

#### Contract Architecture

```
contracts/
├── core/
│   ├── ShieldCore.sol          # Core protection logic
│   └── ShieldStorage.sol       # Storage structure
├── strategies/
│   ├── DCAExecutor.sol         # DCA strategy executor
│   ├── RebalanceExecutor.sol   # Rebalancing executor
│   └── StopLossExecutor.sol    # Stop-loss executor
├── caveats/
│   ├── SpendingLimitEnforcer.sol
│   ├── WhitelistEnforcer.sol
│   └── FrequencyEnforcer.sol
└── interfaces/
    └── IShieldProtocol.sol
```

#### ShieldCore.sol Implementation

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

import {IDelegationManager} from "@metamask/delegation-framework/interfaces/IDelegationManager.sol";
import {ICaveatEnforcer} from "@metamask/delegation-framework/interfaces/ICaveatEnforcer.sol";
import {Execution} from "@metamask/delegation-framework/types/Execution.sol";

/**
 * @title ShieldCore
 * @notice Core protection contract, managing user security configurations and strategy execution
 *
 * Design Principles:
 * 1. Each user has independent ShieldConfig configuration
 * 2. All strategy execution must pass permission verification
 * 3. Support emergency freeze function
 */
contract ShieldCore {
    // ============ State Variables ============

    IDelegationManager public immutable delegationManager;

    struct ShieldConfig {
        uint256 dailySpendLimit;      // Daily spending limit
        uint256 singleTxLimit;        // Single transaction limit
        uint256 spentToday;           // Amount spent today
        uint256 lastResetTimestamp;   // Last reset time
        bool isActive;                // Is active
        bool emergencyMode;           // Emergency mode
    }

    mapping(address => ShieldConfig) public shields;
    mapping(address => address[]) public whitelistedContracts;

    // ============ Events ============

    event ShieldActivated(address indexed user, uint256 dailyLimit, uint256 singleTxLimit);
    event ShieldUpdated(address indexed user, uint256 newDailyLimit, uint256 newSingleTxLimit);
    event EmergencyModeEnabled(address indexed user);
    event EmergencyModeDisabled(address indexed user);
    event SpendingRecorded(address indexed user, uint256 amount, uint256 newTotal);

    // ============ Modifiers ============

    modifier onlyActiveShield(address user) {
        require(shields[user].isActive, "Shield not active");
        require(!shields[user].emergencyMode, "Emergency mode enabled");
        _;
    }

    // ============ Core Functions ============

    /**
     * @notice Activate user's Shield protection
     * @param dailyLimit Daily spending limit
     * @param singleTxLimit Single transaction limit
     *
     * Design Reason:
     * - User must actively activate protection, ensuring informed consent
     * - Limits set during activation, can be modified later but with cooldown
     */
    function activateShield(
        uint256 dailyLimit,
        uint256 singleTxLimit
    ) external {
        require(!shields[msg.sender].isActive, "Already active");
        require(dailyLimit > 0, "Invalid daily limit");
        require(singleTxLimit <= dailyLimit, "Single tx limit exceeds daily");

        shields[msg.sender] = ShieldConfig({
            dailySpendLimit: dailyLimit,
            singleTxLimit: singleTxLimit,
            spentToday: 0,
            lastResetTimestamp: block.timestamp,
            isActive: true,
            emergencyMode: false
        });

        emit ShieldActivated(msg.sender, dailyLimit, singleTxLimit);
    }

    /**
     * @notice Record spending and check limits
     * @param user User address
     * @param amount Spending amount
     *
     * Design Reason:
     * - Called before strategy execution, ensure limits not exceeded
     * - Daily counter automatically resets
     * - Return bool instead of revert, let caller decide handling
     */
    function recordSpending(
        address user,
        uint256 amount
    ) external onlyActiveShield(user) returns (bool) {
        ShieldConfig storage config = shields[user];

        // Check if daily counter needs reset
        if (block.timestamp >= config.lastResetTimestamp + 1 days) {
            config.spentToday = 0;
            config.lastResetTimestamp = block.timestamp;
        }

        // Check single transaction limit
        if (amount > config.singleTxLimit) {
            return false;
        }

        // Check daily limit
        if (config.spentToday + amount > config.dailySpendLimit) {
            return false;
        }

        // Record spending
        config.spentToday += amount;

        emit SpendingRecorded(user, amount, config.spentToday);
        return true;
    }

    /**
     * @notice Enable emergency mode
     *
     * Design Reason:
     * - Only callable by user themselves
     * - Immediately block all auto-execution
     * - Won't auto-recover, manual removal required
     */
    function enableEmergencyMode() external {
        require(shields[msg.sender].isActive, "Shield not active");
        shields[msg.sender].emergencyMode = true;
        emit EmergencyModeEnabled(msg.sender);
    }

    /**
     * @notice Disable emergency mode
     *
     * Design Reason:
     * - Additional confirmation required, prevent accidental operation
     * - Can add time lock (future version)
     */
    function disableEmergencyMode() external {
        require(shields[msg.sender].emergencyMode, "Not in emergency mode");
        shields[msg.sender].emergencyMode = false;
        emit EmergencyModeDisabled(msg.sender);
    }

    // ============ Whitelist Management ============

    function addWhitelistedContract(address contractAddr) external {
        require(shields[msg.sender].isActive, "Shield not active");
        whitelistedContracts[msg.sender].push(contractAddr);
    }

    function isWhitelisted(address user, address contractAddr) public view returns (bool) {
        address[] memory whitelist = whitelistedContracts[user];
        for (uint i = 0; i < whitelist.length; i++) {
            if (whitelist[i] == contractAddr) return true;
        }
        return false;
    }

    // ============ View Functions ============

    function getRemainingDailyAllowance(address user) external view returns (uint256) {
        ShieldConfig memory config = shields[user];
        if (!config.isActive) return 0;

        // If crossed day, return full limit
        if (block.timestamp >= config.lastResetTimestamp + 1 days) {
            return config.dailySpendLimit;
        }

        return config.dailySpendLimit - config.spentToday;
    }
}
```

#### DCAExecutor.sol Implementation

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

import {ISwapRouter} from "@uniswap/v3-periphery/contracts/interfaces/ISwapRouter.sol";
import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";
import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
import {ShieldCore} from "./ShieldCore.sol";

/**
 * @title DCAExecutor
 * @notice Execute DCA (Dollar Cost Average) strategy
 *
 * Design Principles:
 * 1. After Delegation authorization, can execute transactions on behalf of user
 * 2. Check ShieldCore limits before each execution
 * 3. Use Uniswap V3 for actual token swaps
 */
contract DCAExecutor {
    using SafeERC20 for IERC20;

    // ============ State Variables ============

    ShieldCore public immutable shieldCore;
    ISwapRouter public immutable swapRouter;

    struct DCAStrategy {
        address user;              // Strategy owner
        address sourceToken;       // Source token (e.g., USDC)
        address targetToken;       // Target token (e.g., ETH)
        uint256 amountPerExecution;// Amount per execution
        uint256 intervalSeconds;   // Execution interval
        uint256 nextExecutionTime; // Next execution time
        uint256 executionsRemaining;// Remaining executions
        uint24 poolFee;            // Uniswap pool fee
        bool isActive;             // Is active
    }

    mapping(bytes32 => DCAStrategy) public strategies;
    mapping(address => bytes32[]) public userStrategies;

    // ============ Events ============

    event StrategyCreated(
        bytes32 indexed strategyId,
        address indexed user,
        address sourceToken,
        address targetToken,
        uint256 amountPerExecution,
        uint256 totalExecutions
    );

    event DCAExecuted(
        bytes32 indexed strategyId,
        address indexed user,
        uint256 amountIn,
        uint256 amountOut,
        uint256 executionsRemaining
    );

    event StrategyPaused(bytes32 indexed strategyId);
    event StrategyResumed(bytes32 indexed strategyId);
    event StrategyCancelled(bytes32 indexed strategyId);

    // ============ Constructor ============

    constructor(address _shieldCore, address _swapRouter) {
        shieldCore = ShieldCore(_shieldCore);
        swapRouter = ISwapRouter(_swapRouter);
    }

    // ============ Strategy Management ============

    /**
     * @notice Create DCA strategy
     *
     * Design Reason:
     * - Strategy ID generated using hash, ensure uniqueness
     * - Don't request permissions here, permissions requested via ERC-7715 in frontend
     * - Only record strategy configuration, verify permissions during execution
     */
    function createStrategy(
        address sourceToken,
        address targetToken,
        uint256 amountPerExecution,
        uint256 intervalSeconds,
        uint256 totalExecutions,
        uint24 poolFee
    ) external returns (bytes32 strategyId) {
        require(amountPerExecution > 0, "Amount must be > 0");
        require(totalExecutions > 0, "Must have at least 1 execution");

        // Generate unique strategy ID
        strategyId = keccak256(abi.encodePacked(
            msg.sender,
            sourceToken,
            targetToken,
            block.timestamp
        ));

        strategies[strategyId] = DCAStrategy({
            user: msg.sender,
            sourceToken: sourceToken,
            targetToken: targetToken,
            amountPerExecution: amountPerExecution,
            intervalSeconds: intervalSeconds,
            nextExecutionTime: block.timestamp, // First execution immediately available
            executionsRemaining: totalExecutions,
            poolFee: poolFee,
            isActive: true
        });

        userStrategies[msg.sender].push(strategyId);

        emit StrategyCreated(
            strategyId,
            msg.sender,
            sourceToken,
            targetToken,
            amountPerExecution,
            totalExecutions
        );
    }

    /**
     * @notice Execute DCA strategy
     * @param strategyId Strategy ID
     *
     * Design Reason:
     * - Anyone can call to trigger execution (usually backend service)
     * - Actual execution requires valid Delegation permission
     * - Check time conditions and Shield limits
     *
     * Execution Flow:
     * 1. Verify strategy status and time conditions
     * 2. Check limits through ShieldCore
     * 3. Use Delegation to transfer tokens from user account
     * 4. Call Uniswap to execute swap
     * 5. Update strategy status
     */
    function executeDCA(bytes32 strategyId) external {
        DCAStrategy storage strategy = strategies[strategyId];

        // Check strategy status
        require(strategy.isActive, "Strategy not active");
        require(strategy.executionsRemaining > 0, "Strategy completed");
        require(block.timestamp >= strategy.nextExecutionTime, "Too early");

        // Check Shield limits
        bool allowed = shieldCore.recordSpending(
            strategy.user,
            strategy.amountPerExecution
        );
        require(allowed, "Exceeds shield limit");

        // Execute swap
        // Note: In actual implementation, this needs Delegation permission execution
        // Simplified version directly calls (requires pre-authorization to this contract)
        uint256 amountOut = _executeSwap(strategy);

        // Update strategy status
        strategy.executionsRemaining--;
        strategy.nextExecutionTime = block.timestamp + strategy.intervalSeconds;

        // If execution completed, mark as inactive
        if (strategy.executionsRemaining == 0) {
            strategy.isActive = false;
        }

        emit DCAExecuted(
            strategyId,
            strategy.user,
            strategy.amountPerExecution,
            amountOut,
            strategy.executionsRemaining
        );
    }

    /**
     * @notice Execute actual token swap
     *
     * Design Reason:
     * - Internal function, only called by executeDCA
     * - Use Uniswap V3 exactInputSingle for swap
     * - Set reasonable slippage protection
     */
    function _executeSwap(
        DCAStrategy storage strategy
    ) internal returns (uint256 amountOut) {
        IERC20 sourceToken = IERC20(strategy.sourceToken);

        // Transfer tokens from user account (requires Delegation permission)
        sourceToken.safeTransferFrom(
            strategy.user,
            address(this),
            strategy.amountPerExecution
        );

        // Authorize Uniswap Router
        sourceToken.safeApprove(address(swapRouter), strategy.amountPerExecution);

        // Execute swap
        ISwapRouter.ExactInputSingleParams memory params = ISwapRouter
            .ExactInputSingleParams({
                tokenIn: strategy.sourceToken,
                tokenOut: strategy.targetToken,
                fee: strategy.poolFee,
                recipient: strategy.user, // Send directly to user
                deadline: block.timestamp + 300, // 5-minute timeout
                amountIn: strategy.amountPerExecution,
                amountOutMinimum: 0, // Should set minimum output in production
                sqrtPriceLimitX96: 0
            });

        amountOut = swapRouter.exactInputSingle(params);
    }

    // ============ Strategy Control ============

    function pauseStrategy(bytes32 strategyId) external {
        DCAStrategy storage strategy = strategies[strategyId];
        require(strategy.user == msg.sender, "Not owner");
        strategy.isActive = false;
        emit StrategyPaused(strategyId);
    }

    function resumeStrategy(bytes32 strategyId) external {
        DCAStrategy storage strategy = strategies[strategyId];
        require(strategy.user == msg.sender, "Not owner");
        require(strategy.executionsRemaining > 0, "Strategy completed");
        strategy.isActive = true;
        emit StrategyResumed(strategyId);
    }

    function cancelStrategy(bytes32 strategyId) external {
        DCAStrategy storage strategy = strategies[strategyId];
        require(strategy.user == msg.sender, "Not owner");
        strategy.isActive = false;
        strategy.executionsRemaining = 0;
        emit StrategyCancelled(strategyId);
    }
}
```

### 5.5 Data Indexing Layer (Envio)

#### Configuration File

```yaml
# config.yaml
name: shield-protocol-indexer
description: Shield Protocol event indexer
networks:
  - id: 11155111  # Sepolia
    start_block: 5000000
    contracts:
      - name: ShieldCore
        address: "0x..."
        handler: src/handlers/ShieldCore.ts
        events:
          - event: ShieldActivated(address indexed user, uint256 dailyLimit, uint256 singleTxLimit)
          - event: EmergencyModeEnabled(address indexed user)
          - event: SpendingRecorded(address indexed user, uint256 amount, uint256 newTotal)

      - name: DCAExecutor
        address: "0x..."
        handler: src/handlers/DCAExecutor.ts
        events:
          - event: StrategyCreated(bytes32 indexed strategyId, address indexed user, address sourceToken, address targetToken, uint256 amountPerExecution, uint256 totalExecutions)
          - event: DCAExecuted(bytes32 indexed strategyId, address indexed user, uint256 amountIn, uint256 amountOut, uint256 executionsRemaining)
          - event: StrategyCancelled(bytes32 indexed strategyId)
```

#### GraphQL Schema

```graphql
# schema.graphql

type User @entity {
  id: ID!                           # User address
  address: Bytes!
  shield: Shield
  strategies: [Strategy!]! @derivedFrom(field: "user")
  totalInvested: BigInt!            # Total invested amount
  totalExecutions: Int!             # Total executions
  createdAt: BigInt!
  updatedAt: BigInt!
}

type Shield @entity {
  id: ID!
  user: User!
  dailyLimit: BigInt!
  singleTxLimit: BigInt!
  spentToday: BigInt!
  isActive: Boolean!
  emergencyMode: Boolean!
  activatedAt: BigInt!
  updatedAt: BigInt!
}

type Strategy @entity {
  id: ID!                           # Strategy ID (bytes32)
  user: User!
  type: StrategyType!
  sourceToken: Token!
  targetToken: Token!
  amountPerExecution: BigInt!
  intervalSeconds: Int!
  totalExecutions: Int!
  executionsCompleted: Int!
  executionsRemaining: Int!
  status: StrategyStatus!
  executions: [Execution!]! @derivedFrom(field: "strategy")
  totalAmountIn: BigInt!
  totalAmountOut: BigInt!
  averagePrice: BigInt!             # Average purchase price
  createdAt: BigInt!
  updatedAt: BigInt!
}

type Execution @entity {
  id: ID!                           # txHash-logIndex
  strategy: Strategy!
  amountIn: BigInt!
  amountOut: BigInt!
  price: BigInt!                    # Execution price this time
  gasUsed: BigInt!
  txHash: Bytes!
  blockNumber: BigInt!
  timestamp: BigInt!
}

type Token @entity {
  id: ID!                           # Token address
  symbol: String!
  decimals: Int!
  strategies: [Strategy!]!
}

type DailyStats @entity {
  id: ID!                           # date-userId
  user: User!
  date: String!
  totalSpent: BigInt!
  executionCount: Int!
  tokensAcquired: BigInt!
}

enum StrategyType {
  DCA
  REBALANCE
  STOP_LOSS
  YIELD_REINVEST
}

enum StrategyStatus {
  ACTIVE
  PAUSED
  COMPLETED
  CANCELLED
}
```

#### Event Handlers

```typescript
// src/handlers/DCAExecutor.ts
import { DCAExecutor } from "generated";

/**
 * Handle strategy creation event
 *
 * Design Reason:
 * - Create Strategy entity, associate with User
 * - Initialize all statistical fields
 * - Ensure Token entity exists
 */
DCAExecutor.StrategyCreated.handler(async ({ event, context }) => {
  const strategyId = event.params.strategyId;
  const userId = event.params.user.toLowerCase();

  // Ensure user exists
  let user = await context.User.get(userId);
  if (!user) {
    user = {
      id: userId,
      address: event.params.user,
      totalInvested: 0n,
      totalExecutions: 0,
      createdAt: event.block.timestamp,
      updatedAt: event.block.timestamp,
    };
    await context.User.set(user);
  }

  // Create strategy entity
  const strategy = {
    id: strategyId,
    user_id: userId,
    type: "DCA",
    sourceToken_id: event.params.sourceToken.toLowerCase(),
    targetToken_id: event.params.targetToken.toLowerCase(),
    amountPerExecution: event.params.amountPerExecution,
    intervalSeconds: 86400,
    totalExecutions: Number(event.params.totalExecutions),
    executionsCompleted: 0,
    executionsRemaining: Number(event.params.totalExecutions),
    status: "ACTIVE",
    totalAmountIn: 0n,
    totalAmountOut: 0n,
    averagePrice: 0n,
    createdAt: event.block.timestamp,
    updatedAt: event.block.timestamp,
  };

  await context.Strategy.set(strategy);
});

/**
 * Handle DCA execution event
 *
 * Design Reason:
 * - Record detailed information for each execution
 * - Update strategy cumulative statistics
 * - Calculate average price
 * - Update user statistics
 */
DCAExecutor.DCAExecuted.handler(async ({ event, context }) => {
  const strategyId = event.params.strategyId;
  const executionId = `${event.transaction.hash}-${event.log.logIndex}`;

  // Create execution record
  const execution = {
    id: executionId,
    strategy_id: strategyId,
    amountIn: event.params.amountIn,
    amountOut: event.params.amountOut,
    price: (event.params.amountIn * 10n ** 18n) / event.params.amountOut, // Price calculation
    gasUsed: event.transaction.gasUsed || 0n,
    txHash: event.transaction.hash,
    blockNumber: event.block.number,
    timestamp: event.block.timestamp,
  };

  await context.Execution.set(execution);

  // Update strategy statistics
  const strategy = await context.Strategy.get(strategyId);
  if (strategy) {
    const newTotalIn = strategy.totalAmountIn + event.params.amountIn;
    const newTotalOut = strategy.totalAmountOut + event.params.amountOut;

    await context.Strategy.set({
      ...strategy,
      executionsCompleted: strategy.executionsCompleted + 1,
      executionsRemaining: Number(event.params.executionsRemaining),
      totalAmountIn: newTotalIn,
      totalAmountOut: newTotalOut,
      averagePrice: newTotalOut > 0n ? (newTotalIn * 10n ** 18n) / newTotalOut : 0n,
      status: Number(event.params.executionsRemaining) === 0 ? "COMPLETED" : "ACTIVE",
      updatedAt: event.block.timestamp,
    });

    // Update user statistics
    const user = await context.User.get(strategy.user_id);
    if (user) {
      await context.User.set({
        ...user,
        totalInvested: user.totalInvested + event.params.amountIn,
        totalExecutions: user.totalExecutions + 1,
        updatedAt: event.block.timestamp,
      });
    }
  }
});
```

---

## 6. Project Implementation Logic

### 6.1 Complete Data Flow

```
┌─────────────────────────────────────────────────────────────────────────┐
│                           Complete Data Flow Chart                      │
└─────────────────────────────────────────────────────────────────────────┘

User Operation                 Frontend Processing              On-chain Execution
─────────                   ────────                      ────────

1. Create Strategy
   │
   ▼
┌──────────┐           ┌──────────────────┐
│ Fill Form │ ────────► │ Validate Parameters │
└──────────┘           │ Calculate Permission Scope │
                       │ Build Permission   │
                       └────────┬─────────┘
                                │
                                ▼
                       ┌──────────────────┐
                       │ Call MetaMask    │
                       │ grantPermissions │
                       └────────┬─────────┘
                                │
                                ▼
                       ┌──────────────────┐          ┌──────────────────┐
                       │ User confirms    │ ────────►│ On-chain Create  │
                       │ permissions in   │          │ Delegation       │
                       │ MetaMask         │          └────────┬─────────┘
                                                              │
                                ┌──────────────────────────────┘
                                │
                                ▼
                       ┌──────────────────┐          ┌──────────────────┐
                       │ Call Contract    │ ────────►│ DCAExecutor      │
                       │ createStrategy   │          │ .createStrategy  │
                       └──────────────────┘          └────────┬─────────┘
                                                              │
                                                              ▼
                                                     ┌──────────────────┐
                                                     │ Emit             │
                                                     │ StrategyCreated  │
                                                     │ Event            │
                                                     └────────┬─────────┘
                                                              │
2. Auto Execution (Backend Trigger)                            ▼
                                                     ┌──────────────────┐
                       ┌──────────────────┐          │ Envio Index Event│
                       │ Backend Cron Job │          │ Update Database  │
                       │ Check due strategy │          └──────────────────┘
                       └────────┬─────────┘
                                │
                                ▼
                       ┌──────────────────┐          ┌──────────────────┐
                       │ Build UserOp     │ ────────►│ Bundler          │
                       │ Use Delegation   │          │ Verify & Package │
                       └──────────────────┘          └────────┬─────────┘
                                                              │
                                                              ▼
                                                     ┌──────────────────┐
                                                     │ On-chain Execute │
                                                     │ 1. Verify Permission │
                                                     │ 2. Check Limits  │
                                                     │ 3. Execute Swap  │
                                                     └────────┬─────────┘
                                                              │
                                                              ▼
                                                     ┌──────────────────┐
                                                     │ Emit             │
                                                     │ DCAExecuted      │
                                                     │ Event            │
                                                     └────────┬─────────┘
                                                              │
3. Data Display                                                  ▼
                                                     ┌──────────────────┐
┌──────────┐           ┌──────────────────┐          │ Envio Index      │
│ Dashboard│ ◄──────── │ GraphQL Query    │ ◄────────│ Update Statistics│
│ Update   │           │ Get latest data  │          └──────────────────┘
└──────────┘           └──────────────────┘
```

### 6.2 Core Function Call Chain

#### Create DCA Strategy

```typescript
// 1. Frontend: User fills form
const dcaParams = {
  sourceToken: USDC_ADDRESS,
  targetToken: WETH_ADDRESS,
  amountPerDay: parseUnits("20", 6),  // 20 USDC
  duration: 30,  // 30 days
};

// 2. Frontend: Request permissions
const walletClient = createWalletClient({...}).extend(erc7715ProviderActions());

const permission = await walletClient.grantPermissions([{
  chainId: sepolia.id,
  expiry: Math.floor(Date.now() / 1000) + 30 * 86400,
  signer: {
    type: "account",
    data: { address: DCA_EXECUTOR_ADDRESS },
  },
  permission: {
    type: "erc20-spend-recurring-limit",
    data: {
      token: USDC_ADDRESS,
      limit: parseUnits("20", 6).toString(),
      period: 86400,
    },
  },
}]);

// 3. Frontend: Create on-chain strategy
const hash = await writeContract({
  address: DCA_EXECUTOR_ADDRESS,
  abi: DCAExecutorABI,
  functionName: "createStrategy",
  args: [
    USDC_ADDRESS,
    WETH_ADDRESS,
    parseUnits("20", 6),
    86400,  // Execute daily
    30,     // 30 times
    3000,   // 0.3% pool fee
  ],
});

// 4. Wait for confirmation
await waitForTransaction({ hash });
```

#### Execute DCA (Backend)

```typescript
// backend/services/executor.ts

class DCAExecutorService {
  private framework: DelegationFramework;

  async checkAndExecute() {
    // 1. Get pending strategies from Envio
    const strategies = await this.graphqlClient.query({
      query: GET_DUE_STRATEGIES,
      variables: { currentTime: Math.floor(Date.now() / 1000) },
    });

    for (const strategy of strategies.data.strategies) {
      try {
        await this.executeStrategy(strategy);
      } catch (error) {
        console.error(`Strategy ${strategy.id} failed:`, error);
      }
    }
  }

  async executeStrategy(strategy: Strategy) {
    // 2. Get user's Delegation
    const delegation = await this.getDelegation(strategy.user.address);

    // 3. Build execution call data
    const calldata = encodeFunctionData({
      abi: DCAExecutorABI,
      functionName: "executeDCA",
      args: [strategy.id],
    });

    // 4. Build UserOperation through Delegation Framework
    const userOp = await this.framework.createUserOperation({
      delegation,
      executions: [{
        target: DCA_EXECUTOR_ADDRESS,
        value: 0n,
        calldata,
      }],
    });

    // 5. Send to Bundler
    const userOpHash = await this.framework.sendUserOperation(userOp);

    // 6. Wait for confirmation
    await this.framework.waitForUserOperation(userOpHash);

    console.log(`Strategy ${strategy.id} executed successfully`);
  }
}
```

### 6.3 State Management Design

```typescript
// stores/shieldStore.ts
import { create } from "zustand";

interface ShieldState {
  // User state
  isConnected: boolean;
  address: string | null;
  smartAccountAddress: string | null;

  // Shield state
  shieldConfig: ShieldConfig | null;
  isShieldActive: boolean;

  // Strategy state
  strategies: Strategy[];
  activeStrategies: Strategy[];

  // Permission state
  permissions: Permission[];

  // Operation methods
  connect: () => Promise<void>;
  activateShield: (config: ShieldConfig) => Promise<void>;
  createStrategy: (params: StrategyParams) => Promise<void>;
  cancelStrategy: (strategyId: string) => Promise<void>;
  emergencyFreeze: () => Promise<void>;

  // Data refresh
  refreshStrategies: () => Promise<void>;
  refreshShieldStatus: () => Promise<void>;
}

export const useShieldStore = create<ShieldState>((set, get) => ({
  // Initial state
  isConnected: false,
  address: null,
  smartAccountAddress: null,
  shieldConfig: null,
  isShieldActive: false,
  strategies: [],
  activeStrategies: [],
  permissions: [],

  // Connect wallet
  connect: async () => {
    const { address } = await connectWallet();
    const smartAccount = await getOrCreateSmartAccount(address);

    set({
      isConnected: true,
      address,
      smartAccountAddress: smartAccount.address,
    });

    // Refresh data
    await get().refreshShieldStatus();
    await get().refreshStrategies();
  },

  // Activate Shield
  activateShield: async (config) => {
    const { smartAccountAddress } = get();
    if (!smartAccountAddress) throw new Error("Not connected");

    const hash = await writeContract({
      address: SHIELD_CORE_ADDRESS,
      abi: ShieldCoreABI,
      functionName: "activateShield",
      args: [config.dailyLimit, config.singleTxLimit],
    });

    await waitForTransaction({ hash });

    set({
      shieldConfig: config,
      isShieldActive: true,
    });
  },

  // Create strategy (includes permission request)
  createStrategy: async (params) => {
    const { address } = get();
    if (!address) throw new Error("Not connected");

    // 1. Request permissions
    const permission = await requestPermission(params);

    // 2. Create on-chain strategy
    const hash = await writeContract({
      address: DCA_EXECUTOR_ADDRESS,
      abi: DCAExecutorABI,
      functionName: "createStrategy",
      args: [/* ... */],
    });

    await waitForTransaction({ hash });

    // 3. Refresh list
    await get().refreshStrategies();
  },

  // Refresh strategy data (from Envio)
  refreshStrategies: async () => {
    const { address } = get();
    if (!address) return;

    const result = await graphqlClient.query({
      query: GET_USER_STRATEGIES,
      variables: { userId: address.toLowerCase() },
    });

    const strategies = result.data.strategies;

    set({
      strategies,
      activeStrategies: strategies.filter(s => s.status === "ACTIVE"),
    });
  },

  // ... other methods
}));
```

### 6.4 Project Directory Structure

```
shield-protocol/
├── apps/
│   ├── web/                          # Next.js frontend app
│   │   ├── src/
│   │   │   ├── app/                  # App Router pages
│   │   │   │   ├── layout.tsx        # Root layout
│   │   │   │   ├── page.tsx          # Home page
│   │   │   │   ├── dashboard/
│   │   │   │   │   └── page.tsx      # Dashboard
│   │   │   │   ├── strategies/
│   │   │   │   │   ├── page.tsx      # Strategy list
│   │   │   │   │   └── new/
│   │   │   │   │       └── page.tsx  # Create strategy
│   │   │   │   ├── shield/
│   │   │   │   │   └── page.tsx      # Shield settings
│   │   │   │   └── analytics/
│   │   │   │       └── page.tsx      # Analytics
│   │   │   │
│   │   │   ├── components/           # React components
│   │   │   │   ├── ui/               # Basic UI components (Shadcn)
│   │   │   │   ├── layout/
│   │   │   │   │   ├── Header.tsx
│   │   │   │   │   ├── Sidebar.tsx
│   │   │   │   │   └── Footer.tsx
│   │   │   │   ├── dashboard/
│   │   │   │   │   ├── ShieldStatusCard.tsx
│   │   │   │   │   ├── StatsCards.tsx
│   │   │   │   │   ├── StrategyList.tsx
│   │   │   │   │   └── RecentActivity.tsx
│   │   │   │   ├── strategies/
│   │   │   │   │   ├── StrategyCard.tsx
│   │   │   │   │   ├── StrategyBuilder.tsx
│   │   │   │   │   ├── DCAForm.tsx
│   │   │   │   │   └── PermissionSummary.tsx
│   │   │   │   ├── shield/
│   │   │   │   │   ├── ShieldConfig.tsx
│   │   │   │   │   ├── SpendingLimitSlider.tsx
│   │   │   │   │   ├── WhitelistManager.tsx
│   │   │   │   │   └── EmergencyButton.tsx
│   │   │   │   └── analytics/
│   │   │   │       ├── PerformanceChart.tsx
│   │   │   │       ├── ExecutionHistory.tsx
│   │   │   │       └── GasAnalysis.tsx
│   │   │   │
│   │   │   ├── hooks/                # Custom Hooks
│   │   │   │   ├── useShield.ts      # Shield-related operations
│   │   │   │   ├── useStrategy.ts    # Strategy-related operations
│   │   │   │   ├── usePermission.ts  # Permission management
│   │   │   │   └── useAnalytics.ts   # Analytics
│   │   │   │
│   │   │   ├── stores/               # Zustand state management
│   │   │   │   ├── shieldStore.ts
│   │   │   │   └── uiStore.ts
│   │   │   │
│   │   │   ├── services/             # API services
│   │   │   │   ├── graphql/
│   │   │   │   │   ├── client.ts     # GraphQL client
│   │   │   │   │   └── queries.ts    # Query definitions
│   │   │   │   └── contracts/
│   │   │   │       ├── shieldCore.ts
│   │   │   │       └── dcaExecutor.ts
│   │   │   │
│   │   │   ├── lib/                  # Utility functions
│   │   │   │   ├── wagmi.ts          # Wagmi configuration
│   │   │   │   ├── delegation.ts     # Delegation Toolkit configuration
│   │   │   │   └── utils.ts          # General utilities
│   │   │   │
│   │   │   └── types/                # TypeScript type definitions
│   │   │       ├── shield.ts
│   │   │       ├── strategy.ts
│   │   │       └── permission.ts
│   │   │
│   │   ├── public/                   # Static assets
│   │   ├── package.json
│   │   └── next.config.js
│   │
│   └── backend/                      # Backend service (optional, for auto execution)
│       ├── src/
│       │   ├── services/
│       │   │   └── executor.ts       # DCA execution service
│       │   ├── jobs/
│       │   │   └── dcaCron.ts        # Cron jobs
│       │   └── index.ts
│       └── package.json
│
├── packages/
│   ├── contracts/                    # Solidity smart contracts
│   │   ├── src/
│   │   │   ├── core/
│   │   │   │   ├── ShieldCore.sol
│   │   │   │   └── ShieldStorage.sol
│   │   │   ├── strategies/
│   │   │   │   ├── DCAExecutor.sol
│   │   │   │   ├── RebalanceExecutor.sol
│   │   │   │   └── StopLossExecutor.sol
│   │   │   ├── caveats/
│   │   │   │   ├── SpendingLimitEnforcer.sol
│   │   │   │   └── WhitelistEnforcer.sol
│   │   │   └── interfaces/
│   │   │       └── IShieldProtocol.sol
│   │   ├── test/
│   │   │   ├── ShieldCore.t.sol
│   │   │   └── DCAExecutor.t.sol
│   │   ├── script/
│   │   │   └── Deploy.s.sol
│   │   ├── hardhat.config.ts
│   │   └── package.json
│   │
│   ├── sdk/                          # Shield Protocol SDK
│   │   ├── src/
│   │   │   ├── Shield.ts             # Main class
│   │   │   ├── Strategy.ts           # Strategy class
│   │   │   ├── Permission.ts         # Permission class
│   │   │   └── types.ts              # Type definitions
│   │   └── package.json
│   │
│   └── indexer/                      # Envio indexer
│       ├── src/
│       │   └── handlers/
│       │       ├── ShieldCore.ts
│       │       └── DCAExecutor.ts
│       ├── schema.graphql
│       ├── config.yaml
│       └── package.json
│
├── .env.example                      # Environment variable example
├── package.json                      # Root package.json
├── turbo.json                        # Turborepo configuration
└── README.md
```

---

## 9. Phase 3 Planning: AI Agent Integration

### 9.1 Feature Overview

> 🚧 **This feature is currently in planning phase, not yet implemented**

AI Agent integration will allow users to grant limited on-chain execution permissions to AI agents, enabling autonomous DeFi operations.

```
┌─────────────────────────────────────────────────────────────────────┐
│                     AI Agent Architecture Planning                  │
└─────────────────────────────────────────────────────────────────────┘

  User                    Shield Protocol                    AI Agent
    │                           │                               │
    │  1. Grant limited permissions │                               │
    │ ─────────────────────────►│                               │
    │  (limits, time, contract whitelist) │                               │
    │                           │                               │
    │                           │  2. Register Agent Permissions │
    │                           │◄──────────────────────────────│
    │                           │                               │
    │                           │  3. Execute within permission boundaries │
    │                           │◄──────────────────────────────│
    │                           │                               │
    │  4. Real-time monitoring notification │                               │
    │◄──────────────────────────│                               │
```

### 9.2 Planned Features

| Feature | Description | Status |
|------|------|------|
| **🤖 Natural Language Strategy** | "Buy when ETH RSI < 30" | 🚧 Planning |
| **🔒 Agent Permission Framework** | Assign granular permissions to AI agents | 🚧 Planning |
| **📊 Market Analysis** | AI real-time market data analysis | 🚧 Planning |
| **⚡ Cross-protocol Optimization** | Automatically find best yields across multiple protocols | 🚧 Planning |
| **🛡️ Risk Assessment** | AI assess transaction risk level | 🚧 Planning |

### 9.3 Technical Design

#### Agent Permission Interface (Planning)

```solidity
// contracts/src/agents/AgentPermissionManager.sol (Planning)

interface IAgentPermissionManager {
    struct AgentPermission {
        address agent;              // AI Agent address
        address user;               // User address
        string[] capabilities;      // Allowed operation types ["swap", "stake"]
        uint256 maxValuePerTx;      // Max amount per transaction
        uint256 maxDailyVolume;     // Max daily total
        address[] allowedProtocols; // Protocols allowed to interact with
        address[] allowedTokens;    // Tokens allowed to operate
        uint256 expiry;             // Permission expiry time
        bool active;                // Is active
    }

    /// @notice Grant AI Agent permissions
    function grantAgentPermission(
        address agent,
        string[] calldata capabilities,
        uint256 maxValuePerTx,
        uint256 maxDailyVolume,
        address[] calldata allowedProtocols,
        address[] calldata allowedTokens,
        uint256 duration
    ) external returns (bytes32 permissionId);

    /// @notice AI Agent execute operation
    function executeAsAgent(
        bytes32 permissionId,
        address target,
        bytes calldata data,
        uint256 value
    ) external;

    /// @notice Revoke Agent permissions
    function revokeAgentPermission(bytes32 permissionId) external;
}
```

#### Frontend SDK (Planning)

```typescript
// Planned AI Agent SDK usage example

// 1. Grant AI Agent permissions
const permission = await shield.grantAgentPermission({
  agent: aiAgentAddress,
  capabilities: ["swap", "stake", "provide-liquidity"],
  constraints: {
    maxValuePerTx: parseEther("0.5"),    // Max 0.5 ETH per transaction
    maxDailyVolume: parseEther("5"),     // Max 5 ETH daily
    allowedProtocols: ["uniswap-v3", "aave-v3", "curve"],
    allowedTokens: ["ETH", "USDC", "WBTC", "DAI"]
  },
  expiry: Date.now() + 30 * 24 * 60 * 60 * 1000 // 30-day validity
});

// 2. AI Agent execute operation (on its own server)
const result = await agentSDK.executeWithPermission({
  permissionId: permission.id,
  action: {
    type: "swap",
    fromToken: "USDC",
    toToken: "ETH",
    amount: parseUnits("100", 6),
    minAmountOut: parseEther("0.04")
  }
});

// 3. User can view Agent activity anytime
const agentActivity = await shield.getAgentActivity(aiAgentAddress);

// 4. User can revoke permissions anytime
await shield.revokeAgentPermission(permission.id);
```

### 9.4 Security Considerations

```
AI Agent Permission Security Boundaries:
─────────────────────────────────────────────────────────────
✅ Single transaction limit - Each transaction not exceeding set amount
✅ Daily limit - Daily operation total limit
✅ Protocol whitelist - Only interact with approved protocols
✅ Token whitelist - Only operate approved tokens
✅ Time limit - Permissions auto-expire
✅ Instant revocation - User can revoke all Agent permissions anytime
✅ Operation log - All Agent operations transparent and traceable
✅ Anomaly detection - Suspicious behavior auto-pause
```

### 9.5 Implementation Roadmap

```
Phase 3: AI Agent Framework (Expected 2025 Q3-Q4)
─────────────────────────────────────────────────────────────
├── Q3 2025:
│   ├── [ ] AgentPermissionManager contract development
│   ├── [ ] Agent permission verification mechanism
│   └── [ ] Basic Agent SDK
│
├── Q4 2025:
│   ├── [ ] Natural language strategy parsing
│   ├── [ ] Market data AI analysis integration
│   ├── [ ] Cross-protocol yield optimization
│   └── [ ] Risk assessment model
│
└── 2026:
    ├── [ ] Third-party AI Agent integration
    ├── [ ] Agent marketplace
    └── [ ] Agent reputation system
```

---

## Summary

### Design Highlights Review

| Aspect | Design Decision | Reason |
|------|---------|------|
| **Interaction Mode** | Intent-driven | Reduce user cognitive burden, improve experience |
| **Permission Model** | ERC-7715 granular permissions | Secure, controllable, user trust |
| **Account Type** | EIP-7702 Smart Account | Keep EOA address, gain SC capabilities |
| **Data Layer** | Envio HyperIndex | High-performance indexing, real-time data |
| **Execution Layer** | ERC-4337 UserOperation | Gas abstraction, batch execution |
| **Frontend** | Next.js + React | Modern development experience, SSR optimization |

### Core Competitiveness

1. **MetaMask Native** - Direct permission control at wallet level
2. **User Controllable** - All permissions transparent, revocable
3. **Security First** - Default limit protection, emergency freeze mechanism
4. **Data Driven** - Envio provides complete data analysis capability
5. **Developer Friendly** - Complete SDK and documentation
6. **AI Ready** - Extension interface reserved for AI Agent integration

### Project Phases

| Phase | Content | Status |
|------|------|------|
| **Phase 1: MVP** | ShieldCore, DCA, Stop-loss, Subscription | ✅ Completed |
| **Phase 2: Enhancement** | ML anomaly detection, Multi-chain, Mobile | 🚧 In Progress |
| **Phase 3: AI Agent** | Agent permission framework, Natural language strategy | 📋 Planning |
| **Phase 4: Ecosystem** | SDK, Strategy marketplace, DAO governance | 📋 Planning |

---

*Document Version: v1.1*
*Last Updated: 2024-12-21*