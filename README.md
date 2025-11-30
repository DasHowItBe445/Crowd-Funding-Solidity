# Decentralized CrowdFunding Smart Contract

This project implements a secure, transparent Crowdfunding Smart Contract deployed on the Ethereum Sepolia Testnet using MetaMask for wallet interaction. The contract enables contributors to donate funds, vote on spending requests, and receive refunds if the campaign goal is not achieved — ensuring trustless and decentralized management.

Features:

1] Minimum Funding Requirement – Ensures meaningful participation.

2] Deadline-Based Campaigns – Contributions accepted only before expiration.

3] Refund Mechanism – Contributors can withdraw funds if goal is not reached.

4] Admin-Controlled Spending Requests – Campaign owner can submit spending proposals.

5] Voting System for Transparency – Contributors vote before funds are released.

6] Secure Withdrawals – Funds released only if majority approves (>50%).


Smart Contract Workflow:
| Action            | Description                                    |
| ----------------- | ---------------------------------------------- |
| `contribute()`    | Allows users to contribute ETH before deadline |
| `getRefund()`     | Issues refund if the campaign fails            |
| `createRequest()` | Admin proposes a spending request              |
| `voteRequest()`   | Contributors vote on spending proposal         |
| `makePayment()`   | Admin transfers funds if majority approves     |


Contract Variables:
| Variable           | Description                            |
| ------------------ | -------------------------------------- |
| `goal`             | Target funding amount                  |
| `deadline`         | Campaign expiration time               |
| `raisedAmount`     | Total collected funds                  |
| `contributors`     | Tracks contribution amount per address |
| `Request` struct   | Stores payment request details         |
| `noOfContributors` | Voting pool count                      |


Events:
| Event                | Triggered When                        |
| -------------------- | ------------------------------------- |
| `ContributeEvent`    | A user contributes ETH                |
| `CreateRequestEvent` | Admin creates fund withdrawal request |
| `MakePaymentEvent`   | Approved payment is executed          |


Code Sample:

function contribute() public payable {
    require(block.timestamp < deadline, "Deadline has passed!");
    require(msg.value >= minimumContribution, "Minimum Contribution not met");

    if(contributors[msg.sender] == 0){
        noOfContributors++;
    }

    contributors[msg.sender] += msg.value;
    raisedAmount += msg.value;

    emit ContributeEvent(msg.sender, msg.value);
}


Technologies Used:

1] Solidity 0.8.x

2] Ethereum / EVM

3] Metamask & Hardhat/Remix (optional deployment tools)

4] Ethereum Sepolia Testnet

5] Events & Mappings for storage management


How to Deploy:

1] Copy the contract into Remix IDE

2] Compile using Solidity ^0.8.0

3] Connect MetaMask to Sepolia Testnet

4] Deploy with parameters:

goal (in wei), deadline (duration in seconds)

5] Test functionality with multiple MetaMask accounts


Future Improvements:

-> Support for multiple campaigns

-> Frontend dApp integration using Web3.js / Ethers.js

-> Automated unit testing with Hardhat/Foundry

-> Role-based admin control

