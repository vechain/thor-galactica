# Faucet Instructions

This document will guide you through the steps to obtain VET and VTHO. VTHO is the token used for gas in VeChain. More details about these tokens can be found [here](https://docs.vechain.org/introduction-to-vechain/dual-token-economic-model).

The main prerequisite is to have a wallet, such as [VeWorld](https://chromewebstore.google.com/detail/veworld/ffondjhiilhjpmfakjbejdgbemolaaho?pli=1), installed in your browser.

## Devnet

We will be using this [custom faucet](https://faucet-galactica.dev.node.vechain.org/).

1. Once you are in the website, click `Connect`, that will open the VeWorld extension.
2. After that, click `Sign` to `Sign Certificate`:

   <img src="faucet-devnet-sign.png" alt="Faucet Landing Page" style="width: 100%; max-width: 1000px;">

3. And that would be it! You should be able to see now the transaction ID:

   <img src="faucet-devnet-tx.png" alt="Faucet transaction" style="width: 60%; max-width: 600px;">

4. And if [you check the API](https://galactica.live.dev.node.vechain.org/doc/stoplight-ui/#/paths/transactions-id/get) using that ID you will see 2 clauses, the first one for the VET transfer and the second one for the VTHO one (`0x0000000000000000000000000000456e65726779` is the VTHO contract address):

   <img src="faucet-devnet-api.png" alt="Faucet Api Call" style="width: 60%; max-width: 600px;">

## Testnet

We will be using [VeChain Faucet](https://faucet.vecha.in/).

1. Navigate to the faucet website and click on the `Claim Tokens` button. This will bring up the VeWorld extension:

   <img src="faucet-landing.png" alt="Faucet Landing Page" style="width: 100%; max-width: 1000px;">

2. Within VeWorld, click on the `Sign` button to `Sign Certificate`.

That's it! You should now see a confirmation indicating that you have received VET and VTHO (500 and 50, respectively):

   <img src="faucet-confirmation.png" alt="Faucet Confirmation" style="width: 100%; max-width: 600px;">

With these tokens, you can start working on the VeChain testnet. Remember that you can swap VET for VTHO if you need more funds, using VeWorld for that purpose.