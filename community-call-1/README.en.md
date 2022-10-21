<h1> <img src="https://connextscan.io/favicon.png" style="width: 40px"> Connext Community Call #1 </h1>

This is the very first Community Call on Connext, announced after the end of Community Program Phase 1.

## 🗒 Agenda
1. [Who is Connext](#🔎-who-is-connext)
2. [Amarok is Coming](#🐺-amarok-is-comming)
3. [Community](#🎏-community)
4. [Q&A](#qa)

## 🔎 Who is Connext?

<details><summary> <b>🛠 BUIDLing since 2017</b> </summary>

> _this session was moderated by [Arjun](https://twitter.com/arjunbhuptani)_

<p align="center"><img src="img/buidling-since-2017.png" width="500"></p>

#### 2017
Connext team have jumped into the blockchain space and have been BUIDLing since 2017. "We built Connext because we want to bring blockchains to the broader comsumer public. This is something that people hadn't even begun to think about. The ETH price was around 20-30 USD at the time", said Arjun. This is the question that leads to the thesis of **blockchain scalability**.

#### 2018
With the goal of solving **blockchain scalability**, the team became one of the first L2 R&D Team. Arjun and the team have built the first layer-2 on Ethereum, which was the [State Channel Networks](https://ethereum.org/en/developers/docs/scaling/state-channels/) designed for payments. Later, the team have worked with other L2 teams such as OmiseGO team, Matic team.

#### 2020
In 2020, the community the market started to realized that Roll-ups were going to be the future of scalability. At this point, Connext team saw that communication between  is necessary and have built a very first Arbitrum-Optimism bridge called [Spacefold](https://github.com/connext/spacefold) as a POC. This is the very first trust-minimized cross-chain bridge for rollups.

By the end of 2020, the team have built the early implementation of scalability solution targeted for payment that can do cross-chain transfer called [Vector](https://github.com/connext/vector). The team have worked with many projects in the ecosystem. Around this time, the team have been collaborating with [1Hive](https://1hive.org/) have built a POC bridge that later become **xpollinate** (The old name of Connext Bridge, read more [here](https://blog.connext.network/xpollinate-is-now-connext-bridge-d294baea94c2)).

#### 2021
Later in 2021, the team were able to ship NXTP, which is a more stable implementation of the network. At that time, the NXTP is quite unstable, most assumption on liveliness of routers, stability, etc. are incorrect. This cause the team to take more that a year for the upcoming upgrade to the network. This new updates will solve the existed issues, and even improve the stability as well as allows generalized communication among chains.

#### 2022
That update is the Amarok upgrade 🐺

</details>

<details id="why-connext"><summary> <b>🤔 Why Connext?</b> </summary>

> _this session was moderated by [Arjun](https://twitter.com/arjunbhuptani)_

There're key principles that Connext helped shape how Connext is. The very first key principle in designing Connext Network was the **Security**

> 🔒 Security

The team focus on the security as the first priority and have been doing this for 5 years of building Connext.

One of the key realization is that the Web3 space move very quickly that it's not a good idea to bet on any single structure of security model. Thus, this lead us to the second and third principle which are **Modularity**, **Extensibility**, and **Future-Proof**

> 🧩 Modularity<br>
🔌 Extensibility<br>
📡 Future-Proof

_Modularity_ allows the design of infrastrusture to composed of different module that is easy to plug-in and plug-out. This allows the network to be able to adapt with the new technology and robust to changes.

_Composability_ is the key principle that make Connext easily integrated with different blockchains with minimal effort. The future of Connext is to build a xApps that would live on multiple chains. The concept of how users acknowledge which chains they're on would be removed.

The last key value of Connext is the **Ease of Implementation**

> 🌈 Ease of Implementation

The _Ease of Implementation_ for Connext allows the experience of building on Connext seamless.

</details>

## 🐺 Amarok is Comming

<details><summary> <b>🐺 Amarok</b> </summary>

> This session was moderated by [Layne](https://twitter.com/laynehaber)

In the upcoming Amarok upgrade, there's going to be several new features listed below:
- **🖱 1 click UX** - The current version required user to sign before releasing tokens. This is worse in term of UX. Amarok upgrade remove this procedure.
- **⛲️ Better Liquidity** - Currently, Connext routers provides LP on two chain side, this requires routers to always rebalance an asset when the demand is high on one specific chains.
- **🤑 Cheaper & Faster txs** - The Amarok upgrade allows the cross-chain transaction to be initialized on source chain and complete on destination chain. This simplies the process and make cross-chain transaction faster and cheaper.
- **🤖 Arbitrary Message Passing** - This is not available in NXTPv0 as the information can assign a financial values. With Amarok, people can build apps that can communicate with arbitrary message.

</details>

<details><summary> <b>🪢 How it works: Modular Architecture</b> </summary>

> This session was moderated by [Layne](https://twitter.com/laynehaber)

Arjun have mentioned about modular architecture in [`🤔 Why Connext?`](#why-connext) section. Connext abstract cross-chain communication into different module as seen in figure below.

<p align="center"><img src="img/modular-architecture.png" width="500"></p>

- `Transport Layer` - Defines how to get data from chain A to B. Connext use a messaging system that use the default rollup bridges in a [hub and spoke model](https://0xpostman.medium.com/honk-if-you-like-hub-spoke-7b55cba84c0d) to pass a data through from origin chain, to hub, to the destination spoke.
- `Verification Layer` - Evalate the veracity of the message from chain A to B. By default, Connext will use Optimistic Bridge. With the modular design, the verification layer can be changed depending on the path. For example, if we bridge Ethereum to IBC, the first leg would use Optimistic Bridge as a verification layer while on Cosmos use IBC verification.
- `Execution Layer` - This layer packs messages and defines how the message will be put into the transport and verification layer.
- `Liquidity Layer` - Providing a easy-to-use interface for developers and managing asset complexity. This allow users to receive the token that is mainly used on the destination chain apart from the minted asset (e.g. USDC instead of anyUSDC or nextUSDC). This is the layer that user interacted with.

When we put the transaction lifecycle together, we get the following picture:

<p align="center"><img src="img/txn-flow.png" width="500"></p>

Let's look at the Polygon<>Optimism bridge transaction. 
1. User send DAI to the liquidity layer via `xcall` function.
2. DAI is then swap to NextDAI and burn.
3. The message was sent to the Optimism AMB directly to contract on Ethereum. The messages from all of the connected Spokes then push them back out to the destination chain.
4. Optimism AMB push the message to the Optimism chain, ready to be executed.
5. NextDAI was minted on the Optimism and swapped back to DAI for user on Optimism.

No matter what ecosystem users are in, the user experience remains the same. For example, we use AMB on the rollups within Ethereum. But if we change the ecosystem to Cosmos, then we use IBC instead. Similarily, on Polkadot will use XCMP. This is the benefits of using a modular architecture as we can plug-in components in and out to support different communication channel on different chains.

</details>

<details><summary> <b>📞 xCalls</b> </summary>

> _this session was moderated by [Rahul](https://twitter.com/rhlsthrm)_

What Connext wanted to do is to build a infrasturcture for people to make use of it instead of building a UI application. The only thing that developer have to learn to connect their apps is a function call `xcall`. 

<p align="center"><img src="img/xcall.png" width="500"></p>

This `xcall` is very similar to solidity native function `call`. The difference is that `xcall` was designed to do the cross-chain transaction via Connext. The process can be simplifies as shown in the figure above.
- xApp (cross-chain Apps) called `xcall` into Connext.
- Connext takes care of bridging, AMBs, routing, etc. and call some function on some chain.
- Get the data back to xApp in a form of callback.

</details>

<details><summary> <b>📞 xApps are the Future</b> </summary>

> _this session was moderated by [Rahul](https://twitter.com/rhlsthrm)_



</details>

## 🎏 Community

## 📌 Q&A


## 🌊 Author
`chompk.eth | Contribution DAO#9502`