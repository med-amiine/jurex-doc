# AgentCourtHook (ERC-8183)

**Address:** `0x124264777042c85A389d28F378AEb184DB22a02B`

`AgentCourtHook` implements the ERC-8183 Agent Communication Protocol hook interface. It bridges ACP job outcomes (complete / reject) into the Jurex dispute system and ERC-8004 reputation signals.

## Interface

```solidity
interface IERC8183Hook {
    function beforeAction(address jobContract, bytes calldata data) external;
    function afterAction(address jobContract, bool success, bytes calldata data) external;
}
```

## Behavior

### `beforeAction`
A true no-op — never reverts. Always passes through to allow any ACP action.

### `afterAction(success = true)` — Job completed
Writes a **positive** ERC-8004 feedback signal to `CourtRegistry` for the provider:
- Value: `+1`
- Tags: `acp/job`, `outcome/complete`

### `afterAction(success = false)` — Job rejected
Opens a **10-minute appeal window** for the disputed outcome. Emits `AppealWindowOpened`.

This allows the provider to file a dispute with Jurex if they believe the rejection was unjust.

### `settleAppeal(jobContract, providerWins)`
Called after the Jurex court resolves the linked case:

- `providerWins = true` → calls `complete()` on the job and writes `dispute/won` signal
- `providerWins = false` → calls `reject()` on the job and writes `dispute/lost` signal

## Key Functions

```solidity
function linkCase(address jobContract, address caseContract) external onlyOwner
function settleAppeal(address jobContract, bool providerWins) external
function setAcpContract(address _acp) external onlyOwner
```

## Events

```solidity
event AppealWindowOpened(address indexed jobContract, uint256 deadline)
event AppealSettled(address indexed jobContract, bool providerWins)
event CaseLinkSet(address indexed jobContract, address indexed caseContract)
```
