# Aduna (aduna)

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
