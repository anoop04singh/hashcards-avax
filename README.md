### A Web3 Solution for Secure and Flexible Gifting

HashCards
=========

![hashcardsLandscape](https://github.com/user-attachments/assets/f7367b28-785a-4e1a-97d8-21847727da07)


**HashCards** is a physical and fastest crypto gifting solution. It allows users to gift cryptocurrency seamlessly by integrating NFTs and physical gift cards, leveraging the power of the Avalanche network.

How HashCards Work
------------------

1.  **Purchase Physical Card**:Users start by purchasing a physical HashCard.
    
1.  **NFT Minted by HashCards**:Once the purchase is completed, an NFT representing the physical card is minted on the Avalanche network.
    
1.  **Send Physical Card**:The physical card is delivered to the buyer, ready to be gifted.
    
1.  **Add Balance**:The user can add balance to the NFT using its token ID, making the card valuable and ready for gifting. This process is facilitated by smart contract interactions.
    
1.  **Gift the Card**:The HashCard can be gifted to anyone, allowing the recipient to own the NFT and the attached balance.
    
1.  **Redeem Process**:
    
    *   The recipient can redeem the balance by transferring the NFT to their wallet using the unique credentials of each gift card.
        
    *   Once redeemed, the NFT and balance become theirs to use or hold.
        
1.  **Repeat Process**:The same steps can be repeated for new cards, making gifting crypto easier and more efficient.


![Screenshot 2024-12-12 101719](https://github.com/user-attachments/assets/965970eb-db8c-4dad-8adb-4e4b7c9fa8d5)

    

Smart Contract Code Snippet
---------------------------

Below is a snippet of the HashCards smart contract:


```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract HashCards is ERC721, Ownable {
    mapping(uint256 => uint256) public cardBalances;

    constructor() ERC721("HashCards", "HSC") {}

    function mintCard(address to, uint256 tokenId) external onlyOwner {
        _mint(to, tokenId);
    }

    function addBalance(uint256 tokenId, uint256 amount) external payable {
        require(_exists(tokenId), "Token does not exist");
        cardBalances[tokenId] += amount;
    }

    function redeemBalance(uint256 tokenId) external {
        require(ownerOf(tokenId) == msg.sender, "Not the owner");
        uint256 balance = cardBalances[tokenId];
        require(balance > 0, "No balance to redeem");

        cardBalances[tokenId] = 0;
        payable(msg.sender).transfer(balance);
    }
} 
```

Future Integrations
-------------------

### 1\. Multi-Chain HashCards Wallet

To make the process seamless, a multi-chain wallet will be integrated, allowing users to:

*   Store HashCards across multiple blockchain networks.
    
*   Manage balances and NFTs from one unified dashboard.
    

### 2\. D3 Services Integration

*   Users will be able to purchase custom DNS names for their wallets, making it easier to share and gift cards.
    
*   Enhance personalization by linking domain names to HashCards.
    

### 3\. Personalized Gift Cards

*   Offer customizable designs for physical cards.
    
*   Allow users to add messages and branding for a truly unique gifting experience.
    

Deployment Details
------------------

*   **Network**: Avalanche Fuji Testnet
    
*   **Developer**: Anoop Singh

*   **Contract  Address**:  0x1a8292Ec9465e18437E845d219F000846723ABE8

---

## Deployed on Vercel

[![Vercel](https://assets.vercel.com/image/upload/v1662130559/front/vercel/dps.png)](https://hashcards-avax.vercel.app)

HashCards is deployed and live on **Vercel**. Check it out here: [hashcards-avax.vercel.app](https://hashcards-avax.vercel.app)

---

    

How to Use HashCards
--------------------

1.  **Get Started**:
    
    *   Visit the HashCards website.
        
    *   Connect your Avalanche wallet.
        
1.  **Purchase a Card**:
    
    *   Select a card design and mint an NFT.
        
1.  **Add Balance**:
    
    *   Use the token ID to add funds securely via smart contract.
        
1.  **Gift**:
    
    *   Send the physical card or transfer the NFT directly.
        
1.  **Redeem**:
    
    *   The recipient can redeem the card via their wallet.
        

Acknowledgments
---------------

HashCards is built to redefine the way cryptocurrency is gifted, combining the physical and digital worlds for a seamless experience.

Developed and maintained by **Anoop Singh**.

## Issues

### Gas Fee for Redeeming Gift Cards

Currently, when a new wallet attempts to redeem a gift card, they may encounter an issue if they lack the necessary gas fee. Without sufficient gas, the transaction will not go through.

We are actively exploring solutions to resolve this issue, such as allowing the gas fee to be deducted from the amount in the gift card itself. This feature will ensure a smoother experience for all users and will be updated soon.




