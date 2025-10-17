# DynamicTaxToken (DYN-TOKEN)

A Clarity smart contract implementing a fungible token with dynamic transfer tax rates.

## Features

- **Dynamic Tax System**: Switches between stable (0.1%) and volatile (1%) tax modes
- **SIP-010 Compliant**: Implements the Stacks Fungible Token standard
- **Admin Controls**: 
  - Treasury management
  - Tax mode switching
  - Minting/burning capabilities
- **Secure Transfer Logic**: Atomic operations for both fee and net amount transfers

## Contract Functions

### Public Functions

```clarity
(transfer-taxed (amount uint) (sender principal) (recipient principal))
(set-treasury (to principal))
(set-volatile-mode (mode bool))
(admin-mint (to principal) (amount uint))
(admin-burn (from principal) (amount uint))
```

### Read-Only Functions

```clarity
(current-tax) ;; Returns tax rate as (tuple (num uint) (den uint))
(compute-fee (amount uint))
(balance-of (who principal))
(is-volatile)
```

## Tax Rates

- **Stable Mode**: 0.1% (1/1000)
- **Volatile Mode**: 1.0% (10/1000)

## Error Codes

- `ERR-NOT-ADMIN (u100)`: Unauthorized admin action
- `ERR-TRANSFER-FAIL (u101)`: Transfer operation failed
- `ERR-MINT-FAIL (u102)`: Minting operation failed
- `ERR-BURN-FAIL (u103)`: Burning operation failed
- `ERR-ZERO-AMOUNT (u104)`: Invalid zero amount

## Development

```bash
# Deploy to testnet
clarinet test
clarinet deploy --testnet

# Run tests
clarinet test tests/DynamicTaxToken_test.clar
```
