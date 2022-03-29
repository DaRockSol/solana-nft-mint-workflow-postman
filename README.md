# solana-nft-mint-workflow-postman
This is my collection of postman calls to the RPC API of Solana in an order for minting an NFT with metadata.

This is incomplete for now. I am chasing down some understanding of how the Solana blockchain works with transactions, tokens, nfts, etc. I will update an improve this as I increase my understanding.

# Disclaimer
Neither I, nor my current employer, endorse investment or the use of Solana as a way to make money. This is purely for learning purposes and for technical content.

# Fun Disclaimer
Now that the other part is out of the way. Let's have some fun and make use of a cool technology.

# Overall project
I will have many repos that I am using to increase my understanding of Solana and have some fun. I will also be integrating with some open source projects from my employer. This way I can have some fun and work at the same time ;). I recently built a microservice API demo using Solana via the Metaboss CLI and some other technologies to build NFTs (check out Metaboss here it is extra dope! https://github.com/samuelvanderwaal/metaboss) I will try to post to social media as often as I can to update different parts of this project.

## Goals
1. Use Solana without the current Solana or Metaplex SDKs. 
2. Learn how to just use the RPC API from Solana to execute transactions, make and manage new tokens, create nfts with metadata. Emphasis on Goal 1 here as well.
3. Getting over the hurdle of fulling understanding what it takes to encode metadata into a transaction. Currently the Metaboss project has allowed me to get closest to this understanding of how to properly encode transaction, but I am not quite there yet. I am reviewing the Metaboss source code to better understand the encoding part.
4. I want to build my own SDKs utilizing the HTTP RPC API. This may or not make sense to some, but I want to use the current ecosystem and SDKs to build my own. I get the most understanding of technology by doing that. Some of what I do will not always make sense, to you, or me ;), at least until I am done.
5. This postman collection is my gateway to building ontop of the HTTP RPC API.. I will grow it as much as possible. I may not include every HTTP RPC API function that Solana provides documentation for.

## Order of HTTP RPC APIs to Mint and NFT

> Note this is my best understanding of what HTTP RPC API functions to use to mint an NFT. It may be wrong or incomplete. I am always open to suggestions on what is going on.

The below calls and their description are what happens when an NFT is minted.

1. getMinimumBalanceForRentExemption - I don't really know why this is or is not needed.
2. getVersion - I don't really know why this is or is not needed.
3. getLatestBlockhash - When you make this call you get a blockhash id. I believe this is used in the transaction encoding process and/ or the transaction data. I think it is also used to validate the transaction at the end
4. sendTransaction - This function is used for a any transaction that needs to be sent. It is also used for the NFT minting process. The "<encoded-transaction-metadata>" part in the postman collection is where the transaction data and metadata for nfts are encoded before being sent to the solana API to be processed. You need an external process to do that. Once I understand that process I will explain that here. This returns the signature id of this transaction which is used in the next function.
5. getSignatureStatuses - This is used to ensure your transaction has been processed? You need to keep checking this to ensure your transction was executed on the solana blockchain correctly.
6. isBlockhashValid - This checks that the blockhas from number 3 is valid. I am not completely sure why that is needed.