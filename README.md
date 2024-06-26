# LoanApproval Smart Contract

## Overview

The LoanApproval smart contract, implemented in Solidity, is designed to facilitate loan approval decisions based on a borrower's CIBIL score. The contract owner can update and check CIBIL scores to determine eligibility for different types of loans (high-risk, moderate-risk, and low-risk).

## Features

- **CIBIL Score Management**: Public variables and events to manage and log changes in CIBIL scores.
- **Access Control**: Only the contract owner can update and check CIBIL scores.
- **Loan Approval Functions**: Functions to approve or deny loans based on specific CIBIL score thresholds.

## Public Variables

- `uint256 public cibilScore = 300;`
  - The initial CIBIL score, set to 300.
  
- `address public owner;`
  - The owner of the contract, set to the contract deployer.

## Events

- `event CibilScoreChanged(uint256 currentScore);`
  - Logs changes to the CIBIL score.

## Modifiers

- `modifier onlyOwner()`
  - Restricts function access to the contract owner.

## Constructor

- `constructor()`
  - Sets the contract deployer as the owner.

## Functions

### approveHighRiskLoan(uint256 currentScore)

- **Description**: Approves a high-risk loan if the CIBIL score is between 300 and 599.
- **Parameters**:
  - `currentScore` (uint256): The current CIBIL score.
- **Access**: Only the contract owner.

```solidity
function approveHighRiskLoan(uint256 currentScore) external onlyOwner {
    require(currentScore >= 300 && currentScore < 600, "CIBIL score does not qualify for high-risk loan");
    cibilScore = currentScore;
    emit CibilScoreChanged(currentScore);
}
```

### approveModerateRiskLoan(uint256 currentScore)

- **Description**: Approves a moderate-risk loan if the CIBIL score is between 600 and 749.
- **Parameters**:
  - `currentScore` (uint256): The current CIBIL score.
- **Access**: Only the contract owner.

```solidity
function approveModerateRiskLoan(uint256 currentScore) external onlyOwner {
    require(currentScore >= 600 && currentScore < 750, "CIBIL score does not qualify for moderate-risk loan");
    cibilScore = currentScore;
    emit CibilScoreChanged(currentScore);
}
```

### approveLowRiskLoan(uint256 currentScore)

- **Description**: Approves a low-risk loan if the CIBIL score is 750 or above.
- **Parameters**:
  - `currentScore` (uint256): The current CIBIL score.
- **Access**: Only the contract owner.

```solidity
function approveLowRiskLoan(uint256 currentScore) external onlyOwner {
    require(currentScore >= 750, "CIBIL score does not qualify for low-risk loan");
    cibilScore = currentScore;
    emit CibilScoreChanged(currentScore);
}
```

### checkMinimumCibilScore()

- **Description**: Ensures the CIBIL score is above the minimum threshold for any loan approval.
- **Access**: Public view function.

```solidity
function checkMinimumCibilScore() external view {
    assert(cibilScore >= 300); // This should always be true
}
```

### approveAnyLoan(uint256 currentScore)

- **Description**: Approves a loan if the CIBIL score is 300 or above.
- **Parameters**:
  - `currentScore` (uint256): The current CIBIL score.
- **Access**: Only the contract owner.

```solidity
function approveAnyLoan(uint256 currentScore) external onlyOwner {
    if (currentScore < 300) {
        revert("CIBIL score is too low for any loan approval.");
    }
    cibilScore = currentScore;
    emit CibilScoreChanged(currentScore);
}
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
