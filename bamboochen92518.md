---
timezone: UTC+8
---

> 请在上边的 timezone 添加你的当地时区(UTC)，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区


# bamboo

1. 自我介绍：我是bamboo，目前是一個大學生，對智能合約開發和審計都有興趣，請多多指教

2. 你认为你会完成本次残酷学习吗？ 會
3. 你的联系方式（推荐 Telegram）[t.me/bamboo92518](http://t.me/bamboo92518)

## Notes

<!-- Content_START -->

### 2025.05.14

參考資料：

1. [DeFiHackLabs 解說影片](https://www.youtube.com/watch?v=uZTeYfYM6fM)
2. [EIP-3074](https://eips.ethereum.org/EIPS/eip-3074)
3. [EIP-4337](https://eips.ethereum.org/EIPS/eip-4337)
4. [EIP-4337 Video](https://www.youtube.com/watch?v=PZ8svp68NXM&ab_channel=PatrickCollins)
5. [EIP-6551](https://eips.ethereum.org/EIPS/eip-6551)
6. [EIP-7702](https://eips.ethereum.org/EIPS/eip-7702)
7. [Ethereum Accounts](https://decrypt101.gitbook.io/decrypt101/blockchain-platforms/ethereum/ethereum-accounts)

#### EIP 3074

1. EIP-3074 引入兩個新操作碼（opcode）：
   1. **`AUTH`**：驗證某個 EOA 的簽名，授權一段後續操作。
   2. **`AUTHCALL`**：代表該授權帳戶去執行一次交易，就像那個帳戶自己發的交易一樣。
2. 不像 ERC-4337 需要創建新的 smart account，EIP-3074 能讓現有 EOA 的功能升級。
3. 新增 opcode，執行上更有效率；不需 Bundler、EntryPoint 合約等配套系統。但由於必須修改 EVM opcode，因此升級需要社群共識。

#### EIP 4337

1. 不需要透過私鑰才能交易，各種off-chain的驗證方法也行（驗證邏輯由智能合約決定）
2. 交易會先被送到Alt-MemPool Node（又稱 UserOperation Pool or Bundler），由於這東西不在鏈上，所以不一定要用native token交易（甚至可由第三方代付），且可以把多筆交易打包成一個atomic operation
3. 交易送到Alt-MemPool Node並處理後，會再被送到鏈上的 `EntryPoint` 合約處理
4. 不需要對 Ethereum protocol 本身修改，完全在應用層完成

#### EIP 6551

1. 可以為每一個NFT（ERC721 token）創建一個合約帳戶，讓 NFT 能夠擁有資產、簽署訊息、執行操作
2. 因為帳戶與 NFT 綁定，轉移 NFT 就等於轉移帳戶擁有權，實現身份/資產一次轉移。

#### EIP 7702

1. `EOA` -> set code tx (0x04) -> Smart Contract Account
2. 在 Transaction Payload 新增`authorization_list = [[chain_id, address, nonce, y_parity, r, s], ...]`
   1. `chain_id`是你想在哪條鏈上交易
   2. `address`是你想呼叫（或授權）的合約地址
   3. `nonce`是你想在哪個nonce執行這個交易
   4. `y_parity, r, s`都是用來簽名的東西
   5. 即使list中的其中一筆交易沒過or失敗，剩下的還是會照樣執行（prevent DoS）
3. Account code part 是 delegate designator，格式為`0xef + 0100 + target address`
   1. Delegation indicators use the banned opcode `0xef`, defined in [EIP-3541](https://eips.ethereum.org/EIPS/eip-3541), to indicate that the code must be handled differently than regular code.

#### EIP 7702 vs EIP 3074 and EIP 4337

1. EIP 7702 不像 EIP 3074 新增一個 opcode，而是新增一個 transaction type，`AUTH` 被替換成 `verify` 或者 `authorize()`，`AUTHCALL`被替換成`execute`。
2. EIP 7702 不像 EIP 4337 需要在off-chain做驗證，也不需要`EntryPoint`和`UserOperation Pool`等，`UserOperation Pool`被替換成類似`authorization_list`的東西，因為 EIP 7702 的所有操作都在鏈上，自然不需要`EntryPoint`去連接鏈嚇得驗證到鏈上
3. 由於EIP 7702 可以將現有的EOA升級，不需要像 EIP 4337 用 `initcode`創建一個新的 smart contract wallet，比較省gas fee

### 2025.05.15

笔记内容

### 2025.05.16

笔记内容

### 2025.05.17

笔记内容

### 2025.05.18

笔记内容

<!-- Content_END -->