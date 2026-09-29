<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://cdn.openfsp.org/logo/openfsp-logo-inverse.svg">
  <img src="https://cdn.openfsp.org/logo/openfsp-logo.svg" alt="OpenFSP" width="320">
</picture>

**An open standard for payment interoperability in Haiti**

</div>

[Lire en français](README.fr.md)

Haiti has working digital payment services and no interoperability between them. Every
merchant integration is written from scratch, per provider, in every language. Provider
sandboxes let you test a payment that succeeds, but not reproduce on demand the ones that
fail, and those are the ones that cost money. Adding a second provider means writing a
second integration.

OpenFSP proposes a single open protocol for merchant integration with every payment
provider, together with a self-hosted gateway that implements it and thin client SDKs.

```mermaid
flowchart TD
    A["<b>Your application</b><br/>PHP, TypeScript, Python, ..."]
    G["<b>OpenFSP Gateway</b><br/><i>you deploy it, you hold the credentials</i>"]
    P["<b>Payment service providers</b>"]

    A -- "OpenFSP protocol&nbsp;&nbsp;HTTP + JSON" --> G
    G -- "each provider's own API" --> P
```

Provider integration is written **once**, in the gateway, and every language gets it.

## What we build

| | |
|---|---|
| 📚 **The specification** | The protocol: data model, payment lifecycle, capabilities, errors, idempotency, webhooks. Settled in the open through an ADR process. |
| ⚙️ **The gateway** | A self-hosted Kotlin and Spring Boot server: OpenFSP protocol in, provider APIs out. One adapter per provider. |
| 🧪 **The mock server** | Imitates real providers, failure modes included, so you can build and test without a merchant account. |
| 📦 **The SDKs** | Thin protocol clients, idiomatic per ecosystem. Plain HTTP always works too. |
| ✅ **The conformance suite** | Machine-executable: the report is reproducible by anyone. |

## What OpenFSP is not

Permanent boundaries, not a description of an early stage:

- It **does not hold or move funds**.
- It **operates no hosted service**. You deploy the gateway.
- It is **not a licensed payment institution**, and replaces no licence or agreement.
- It is **not a switch or settlement system**.

## Principles

- **Nothing is ever faked.** An operation a provider cannot perform is absent and
  discoverable as absent, never emulated.
- **Never silently degraded.** No automatic failover, no partial success reported as
  success.
- **Safe to retry.** Every mutating operation is idempotent, because networks fail
  between the request arriving and the response returning.
- **Boring on purpose.** HTTP, JSON, existing standards. Implementable with a standard
  library.
- **Open, and unable to close.** Apache-2.0 throughout, no contributor licence agreement.

## Status

**Specification draft.** Eighteen ADRs and the specification they ground are written, in French.
Not for production use. The protocol is settled in the open first; implementation follows,
starting with the mock server and the conformance suite, then the gateway.

The work is phased, and two phases are scoped so far: the protocol with its gateway, then
proximity payment at a counter. The protocol is built to grow, not to be finished.

This is the best moment to influence it.

## Where to start

| | |
|---|---|
| [**adrs**](https://github.com/openfspht/adrs) | The specification (the rules) and the ADRs (the decisions), with the bibliography. |
| [**openfsp**](https://github.com/openfspht/openfsp) | Governance, contribution rules, the provider registry. |

## Contributing

Developers, payment service providers, financial institutions, researchers and public
authorities are all welcome, through the same public ADR process, with no private track.

Governance, the declared interests of the project's steward, and the conditions under
which governance opens to a steering committee are all written down rather than implied.

## Licence

**Apache-2.0**: the specification, the gateway, the mock server, the SDKs, and the
conformance suite alike. Contributions under the Developer Certificate of Origin: you
keep your copyright, nothing is assigned, and the project cannot be re-closed later.

---

<sub>Stewarded by <a href="https://karakosystems.com">Karako Systems</a> · Built in Haiti, for Haiti.</sub>
