# Creating My NFT - ManuNFT

We are creating an NFT contract in order to generate an NFT collection called ManuNFT. We’ll import the [Open Zeppelin's](https://openzeppelin.com) code for standard functions and add our functionality on top of it.

## Overview



### Base

We are creating a basic smart contract and importing ERC721.sol.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.9;
 
import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
 
contract ManuNFT is ERC721 {
   constructor() ERC721("ManuNFT", "MAN") {}
}
```

### Implement Constructor

_ERC721.sol takes two parameters in its constructor, the NFT name and NFT symbol. To inherit it properly, we need to implement its constructor. Let’s call this NFT ManuNFT and symbol “MAN”._


```solidity
contract ManuNFT is ERC721 {
   constructor() ERC721("ManuNFT", "MAN") {}
}
```
The above code imports [Open Zeppelin's](https://openzeppelin.com) contract for ERC-721 and creates a collection called ManuNFT with a symbol MAN.

### Usage

But currently, no NFT has been minted (created). We’ll add a function that enables a user to call the _safeMint function in the imported [Open Zeppelin's](https://openzeppelin.com) code as depicted below:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract ManuNFT is ERC721, Ownable {

    constructor() ERC721("ManuNFT", "MAN") {}

    function safeMint(address to) public onlyOwner {
        uint256 tokenId = _tokenIdCounter.current();
        _tokenIdCounter.increment();
        _safeMint(to, tokenId);
    }
}
```

**safeMint**
_safeMint is an internal function defined in [Open Zeppelin's](https://openzeppelin.com) code. We call it by defining our own function safeMint so that we can add any other conditions to it. For example, we can require the address to be whitelisted, or have a certain balance, or check if the current supply is less than the max supply etc. before a user is allowed to mint it. We’ll use these conditions in future modules when we create more complex contracts.

**Other Functions from ERC721**
Now, when we deploy this contract, it provides us the functionality to mint an NFT and use all the other functionalities provided by the ERC-721 standard that we discussed above. For example: safeTransferFrom, approve etc.

## License

This Contract is released under the [MIT License](LICENSE) and thanks to [OpenZeppelin](https://openzeppelin.com).

