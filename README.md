# Aduna (aduna)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Aduna is the Ericsson-led network API joint venture — a 50:50 company owned half by Ericsson (Stockholm, Sweden) and half by twelve global communications service providers including AT&T, Bharti Airtel, Deutsche Telekom, KDDI, Orange, Reliance Jio, Singtel, Telefonica, Telstra, T-Mobile, Verizon and Vodafone, with e& added later as an equity partner. Announced from Stockholm and incorporated as Aduna Global, LLC, it exists to aggregate CAMARA-standardised mobile network APIs from many carriers into one commercial channel so that developers do not have to negotiate operator by operator.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/aduna/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/aduna/refs/heads/main/apis.yml)

## Tags

- Telecommunications
- Sweden
- Network APIs
- CAMARA
- Open Gateway
- API Aggregator
- Identity Verification
- SIM Swap
- Number Verification
- Fraud Prevention
- Quality on Demand
- Device Location
- Ericsson

## Timestamps

- **Created:** 2026-07-25
- **Modified:** 2026-07-25

## The API posture, honestly

Aduna sits in the exposure layer of the telecom value chain. It does not own spectrum, and it does not sell to developers directly at scale — it aggregates operator capability and reaches the market through partner platforms: Google Cloud, Infobip, Sinch, Vonage, Microsoft Azure and the Azure Marketplace, Comviva on AWS, and Bridge Alliance.

The developer surface is partner-gated:

- `https://adunaglobal.com/` (**200**) is a marketing site. It names its API catalogue in prose across six segment pages and publishes no technical artifacts.
- `https://docs.adunaglobal.com/` (**302 → login**) is GitBook-hosted, and every path — including `/robots.txt` and `/sitemap.xml` — redirects to an Auth0 login wall.
- `https://portal.adunaglobal.com/` (**200**) is an Angular single-page app that renders nothing without authentication. `/openapi.json`, `/swagger.json`, `/api-docs` and `/docs` all return the same SPA shell, not a specification.
- `https://adunaglobal.com/openapi.json` returns **404**. `api.adunaglobal.com`, `developer.adunaglobal.com` and `developers.adunaglobal.com` do not resolve.
- The domain `aduna.global` does not resolve at all. The real primary domain is `adunaglobal.com`.

There is **no public OpenAPI, no sandbox, no self-serve signup, no published base URL, no pricing and no rate-limit documentation.** Aduna's own SDK README states the onboarding procedure plainly: *"Contact Aduna Global for the onboarding procedure of an ASP Application."*

## What IS public

The one genuinely open surface is [github.com/adunaglobal](https://github.com/adunaglobal) — six public repositories, five of them source-available first-party SDKs for CAMARA Number Verification v2 (Java/Spring Boot, Kotlin/Android, Swift/iOS, TypeScript/web, and an iOS XCFramework). They are source-available under a proprietary Aduna license, not open source, and are not published to npm or Maven Central.

Those repositories are the only place Aduna's real technical contract is visible:

| Confirmed from first-party SDK source | |
| --- | --- |
| `POST {baseURL}/auth/auth-info` | authentication options for a number or PLMN |
| `POST {baseURL}/auth/bc-authorize` | **CIBA** backchannel authentication |
| `POST {baseURL}/auth/token` | token exchange |
| `POST {baseURL}/number-verification/v2/verify` | CAMARA Number Verification v2.1 verify |
| `GET {baseURL}/number-verification/v2/device-phone-number` | CAMARA Number Verification v2.1 read |

Confirmed OAuth scopes: `openid`, `dpv:FraudPreventionAndDetection`, `number-verification:verify`, `number-verification:device-phone-number:read`. Confirmed headers: `Authorization`, `X-Correlator`. The base URL is a configuration property injected at onboarding and is not published — no host is asserted here because none is public.

## CAMARA posture

**Commercial aggregator of CAMARA APIs with live deployments, everything else partner-gated.** This is an implementation, not a press release: Number Verification is live across AT&T, T-Mobile and Verizon in the United States as of July 2026, and the SDKs prove a working contract with a real CIBA flow.

**Live or in development:** Number Verification, SIM Swap, KYC Match.

**Announced roadmap:** Device Swap, Call Forwarding Signal, Scam Signal, SIM Swap Subscriptions, KYC Tenure, Number Recycling, Device Reachability Status, Device Roaming Status (and their subscription variants), Device Location Verification, Device Location Retrieval, Device Geofencing Subscription, Quality on Demand, Connectivity Insights, Dedicated Networks, Population Density, Region Device Count, Rain Attenuation.

**Markets live:** United States, Germany, Spain, Canada, France, Netherlands. **Announced:** Australia, Brazil, India, Greece, Singapore, Thailand, United Kingdom. Aduna states aggregation across 40 mobile operators.

**GSMA Open Gateway:** Aduna is not an operator and is not an Open Gateway signatory. Its GitHub organisation profile names GSMA Open Gateway as an ecosystem it builds upon, and all twelve of its CSP shareholders are Open Gateway operators. Aduna is the commercial aggregation channel *for* Open Gateway, not a member *of* it.

**TM Forum:** no Open API conformance certification claimed anywhere. **3GPP:** no NEF/SCEF, slicing or MEC surface published.

## APIs

### Aduna Number Verification API

Aduna's aggregated implementation of the CAMARA Number Verification API (v2.1), confirming possession of a mobile phone number in real time by verifying it directly against the carrier network, as a replacement for SMS one-time passwords.

- **Human URL:** [https://adunaglobal.com/api-segments/security/](https://adunaglobal.com/api-segments/security/)

#### Properties

- [Documentation](https://adunaglobal.com/api-segments/security/)
- [API Reference](https://docs.adunaglobal.com/how-to-enable-an-api/number-verification-api-v-2.1-landing-page) — gated
- [SDK — Java](https://github.com/adunaglobal/nv2-asp-server-java-aduna-sdk)
- [SDK — Android](https://github.com/adunaglobal/nv2-asp-android-aduna-sdk)
- [SDK — iOS](https://github.com/adunaglobal/nv2-asp-ios-aduna-sdk)
- [SDK — Web](https://github.com/adunaglobal/nv2-asp-web-aduna-sdk)
- [SDK — iOS XCFramework](https://github.com/adunaglobal/cac-ios-aduna-sdk)
- [Upstream CAMARA specification](https://github.com/camaraproject/NumberVerification/blob/r3.2/code/API_definitions/number-verification.yaml) — CAMARA-published, not Aduna-published

### Aduna SIM Swap API

Real-time information about recent SIM card changes associated with a mobile phone number, so an application can detect account-takeover risk and trigger additional checks.

- **Human URL:** [https://adunaglobal.com/api-segments/security/](https://adunaglobal.com/api-segments/security/)

### Aduna KYC Match API

Compares customer-supplied identity attributes against the verified KYC data held by the user's mobile network operator, returning match results without returning personally identifiable information to the caller.

- **Human URL:** [https://adunaglobal.com/api-segments/identity/](https://adunaglobal.com/api-segments/identity/)

## Links

- [Website](https://adunaglobal.com/)
- [Documentation](https://docs.adunaglobal.com/) — gated
- [Developer Portal](https://portal.adunaglobal.com/) — Auth0 login wall
- [GitHub Organization](https://github.com/adunaglobal)
- [LinkedIn](https://www.linkedin.com/company/adunaglobal/)
- [Availability](https://adunaglobal.com/work-with-us/availability/)
- [Newsroom](https://adunaglobal.com/resources/?contentType=Newsroom)
