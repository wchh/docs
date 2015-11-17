# 用户发行资产 User-Issued Assets


**法规兼容的加密资产发行 Regulation-compatible cryptoasset issuance**

> BitShares平台提供了一个特性称为“用户发行资产”，对某些类型的服务有助于提升商业盈利模式。该术语指的是注册在该平台上自定义的一种类型的代币(token)，在一定范围内，用户可以持有或交易。类似这些资产的创建者公开他的姓名，介绍以及分发的代币，并指定个性化的需求，比如一份被用户认可的白名单允许持有这些代币，或者相关的交易费和转账费。

BitShares允许个人和公司发行他们自己的代币，可以代表他们想象的任何事物。常见的用例包括：

- [存款收据 Deposit Receipts](#dr)
  - [1. 了解你的客户 Know Your Customer KYC](#1kyc)
  - [2. 资产绑定 Asset Seizing](#2as)
  - [3. 市场约束 Market Restriction](#3mr)
  - [4. 交易约束 Transfer Restrictions](#4rr)
- [公司股份 Company Shares](#cs)
- [活动门票 Event Tickets](#et)
- [奖励积分 Rewards Points](#rp)
- [个人或公司债务 Individual or Corporate Debt](#icd)
- [众筹 Crowd Funding](#cf)
- [数字资产Digital Property](#dp)
- [私有化的智能货币 Privatized SmartCoins (稳定的加密货币Stable Cryptocurrencies)](#ps)
- [信息/预测市场 Information/Prediction Markets](#ipm)
- [如何通过发行资产盈利 How to Profit by Issuing an Asset](#hpis)
  - [收费池 Fee Pools](#fp)

用户发行资产的潜在用例是无数的，各种代币的适用规则差别很大，并且每个司法辖区往往不同。BitShares提供工具允许发行人发布资产时，仍然符合所有适用的法规。

下面是几个用户发行资产的用例

## <span id="Deposit Receipts">存款收据</span>

Banks are simply companies that maintain a database of customer account balances and facilitate the transfer of these assets among their depositors. Companies like Dwolla and Paypal essentially issue deposit receipts, and then offer cheaper transfers among their users than between banks. With BitShares, it is now possible to move these internal databases onto the blockchain where the deposits can be used with other smart contracts such as the internal markets, escrow, or bonds.

In talking to many different banks and exchanges, we have learned a lot about what the law requires of those who wish to issue deposit receipts.

### <span id="1kyc">1. Know Your Customer</span>

First and foremost the issuer must know every single customer. BitShares supports this by enabling both whitelists and blacklists. Rather than requiring every issuer to whitelist every customer separately, an issuer may specify a set of identity verifiers that they trust to do this job. This allows issuers to benefit from the network effect of validated users without having to do any direct identity verification themselves.

When an asset enables whitelists, no account may send or receive that asset without being on an authorized whitelist. An accounts funds can be frozen by removing them from the whitelist.

### <span id="2as">2. Asset Seizing</span>

From time to time, an issuer may be required to seize funds as a result of a court order. While this may be unappealing to cryptocurrency purists, it is an unavoidable reality of trust-based assets. An issuer can determine whether or not they wish to revoke this privilege, but it may be a requirement in some jurisdictions.

### <span id="3mr">3. Market Restriction</span>

An issuer who offers both USD and EUR deposits may need to restrict direct trading between their USD and EUR assets to avoid being subject to foreign currency exchange regulations. Some cryptocurrency exchanges allow trading between fiat and cryptocurrencies, but not between two fiat currencies. Without this feature, many exchanges would be unable to issue their assets on the BitShares blockchain.

### <span id="4tr">4. Transfer Restrictions</span>

A transfer-restricted asset allows the holders of the asset to trade it in the markets but not transfer it from person to person. Only a few cryptocurrency exchanges allow user-to-user transfer of funds outside the market, because this particular activity is often subject to a different set of money transmission regulations.

The deposit receipt example is probably one of the most important, and yet most heavily regulated, use cases of user-issued assets.

## <span id="cs">Company Shares</span>
Corporate shares are heavily regulated by the SEC, but none of those regulations prevent them from being issued or traded on an alternative trading system. The regulations in many jurisdictions require all shares to be registered (aka held by known identities). BitShares corporate shares can be used as collateral for a bond or be used in any number of smart contracts.

## <span id="et">Event Tickets</span>
Event tickets are a largely unregulated use case for user-issued assets. Tickets to a school play could be issued as digital tokens that are auctioned off to the highest bidder, who would then resell them. This ensures that the ticket issuer raises as much money as possible up front, while transferring the risk of ticket sales on to speculators.

On the day of the event, the issuer can freeze all trading of the asset and then allow users to cryptographically check in.

## <span id="rp">Rewards Points</span>
Merchants around the world offer rewards points for loyal customers. These points are accumulated to earn discounts on future purchases. Rewards systems are a prime opportunity to add value by making them available to Bitshares smart contracts.

## <span id="icd">Individual or Corporate Debt</span>
Many businesses raise money by selling bonds. With BitShares, these bonds can be made tradeable and/or fungible, which makes them more compelling to investors.

## <span id="cf">Crowd Funding</span>
Whether being used as a transferable coupon for a pre-sale, or doing an IPO on a small company, issuing an asset is one of the most effective means of raising money for a cause.

## <span id="dp">Digital Property</span>
Software and music licenses can be made transferable by issuing them as a digital asset. Every copy of a program can check to make sure that the user has control of a token before running. Software implementing such a licensing scheme can remain functional even if the company that produced the license goes out of business.

Trading cards can be simulated by creating many limited issue assets. Online games can use these assets to represent game items.

## <span id="ps">Privatized SmartCoins (Stable Cryptocurrencies)</span>
Price-stable cryptocurrencies (aka SmartCoins) were the inspiration for BitShares. Now, users can create their own price-stable assets with custom parameters designed to track the value of any asset they can imagine. The benefit of price-stable cryptocurrencies is that they are fully collateralized, and the issuer only needs to be trusted to appoint an honest set of independent (non-collusive) feed producers. Unlike deposit receipts, the value of a Privatized SmartCoin is secured even if the issuer disappears.

Bitshares provides many parameters that an issuer may tune. In addition to account whitelists, market restrictions, and transfer restrictions, the issuer of a private SmartCoin has control over:

Collateral Type
Initial Collateral Rate
Maintenance Collateral Rate
Forced Settlement Fee, Delay, and Daily Volume
Price Feed Update Rate
Global Forced Settlement
With these tools it is possible to emulate a pure contract for difference with periodic global forced settlement (ie: monthly, yearly, etc), or to emulate BitShares 1.0 BitAssets by having a 30 day delay on forced settlement.

Arbitrary financial indexes can be used for the price feed to mimic all manner of exotic assets.

## <span id="ipm">Information/Prediction Markets</span>
A prediction market is a specialization of SmartCoins where there is no need for margin calls or forced settlement because all positions are fully collateralized at any price. A prediction market has a price between 0 and 1 and the issuer settles all positions after the event occurs and the final price is known. These prediction markets can be very secure if the issuer is a multi-sig account with many independent and trustworthy parties involved.

## <span id="hpia">How to Profit by Issuing an Asset</span>
There are many ways to profit from issuing an asset. As the issuer you have complete control over market fees and can tune parameters such as the percent of each trade that is collected as a fee. This percentage can be bounded by a minimum and maximum fee. The combination of these three parameters give issuers great flexibility in pricing.

### <span id="fp">Fee Pools</span>

Issuers may optionally maintain a Fee Pool. The Fee Pool is a pool of BTS and an exchange rate at which the issued asset may be converted into BTS. When a user wishes to pay a network fee with the asset, the fee pool will step in to convert the asset into BTS at the rate that the issuer has specified. This means that issuers may charge a premium every time users opt to use their asset to pay network fees rather than paying them directly with BTS.

The purpose of the fee pool is to provide a convenience to users that would like to use an asset without concerning themselves with the details of acquiring BTS. Anyone may fund the fee pool, but only the issuer may specify the exchange rate. This exchange rate is automatically set to the settlement price if the asset is collateralized by BTS.
