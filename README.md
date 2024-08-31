# Vault and ERC20 Token Contracts

## Overview

This repository contains two Solidity smart contracts:

1. **ERC20**: A basic implementation of the ERC20 token standard.
2. **Vault**: A contract that interacts with an ERC20 token to manage deposits and withdrawals, issuing and burning shares.

## License

This code is licensed under the [MIT License](LICENSE).

## Contracts

### ERC20 Contract

A straightforward implementation of the ERC20 token standard with additional minting and burning features.

#### Features

- **Minting**: Allows users to mint new tokens.
- **Burning**: Allows users to burn tokens.
- **Transfer**: Enables the transfer of tokens between addresses.
- **Allowance**: Manages allowances for third-party spending.

#### Functions

- `transfer(address recipient, uint amount) external returns (bool)`: Transfers `amount` tokens from the caller to `recipient`.
- `approve(address spender, uint amount) external returns (bool)`: Approves `spender` to spend `amount` tokens on behalf of the caller.
- `transferFrom(address sender, address recipient, uint amount) external returns (bool)`: Transfers `amount` tokens from `sender` to `recipient` using the caller's allowance.
- `mint(uint amount) external`: Mints `amount` new tokens and assigns them to the caller.
- `burn(uint amount) external`: Burns `amount` tokens from the caller's balance.

#### Events

- `Transfer(address indexed from, address indexed to, uint value)`: Emitted when tokens are transferred.
- `Approval(address indexed owner, address indexed spender, uint value)`: Emitted when an allowance is set.

### Vault Contract

A contract for managing token deposits and withdrawals, issuing and burning shares in exchange for ERC20 tokens.

#### Constructor

- `constructor(address _token)`: Initializes the Vault with the address of the ERC20 token contract.

#### Functions

- `deposit(uint _amount) external`: Deposits `_amount` of ERC20 tokens into the vault and mints shares to the depositor. The number of shares is proportional to the amount deposited.
- `withdraw(uint _shares) external`: Withdraws ERC20 tokens from the vault in exchange for `_shares`. The amount of tokens returned is proportional to the shares burned.

#### Private Functions

- `_mint(address _to, uint _shares) private`: Mints `_shares` and assigns them to `_to`.
- `_burn(address _from, uint _shares) private`: Burns `_shares` from `_from`.

#### Calculation Formulas

- **Deposit Calculation**:
  \[
  \text{shares} = \frac{\text{amount} \times \text{totalSupply}}{\text{balance of token before deposit}}
  \]

- **Withdrawal Calculation**:
  \[
  \text{amount} = \frac{\text{shares} \times \text{balance of token before withdraw}}{\text{totalSupply}}
  \]

## Usage

1. **Deploy the ERC20 Contract**: Deploy the ERC20 contract and mint initial tokens as required.
2. **Deploy the Vault Contract**: Deploy the Vault contract with the address of the ERC20 token contract.
3. **Interact with Contracts**: Users can deposit tokens into the vault to receive shares or withdraw tokens by burning shares.

## Security Considerations

- **Reentrancy**: Contracts do not currently include reentrancy guards. Consider adding reentrancy protection if integrating with other contracts or external systems.
- **Error Handling**: Ensure proper error handling and validation to cover edge cases and potential vulnerabilities.

## Contributing

Contributions are welcome! To contribute, please open an issue or submit a pull request with your changes.
