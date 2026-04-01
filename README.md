# NFT-ticket-with-one-time-use
NFT “ticket” with one‑time use
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract TicketNFT is ERC721 {
    uint256 public nextId;
    mapping(uint256 => bool) public used;

    constructor() ERC721("TicketNFT", "TKT") {}

    function mint() public {
        _mint(msg.sender, nextId++);
    }

    function useTicket(uint256 id) public {
        require(ownerOf(id) == msg.sender, "Not owner");
        require(!used[id], "Used");
        used[id] = true;
    }
}
