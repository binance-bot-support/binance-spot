


# Binance JavaScript Wallet Connector



[![Code Style: Prettier](https://img.shields.io/badge/code%20style-prettier-ff69b4)](https://prettier.io/)
[![npm version](https://badge.fury.io/js/@binance%2Fwallet.svg)](https://badge.fury.io/js/@binance%2Fwallet)
[![npm Downloads](https://img.shields.io/npm/dm/@binance/wallet.svg)](https://www.npmjs.com/package/@binance/wallet)
![Node.js Version](https://img.shields.io/badge/Node.js-%3E=22.12.0-brightgreen)
[![Socket Badge](https://socket.dev/api/badge/npm/package/@binance/wallet)](https://socket.dev/npm/package/@binance/wallet)
[![Docs](https://img.shields.io/badge/docs-online-blue?style=flat-square)](https://binance.github.io/binance-connector-js/modules/_binance_wallet.html)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)





This is a client library for the Binance Wallet API, enabling developers to interact programmatically with Binance's Wallet trading platform. The library provides tools to interact with wallet related functions like dust convert/ query balance etc through the REST API:









## Supported Features

- REST API Endpoints:
  - `/sapi/v1/account/*`
  - `/sapi/v1/accountSnapshot/*`
  - `/sapi/v1/asset/*`
  - `/sapi/v3/asset/*`
  - `/sapi/v1/capital/*`
  - `/sapi/v1/spot/*`
  - `/sapi/v1/system/*`
  - `/sapi/v1/localentity/*`
  - `/sapi/v2/localentity/*`
- Inclusion of test cases and examples for quick onboarding.






```bash
npm install @binance/spot
```



## Balance

```js

import { Spot } from "@binance/spot";

// Configura tus credenciales (se recomienda usar variables de entorno)
const configurationRestAPI = {
  apiKey: 'TU_API_KEY',
  apiSecret: 'TU_SECRET_KEY' // Si utilizas autenticación HMAC estándar
};

const spotClient = new Spot({ configurationRestAPI });

async function getSpotBalance() {
  try {
    // Llama al endpoint de información de la cuenta spot
    const response = await spotClient.restAPI.getAccount();
    const accountInfo = response.data;

    console.log("--- Balances Spot ---");
    // Filtra para mostrar solo los activos que tienen saldo disponible o bloqueado
    accountInfo.balances.forEach(asset => {
      const free = parseFloat(asset.free);
      const locked = parseFloat(asset.locked);
      
      if (free > 0 || locked > 0) {
        console.log(`Moneda: ${asset.asset} | Disponible: ${free} | En Órdenes: ${locked}`);
      }
    });

  } catch (error) {
    console.error("Error al obtener el balance:", error);
  }
}

getSpotBalance();


```




```js

import { Spot } from '@binance/spot';

// Configura tus credenciales (se recomienda usar variables de entorno)
const spotClient = new Spot({
  configurationRestAPI: {
    apiKey: process.env.BINANCE_API_KEY,
    privateKey: process.env.BINANCE_PRIVATE_KEY, // Soporta firma RSA/Asimétrica o HMAC Secret Key
  }
});

async function retirarCripto() {
  try {
    // El método invoca el endpoint POST /sapi/v1/capital/withdraw/apply
    const respuesta = await spotClient.restAPI.withdraw({
      coin: 'USDT',                               // Criptomoneda a retirar
      network: 'TRX',                             // Red (ej. TRX para TRC20, BSC para BEP20, ETH para ERC20)
      address: 'TYM6y....DIRECCION_DE_DESTINO',    // Dirección de la billetera destino
      amount: 100,                                // Cantidad a retirar
      walletType: 0                               // 0 para Billetera Spot, 1 para Billetera de Fondos
    });

    console.log('Retiro solicitado con éxito:', respuesta);
  } catch (error) {
    console.error('Error al procesar el retiro:', error);
  }
}

retirarCripto();


```






## Documentation

For detailed information, refer to the [Binance API Documentation](https://developers.binance.com/docs/wallet).





## Contributing

Contributions are welcome!






Thank you for your contributions!

## Disclaimer

This SDK is provided by Binance on an "as is" and "as available" basis for use at your own risk. Binance makes no representations or warranties of any kind, whether express or implied, as to the operation of the SDK, its accuracy, reliability, completeness, or fitness for any particular purpose.

To the fullest extent permitted by law, Binance shall not be liable for any losses, damages, or expenses of any kind arising from or in connection with your use of, or inability to use, this SDK, including but not limited to any financial losses resulting from errors, bugs, interruptions, or inaccuracies in the SDK.

Your use of this SDK to access the Binance Platform is subject to the Binance API Key Terms and the Binance Terms of Use, which shall prevail in the event of any conflict with this disclaimer. You are solely responsible for any orders or transactions executed through the Binance Platform using this SDK.

This SDK is not intended to constitute investment advice or a recommendation to buy, sell, or hold any digital asset. You should independently evaluate and verify all information before acting.

- [Binance Terms of Use](https://www.binance.com/en/terms)
- [Binance API Key Terms](https://www.binance.com/en/about-legal/terms-binance-api)

## Licence

This project is licensed under the MIT License. See the <strong>LICENCE</strong> file for details.







