# Blockchain

- Consensus mechanism
- Proof of stake



```javascript
// block들이 들어있는  blockchain
// like Database
// Append only
// Decentralization - all have copy
let blockchain = {
	1: [block_hash_previous_block_hash, block_data],
	2: [block_hash_previous_block_hash, block_data],
	3: [block_hash_previous_block_hash, block_data],
    ...
}

// 새로운 블록은 새로운 데이터 + 이전블록의 해시를 합쳐서 다시 해시한다.
let keysOfBlockchain = Object.keys(blockchain);
blockchain[keysOfBlockchain[keysOfBlockchain.length - 1] + 1] = 
    // previous hash
    [Nonce, hash(keysOfBlockchain[keysOfBlockchain.length - 2],
          // new hash
          blockchain[keysOfBlockchain[keysOfBlockchain.length - 2]]),
     	  // new data
          transaction];

// One way function
// Deterministic
function hash(preHash, data) {return encryption(preHash + data);}
```





Proof of work

data of block , nonce (difficulty)