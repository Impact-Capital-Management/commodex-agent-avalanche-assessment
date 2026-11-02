# Evidence register — Avalanche Fuji (chain id 43113)

Newest first. A row is added only after the transaction is mined and opened on the explorer.

| Date (UTC) | Step | Requirement | Block | Explorer | What it proves |
|---|---|---|---|---|---|
| 2026-11-02 | First escrow trade on Fuji: buyer funds 1 USDC, then releases it | FR-03 | 60383092, 60383096 | https://testnet.snowtrace.io/tx/0x68fe1c6fade7af222b4aa99363c8d7eb52d578ac63242733de14c43d4359d519 and https://testnet.snowtrace.io/tx/0xa69f086729fcd392e3e5d29989aa561a7135f44e3bee290813ef4405e25da9c9 | The full buyer path works on chain with Circle test USDC; the seller is a stand-in (the Commodex operator wallet), not a counterparty |
| 2026-11-01 | CommodexEscrow v2 source verified on the explorer; independent check 11/11 | FR-03 | — | https://testnet.snowtrace.io/address/0xe453ebae20f06d53c44946b15A35E0e790A3089e/contract/43113/code | The deploy input is byte-for-byte the published build plus its constructor arguments (`checks/verify-fuji-escrow.mjs` in commodex-agent-contract-assurance) |
| 2026-11-01 20:43 | CommodexEscrow v2 deployed at `0xe453ebae20f06d53c44946b15A35E0e790A3089e` on Circle Fuji USDC | FR-03 | 60366934 | https://testnet.snowtrace.io/tx/0xa97409ec2d65e404c6e40cee52b9db715556ba1050282f0c2727b2c1435ca293 | Stablecoin escrow is live on Fuji: buyer releases; operator force-releases after a 7-day deadline; operator alone resolves disputes; fee 0%; test USDC only |
| 2026-10-11 16:00 | App anchors Pool-to-Pool match root `P2P_ROOT` | FR-03 | 59309318 | https://testnet.snowtrace.io/tx/0x54a4a46708d4bbdd641f9f4f14fb88c085f2af29d35295834f4d6caab4ec38e6 | A 12-buyer match is fixed on chain; each buyer proves their share with a Merkle proof against the anchored root |
| 2026-10-11 16:00 | App anchors `tax` ledger head `LEDGER_HEAD` | FR-03 | 59309310 | https://testnet.snowtrace.io/tx/0x3a1c5d0093de40c15deed22f9a568c0a1b2ad04f66f5ae084771583c69e45ac9 | The hash-chained corridor ledger is timestamped on Fuji by the app itself |
| 2026-10-11 15:59 | App sends its first anchor (`TEST`) | FR-01 | 59309304 | https://testnet.snowtrace.io/tx/0x41a6b23d19891b6fa92896242dbfd827c6b8707eeb36f0855ce4c57d23469e42 | The staging app signs and sends with its own operator wallet |
| 2026-10-11 15:32 | `setOperator` to the server wallet | FR-01 | 59308707 | https://testnet.snowtrace.io/tx/0xcca9d1976ab774685cef487e1475ee685f19960e5af56ba73973a731c1e9f9f7 | Only the Commodex server can anchor from now on |
| 2026-10-11 15:32 | Server wallet funded for gas | — | 59308703 | https://testnet.snowtrace.io/tx/0xe931ef101e016bbad59cc04a1a8db6b147c55e495bbcd013e98811e6af9dc3c3 | Test AVAX only |
| 2026-10-11 | Contract source verified on the explorer | FR-03 | — | https://testnet.snowtrace.io/address/0xe274C452dFb0D259FA413EEd3a830197a4Fd50ef/contract/43113/code | Anyone can read the deployed code; it matches the source in commodex-agent-avalanche-contracts |
| 2026-10-11 14:08 | First anchor, kind `TEST` | FR-01 | 59306896 | https://testnet.snowtrace.io/tx/0x2384d975b453a523524346ce7cd00e8d039bd8c4b6e7ec2ea73e1f5970077bef | The Commodex operator wallet records a hash on Fuji with no participant wallet; `Anchored` event emitted |
| 2026-10-11 14:07 | CommodexAnchor v0 deployed at `0xe274C452dFb0D259FA413EEd3a830197a4Fd50ef` | FR-03 | 59306874 | https://testnet.snowtrace.io/tx/0x24efb4ba147d4dab9cd9ae98a11edddd53b4ae4dc1cd861f5a8b44a66a3673a4 | Gate M0 / milestone M2.2: the hash-anchor contract is live on Fuji; deploy input equals the published build |
| 2026-10-11 | CommodexAnchor v0 built | FR-03 | — | — | Contract and 7 local tests; reviewed by contract assurance (one medium finding, fixed before deploy) |

How each row was checked on 2026-10-11: transaction receipts read from the public Fuji RPC
(`https://api.avax-test.network/ext/bc/C/rpc`, `eth_chainId` = `0xa869`), status `0x1`, sender
`0xa6547c2812140c0495113d4490eb0f2805A67ecD`; `anchoredAtBlock(0x8b8d8a98…eae3fc00)` returns 59306896.

## Acceptance status

| Req. | Evidence required | Status |
|---|---|---|
| FR-01 | Operator submits on Fuji 43113 (no participant wallet) | **demonstrated 2026-10-11** (block 59306896) |
| FR-02 | Rehearsal PO on staging with document SHA-256s | not yet demonstrated |
| FR-03 | Document-hash tx recorded on Fuji against the PO | started 2026-10-11: app anchors ledger heads and a Pool-to-Pool root; 2026-11-01: USDC escrow contract deployed and verified on Fuji; 2026-11-02: first funded and released trade. Next: escrow wired into the staging app, then a settled PO anchor |
| FR-04 | Each contribution traced to a full commit | not yet demonstrated |
