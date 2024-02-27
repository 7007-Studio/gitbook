# Architecture

### ERC7007

We propose ERC7007 in specific for the need of a standardized interface to verify on-chain AI generated content. Smart contract developers can follow this interface in their development to enable this feature in their own applications. This standard is an extension of the ERC-721 token standard. It proposes a set of interfaces for basic interactions and enumerable interactions for AIGC-NFTs. The standard includes a new mint event and a JSON schema for AIGC-NFT metadata. Additionally, it incorporates zkML as well as opML capabilities to enable verification of AIGC-NFT ownership. In our application, we adopt opML as the verification method as it has lower service cost compared to zkML.

### ERC7007 Function Interface

Below is the smart contract interface of ERC7007. Other applications can adopt this standard easily by inheriting this smart contract interface and implementing their custom logic.

```solidity
pragma solidity ^0.8.18;

interface IERC7007 is IERC165, IERC721 {
    event Mint(
        uint256 indexed tokenId,
        bytes indexed prompt,
        bytes indexed aigcData,
        string uri,
        bytes proof
    );

    function mint(
        bytes calldata prompt,
        bytes calldata aigcData,
        string calldata uri,
        bytes calldata proof
    ) external returns (uint256 tokenId);

    function verify(
        bytes calldata prompt,
        bytes calldata aigcData,
        bytes calldata proof
    ) external view returns (bool success);
}
```

### Story Protocol (Testnet)
![photo_2024-02-26_12-25-09](https://github.com/7007-Studio/gitbook/assets/153342102/3e96ad27-879f-4ce5-9391-af060e5c2a9c)

7007.studio performs IP Asset registration for each AIGC NFT using the story Protocol, which contains the Prompt used to generate the content and its corresponding generation result.

All Prompts and generated results can be used on the Story Protocol, and owners can edit the License for individual content, providing more diverse commercial licensing models and revenue streams.
