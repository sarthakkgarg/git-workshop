# XDC3DART

[![Version](https://img.shields.io/cocoapods/v/XDC3Swift.svg?style=flat)](https://cocoapods.org/pods/XDC3Swift)
[![License](https://img.shields.io/cocoapods/l/XDC3Swift.svg?style=flat)](https://cocoapods.org/pods/XDC3Swift)
[![Platform](https://img.shields.io/cocoapods/p/XDC3Swift.svg?style=flat)](https://cocoapods.org/pods/XDC3Swift)

A dart library that connects to interact with the xdc blockchain. It connects to an xdc node to send transactions, interact with smart contracts and much more!

XRC20 Methods:
1.getName  2.getDecimal  3.getSymbol  4.getTotalSupply  5.getAllowance  6.getBalanceOf  7.getApprove  8.decreaseAllowance  9.increaseAllowance  10.transferFrom 11.transferToken  12.transferXDC

## Example

To run the example project, clone the repo, and run `dart pub get` from the Example directory first.

## Requirements

## Installation

XDC3DART is available through [pub.dev](https://pub.dev). To install
it, simply add the following command to your project:

```
dart pub add XDC3DART
```

then 

Import 'package:XDC3DART';
```
Creating a XDC account
```
      final keyGen = RSAKeyGenerator()
        ..init(ParametersWithRandom(
            RSAKeyGeneratorParameters(BigInt.parse('65537'), bitLength, 64),
            secureRandom));

      final pair = keyGen.generateKeyPair();
      
      final myPublic = pair.publicKey as RSAPublicKey;
      final myPrivate = pair.privateKey as RSAPrivateKey;

      return AsymmetricKeyPair<RSAPublicKey, RSAPrivateKey>(
          myPublic, myPrivate);
    }

    final pair = generateRSAkeyPair(exampleSecureRandom());
    final public = pair.publicKey;
    final private = pair.privateKey;

    var private_key = private.hashCode.toString();
    var public_key = public.hashCode.toString();
    var bytes = utf8.encode(public_key); //Public
    var bytesPrivate = utf8.encode(private_key); //Private
    var sha1Result = sha1.convert(bytes);
    var sha256Result = sha256.convert(bytesPrivate);

Create an instance of XDC3DART. This will provide you access to a set of functions interacting with the blockchain.
```
guard let clientUrl = URL(string: "https://apothem-or-mainnet-url") else { return }

```
final client = Web3Client(rpcUrl, Client(), socketConnector: () {
  return IOWebSocketChannel.connect(wsUrl).cast<String>();

```
Now, we can interact with the XRC20 methods
### XRC20 Read methods

Creating an instance of XRC20
Now, we can interact with the XRC20 read methods.

name() → string Returns the name of the token.
```  final name =
        await client.call(contract: contract, function: tokenName, params: []);
    return '$name';
```
      
balanceOf(address token,address account) → uint256  Returns the amount of tokens owned by account.

```
 final balanceOf = await client.call(
        contract: contract, function: tokenBalanceOf, params: [ownerAddress]);
    return ('$balanceOf');
        }
  }
```
### XRC20 Write methods

For write methods, we need token owner private keys

transfer(address token, address recipient, uint256 amount) → Moves amount tokens from the caller’s account to recipient. It will return a transaction hash.
```
    final transfer = await Transaction.callContract(
      from: ownAddress,
      contract: contract,
      function: tokenTransfer,
      parameters: [receiver, transfer_value],
    );

    final transferDetails = await client.sendTransaction(credentials, transfer,
        chainId: null, fetchChainIdFromNetworkId: true);
    return ('$transferDetails');
  }
  ```
approve(address token, address spender, uint256 amount) → Sets amount as the allowance of spender over the caller’s tokens. It will return a transaction hash.

```
    final approve = await Transaction.callContract(
        contract: contract,
        function: tokenApprove,
        parameters: [spender, BigInt.from(approve_value)]);
    final approvel = await client.sendTransaction(credentials, approve,
        chainId: null, fetchChainIdFromNetworkId: true);
    return ('$approvel');
}
``` 

For increaseAllowance and decreaseAllowance we need an instance of XRC20 and private key of owner: 
 
increaseAllowance(XDCAccount account, address token, address owner, address spender, uint256 subtractedValue)
Automically increases the allowance granted to spender by the caller.

This is an alternative to approve.

Emits an Approval event indicating the updated allowance.

```
## Author

XDCFoundation, XFLW@xinfin.org

## License

XDC3DART is available under the MIT license. See the LICENSE file for more info.
