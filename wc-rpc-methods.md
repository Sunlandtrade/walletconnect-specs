# JSON-RPC Methods
This doc should be used as a *source-of-truth* and reflect the latest decisions and changes applied to the WalletConnect collection of client-to-client JSON-RPC methods for all platforms SDKs.

## Definitions
- **Nullables:** Fields flagged as `Optional` can be ommited from the payload.
- Unless explicitly mentioned that a response requires associated data, all methods response's follow a default JSON-RPC pattern for the success and failure cases:
```jsonc
// Success
result: true

// Failure
error: {
    "code": number,
    "message": string
}
```

## Pairings:

### wc_sessionPropose
Used to propose a session through topic A. Requires a success response with associated data. 
- Success response is equivalent to session approval.
- Error response is equivalent to session rejection.
- This method *might* require a special timeout, because it needs end-user interaction to respond.
- Proposer must use the relay parameter selected and sent by the responder, if different than the proposed one.
```jsonc
// wc_sessionPropose params
{
    "relays": [
        {
            "protocol": string,
            "data": string // Optional
        },
    ],
    "blockchainProposed": {
        "auth": string, // Optional
        "chains": [string] // CAIP-2 chain IDs
    },
    "permissions": {
        "jsonrpc": {
            "methods": [string]
        },
        "notifications": {
            "types": [string]
        }
    },
    "proposer": {
        "publicKey": string,
        "metadata": {
            "name": string,
            "description": string,
            "url": string,
            "icons": [string]
        }
    },
    "ttl": uInt64
}
```

```jsonc
// Success result
{
    "relay": {
        "protocol": string,
        "data": string // Optional
    },
    "responder": {
        "publicKey": string
    }
}
```

### wc_pairingDelete

### wc_pairingPing

## Sessions:

### wc_sessionSettle

### wc_sessionRequest

### wc_sessionUpdate

### wc_sessionUpgrade

### wc_sessionExtend
Used to extend the lifetime of a session.
- The expiry is the absolute timestamp of the expiration date, in seconds.
```jsonc
// wc_sessionExtend params
{
    "expiry": number
}
```

### wc_sessionDelete

### wc_sessionPing

### wc_sessionNotify