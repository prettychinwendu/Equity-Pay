# Automated Equity-Based Profit Sharing System

A sophisticated blockchain-powered platform for transparent and automated profit distribution among equity shareholders. This system enables businesses to programmatically distribute profits based on predefined ownership stakes with complete transparency and auditability.

## Key Features

- **High-precision equity management** with basis points (0.01% granularity)
- **Automated multi-cycle profit distribution** with complete historical tracking
- **Role-based access control** with comprehensive security protocols
- **Real-time balance tracking** and claim verification system
- **Emergency recovery mechanisms** and administrative controls
- **Built-in validation** and fraud prevention measures

## Overview

This smart contract implements a comprehensive profit-sharing system that allows businesses to:

- Register shareholders with precise ownership percentages (using basis points)
- Automatically distribute profits based on equity stakes
- Maintain complete historical records of all distributions
- Provide transparent and auditable profit sharing
- Implement robust access controls and security measures

The system operates in cycles: funds are contributed during active distribution cycles, and profits are distributed proportionally to shareholders based on their registered ownership percentages.

## Installation

### Prerequisites

- Stacks blockchain environment
- Clarity smart contract deployment tools
- STX tokens for testing and deployment

### Deployment

1. Clone the contract code
2. Deploy to Stacks blockchain using your preferred deployment method
3. Initialize the system with minimum participation threshold
4. Register shareholders and their ownership percentages

```clarity
;; Example initialization
(contract-call? .profit-sharing initialize-profit-sharing-system u1000000) ;; 1 STX minimum
```

## Contract Architecture

### Core Components

1. **Access Control System**: Role-based permissions with administrator controls
2. **Shareholder Registry**: Mapping of wallet addresses to ownership percentages
3. **Distribution Cycles**: Structured profit distribution periods
4. **Balance Tracking**: Individual shareholder balance management
5. **Historical Records**: Complete audit trail of all distributions

### Data Structures

- **Shareholder Registry**: Maps principals to ownership basis points
- **Balance Tracker**: Tracks accumulated balances for each shareholder
- **Distribution Archive**: Historical record of all profit distributions
- **Claim Verification**: Prevents double-claiming of profits
- **Access Restrictions**: Manages shareholder access permissions

## Usage Guide

### 1. System Initialization

The contract administrator must first initialize the system:

```clarity
;; Initialize with minimum participation threshold (in microSTX)
(contract-call? .profit-sharing initialize-profit-sharing-system u1000000)
```

### 2. Shareholder Registration

Register shareholders with their ownership percentages:

```clarity
;; Register shareholder with 25.00% ownership (2500 basis points)
(contract-call? .profit-sharing register-new-shareholder 'SP1EXAMPLE... u2500)
```

### 3. Profit Distribution Cycle

**Start a distribution cycle:**
```clarity
(contract-call? .profit-sharing initiate-profit-distribution-cycle)
```

**Contributors add funds:**
```clarity
;; Contribute specific amount
(contract-call? .profit-sharing contribute-specified-amount u5000000)

;; Or contribute entire wallet balance
(contract-call? .profit-sharing contribute-entire-wallet-balance)
```

**Execute distribution:**
```clarity
(contract-call? .profit-sharing execute-comprehensive-profit-distribution)
```

### 4. Claim Profits

Shareholders claim their entitled profits:

```clarity
;; Claim profits from distribution cycle #1
(contract-call? .profit-sharing claim-shareholder-profit-entitlement u1)
```

## API Reference

### Administrative Functions

| Function | Description | Access |
|----------|-------------|---------|
| `initialize-profit-sharing-system` | Initialize the system | Admin only |
| `register-new-shareholder` | Add new shareholder | Admin only |
| `modify-shareholder-ownership-allocation` | Update ownership % | Admin only |
| `remove-shareholder-from-registry` | Remove shareholder | Admin only |
| `initiate-profit-distribution-cycle` | Start distribution cycle | Admin only |
| `conclude-profit-distribution-cycle` | End distribution cycle | Admin only |
| `execute-comprehensive-profit-distribution` | Distribute profits | Admin only |

### Public Functions

| Function | Description | Access |
|----------|-------------|---------|
| `contribute-specified-amount` | Contribute specific amount | Public |
| `contribute-entire-wallet-balance` | Contribute full balance | Public |
| `claim-shareholder-profit-entitlement` | Claim profits | Shareholders |

### Read-Only Functions

| Function | Description | Returns |
|----------|-------------|---------|
| `get-shareholder-ownership-details` | Get ownership info | `{allocated-ownership-basis-points: uint}` |
| `get-shareholder-accumulated-balance` | Get accumulated balance | `uint` |
| `get-profit-distribution-cycle-details` | Get cycle details | `{distributed-profit-amount: uint, cycle-completion-block-height: uint}` |
| `verify-profit-claim-status` | Check if profits claimed | `bool` |
| `get-comprehensive-system-overview` | Get full system status | System overview object |

## Security Features

### Access Control
- **Administrator-only functions**: Critical operations restricted to contract deployer
- **Shareholder access restrictions**: Ability to block specific shareholders
- **Input validation**: Comprehensive validation of all inputs and parameters

### Financial Security
- **Double-spending prevention**: Claims are tracked to prevent multiple withdrawals
- **Balance verification**: All transfers are verified before execution
- **Emergency controls**: Administrator can withdraw all funds in emergencies

### Data Integrity
- **Immutable records**: All distributions are permanently recorded
- **Audit trails**: Complete history of all operations
- **State consistency**: Robust state management prevents inconsistencies

## Examples

### Complete Workflow Example

```clarity
;; 1. Initialize system (Admin)
(contract-call? .profit-sharing initialize-profit-sharing-system u1000000)

;; 2. Register shareholders (Admin)
(contract-call? .profit-sharing register-new-shareholder 'SP1ALICE... u3000) ;; 30%
(contract-call? .profit-sharing register-new-shareholder 'SP1BOB... u2000)   ;; 20%
(contract-call? .profit-sharing register-new-shareholder 'SP1CAROL... u5000) ;; 50%

;; 3. Start distribution cycle (Admin)
(contract-call? .profit-sharing initiate-profit-distribution-cycle)

;; 4. Contributors add funds (Anyone)
(contract-call? .profit-sharing contribute-specified-amount u10000000) ;; 10 STX

;; 5. Execute distribution (Admin)
(contract-call? .profit-sharing execute-comprehensive-profit-distribution)

;; 6. Shareholders claim profits
;; Alice gets 30% = 3 STX
;; Bob gets 20% = 2 STX  
;; Carol gets 50% = 5 STX
(contract-call? .profit-sharing claim-shareholder-profit-entitlement u1)
```

### Query System Status

```clarity
;; Get comprehensive system overview
(contract-call? .profit-sharing get-comprehensive-system-overview)

;; Check specific shareholder details
(contract-call? .profit-sharing get-shareholder-ownership-details 'SP1ALICE...)

;; Verify if profits were claimed
(contract-call? .profit-sharing verify-profit-claim-status u1 'SP1ALICE...)
```

## Error Codes

### Access Control Errors (100-199)
- `u100`: `ERR-UNAUTHORIZED-OPERATION` - Operation requires administrator privileges
- `u101`: `ERR-SHAREHOLDER-ACCESS-DENIED` - Shareholder access restricted
- `u102`: `ERR-INSUFFICIENT-PERMISSIONS` - Insufficient permissions for operation

### System State Errors (200-299)
- `u200`: `ERR-SYSTEM-ALREADY-ACTIVE` - System already initialized
- `u201`: `ERR-SYSTEM-NOT-INITIALIZED` - System not yet initialized
- `u202`: `ERR-INVALID-SYSTEM-STATE` - Invalid system state for operation

### Input Validation Errors (300-399)
- `u300`: `ERR-INVALID-OWNERSHIP-PERCENTAGE` - Ownership percentage exceeds 100%
- `u301`: `ERR-INVALID-MINIMUM-THRESHOLD` - Invalid minimum participation threshold
- `u302`: `ERR-INVALID-ADDRESS-FORMAT` - Invalid wallet address format
- `u303`: `ERR-ZERO-VALUE-NOT-ALLOWED` - Zero values not permitted
- `u304`: `ERR-INVALID-DISTRIBUTION-CYCLE` - Invalid distribution cycle ID

### Business Logic Errors (400-499)
- `u400`: `ERR-OWNERSHIP-LIMIT-EXCEEDED` - Total ownership would exceed 100%
- `u401`: `ERR-SHAREHOLDER-NOT-FOUND` - Shareholder not registered
- `u402`: `ERR-INSUFFICIENT-EQUITY-STAKE` - No ownership stake found
- `u403`: `ERR-PROFIT-CYCLE-IN-PROGRESS` - Distribution cycle currently active
- `u404`: `ERR-NO-ACTIVE-PROFIT-CYCLE` - No active distribution cycle
- `u405`: `ERR-PROFITS-PREVIOUSLY-CLAIMED` - Profits already claimed for this cycle
- `u406`: `ERR-SHAREHOLDER-REGISTRATION-EXISTS` - Shareholder already registered

### Financial Transaction Errors (500-599)
- `u500`: `ERR-INSUFFICIENT-CONTRACT-FUNDS` - Contract has insufficient balance
- `u501`: `ERR-PAYMENT-TRANSFER-FAILED` - STX transfer failed
- `u502`: `ERR-INSUFFICIENT-USER-FUNDS` - User has insufficient balance

## Contributing

1. Fork the repository
2. Create a feature branch
3. Add comprehensive tests
4. Submit a pull request