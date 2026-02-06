# 💰 Allowance Wallet

A smart contract system for parents to set up recurring STX allowances for their children with spending limits and approval requirements.

## 🎯 What It Does

Allowance Wallet enables parents to create structured, automated allowances on the Stacks blockchain. Parents can:

- 🔄 Set up recurring STX allowances with customizable intervals
- 💵 Define spending limits per period
- ✅ Require approval for certain withdrawals
- 👀 Track spending patterns
- 🎮 Teach kids financial responsibility in a safe environment

## 🛠️ Core Features

### For Parents

- **Create Allowance**: Set up a new allowance for a child with custom parameters
- **Fund Allowance**: Deposit STX into the contract to fund allowances
- **Approve/Reject Withdrawals**: Review and approve withdrawal requests
- **Update Settings**: Modify allowance amounts, intervals, and limits
- **Activate/Deactivate**: Pause or resume allowances as needed

### For Children

- **Claim Allowance**: Automatically receive allowance when the interval period passes
- **Direct Spending**: Spend within limits without approval (if enabled)
- **Request Withdrawals**: Submit withdrawal requests with reasons for parental approval

## 📋 Usage Instructions

### Setup

1. Deploy the contract to Stacks blockchain
2. Parent calls `create-allowance` with child's address and parameters
3. Parent calls `fund-allowance` to deposit STX into the contract

### Creating an Allowance

```clarity
(contract-call? .allowance-wallet create-allowance
  'ST1CHILD...
  u100000000  ;; 100 STX per allowance
  u1440       ;; Every 1440 blocks (~10 days)
  u50000000   ;; 50 STX spending limit per period
  true        ;; Requires approval for withdrawals
)
```

### Funding the Allowance

```clarity
(contract-call? .allowance-wallet fund-allowance
  'ST1CHILD...
  u500000000  ;; Fund with 500 STX
)
```

### Child Claims Allowance

```clarity
(contract-call? .allowance-wallet claim-allowance)
```

### Child Requests Withdrawal

```clarity
(contract-call? .allowance-wallet request-withdrawal
  u25000000  ;; 25 STX
  "For new video game"
)
```

### Parent Approves Request

```clarity
(contract-call? .allowance-wallet approve-withdrawal
  'ST1CHILD...
  u0  ;; Request ID
)
```

### Spending Without Approval

If `requires-approval` is set to `false`:

```clarity
(contract-call? .allowance-wallet spend
  u10000000  ;; 10 STX
)
```

## 🔑 Key Parameters

- **amount**: STX amount per allowance (in microSTX)
- **interval**: Blocks between allowances (~144 blocks = 1 day)
- **spending-limit**: Max spending per period (in microSTX)
- **requires-approval**: Whether withdrawals need parent approval

## 📊 Read-Only Functions

Check allowance status:

```clarity
(contract-call? .allowance-wallet get-allowance 'ST1CHILD...)
```

Check if child can claim:

```clarity
(contract-call? .allowance-wallet can-claim 'ST1CHILD...)
```

View spending for period:

```clarity
(contract-call? .allowance-wallet get-spending 'ST1CHILD... u123)
```

Check withdrawal request:

```clarity
(contract-call? .allowance-wallet get-withdrawal-request 'ST1CHILD... u0)
```

## 🎓 What It Teaches

### Multi-Signature Patterns
- Parent approval required for certain transactions
- Two-party authorization workflow

### Scheduled Payments
- Time-based allowance claims using block height
- Automated recurring distributions

### Spending Controls
- Per-period spending limits
- Real-time spending tracking
- Balance management

## 🔒 Security Features

- Parent-only administrative functions
- Child-only claim and spending functions
- Spending limit enforcement
- Approval requirement toggles
- Allowance activation controls

## ⚡ Error Codes

- `u100`: Owner-only function
- `u101`: Not the parent
- `u102`: Not the child
- `u103`: Allowance not found
- `u104`: Insufficient balance
- `u105`: Spending limit exceeded
- `u106`: Approval required
- `u107`: Invalid amount
- `u108`: Already approved
- `u109`: Already rejected
- `u110`: Not ready to claim
- `u111`: Allowance already exists

## 🚀 Getting Started

1. Install Clarinet
2. Create a new project: `clarinet new allowance-wallet-project`
3. Copy `allowance-wallet.clar` to `contracts/` folder
4. Test with: `clarinet test`
5. Deploy with: `clarinet deploy`

## 💡 Use Cases

- 👨‍👩‍👧‍👦 Family allowance management
- 🎓 Teaching financial literacy to children
- 💳 Controlled spending for teens
- 🎮 Gaming budgets with parental oversight
- 📱 First crypto wallet experience for kids

## 🤝 Contributing

Feel free to submit issues and enhancement requests!

## 📄 License

MIT License - feel free to use and modify!

---

Built with ❤️ for teaching kids about blockchain and financial responsibility