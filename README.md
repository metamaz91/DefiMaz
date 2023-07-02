# DefiMaz

import { WagmiConfig, createConfig, mainnet } from 'wagmi'
import { createPublicClient, http } from 'viem'

const config = createConfig({
  autoConnect: true,
  publicClient: createPublicClient({
    chain: mainnet,
    transport: http(),
  }),
})

function App() {
  return (
    <WagmiConfig config={config}>
      <Profile />
    </WagmiConfig>
  )
}
import { useAccount, useConnect, useDisconnect } from 'wagmi'
import { InjectedConnector } from 'wagmi/connectors/injected'

function Profile() {
  const { address } = useAccount()
  const { connect } = useConnect({
    connector: new InjectedConnector(),
  })
  const { disconnect } = useDisconnect()

  if (address)
    return (
      <div>
        Connected to {address}
        <button onClick={() => disconnect()}>Disconnect</button>
      </div>
    )
  return <button onClick={() => connect()}>Connect Wallet</button>
}
In this example, we create a wagmi config and pass it to the WagmiConfig React Context. The config is set up to use viem's Public Client and automatically connect to previously connected wallets.

Next, we use the useConnect hook to connect an injected wallet (e.g. MetaMask) to the app. Finally, we show the connected account's address with useAccount and allow them to disconnect with useDisconnect.

We've only scratched the surface for what you can do with wagmi!
Going well
