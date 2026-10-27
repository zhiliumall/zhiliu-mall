<p align="center">
  <img src="doc/images/zhiflow-banner.jpg" alt="ZhiFlow open-source Java e-commerce system built on JDK 25 and Spring Boot 4, with full source code" width="100%">
</p>

# ZhiFlow: Open-Source Java E-commerce System

[简体中文](README.md) | [繁體中文](README.zh-TW.md) | **English** | [日本語](README.ja.md)

[![License: AGPL-3.0](https://img.shields.io/badge/License-AGPL--3.0-blue.svg)](LICENSE)
![JDK 25](https://img.shields.io/badge/JDK-25-orange.svg)
![Spring Boot 4.1](https://img.shields.io/badge/Spring%20Boot-4.1-brightgreen.svg)
![Vue 3](https://img.shields.io/badge/Vue-3-42b883.svg)
![PostgreSQL 18](https://img.shields.io/badge/PostgreSQL-18-336791.svg)

ZhiFlow (智流商城) is open-source Java e-commerce software. This is the main backend repository of the ZhiFlow open-source edition, built with JDK 25, Spring Boot 4, Spring Security 7, PostgreSQL, Valkey, Vue 3 and uni-app. It targets single-store online shops and covers products, variants / SKUs, cart, orders, WeChat Pay, Alipay, members, access control, content and reports. Use it to learn, to evaluate e-commerce platforms, to build on, or to run your own shop.

If you are looking for a Java e-commerce system, shopping cart software or e-commerce source code, start here. If you need multi-store, multi-tenant SaaS, marketing and affiliate features, cross-border commerce, healthcare scenarios such as online consultations, more storefronts or commercial support, see [Licensing and editions](#licensing-and-editions).

## Project overview

- **Name**: ZhiFlow, a Java e-commerce system with full source code
- **About**: the open-source edition of our commercial platform ZhiFlow Store Engine (智流 · 开店引擎). The code comes from a shop system that has run in production for a long time; it is not a demo written for open source
- **Business model**: single-store shop with an admin console and an H5 storefront
- **Tech**: backend on JDK 25 + Spring Boot 4.1.1 + Spring Security 7.1.1, frontend on Vue 3 + uni-app; exact dependency versions are in the backend `pom.xml` and frontend `package.json`
- **Deployment**: modular monolith packaged as one jar; the only required services are PostgreSQL and Valkey (or Redis)
- **Open-source license**: AGPL-3.0, for learning, evaluation and any use that complies with the license
- **Commercial license**: closed-source commercial use, private deployment, commercial support and the full editions; see [Licensing and editions](#licensing-and-editions)
- **Commercial editions**: Standard, Cross-border and Healthcare; features and services are subject to the commercial contract
- **Links**: source repositories; see [Resources](#resources)

## Highlights

- JDK 25 + Spring Boot 4 + Vue 3, separate frontend and backend
- Modular monolith, one jar to deploy, no service registry or config server
- Spring Security 7 with the built-in OAuth2 Authorization Server
- PostgreSQL database, Valkey / Redis cache, Redisson distributed locks
- Real WeChat Pay and Alipay integration, not a mock payment
- State machines for both payments and orders; after each callback the system queries the payment channel again, and mismatches go into a reconciliation queue
- Modules talk only through API contracts; ArchUnit catches illegal dependencies at test time
- AGPL-3.0 open source; for commercial licensing and editions see [Licensing and editions](#licensing-and-editions)

## About the tech versions

The open-source edition is built directly on JDK 25 and Spring Boot 4.1. Spring Security 7, Tomcat 11 and PostgreSQL 18 are all current mainline releases, which makes the project a good fit for new builds and long-term maintenance. Shop systems still running on older framework versions usually pay more later in framework upgrades, dependency conflicts and security patches.

## Features

### H5 storefront

| Module | Features |
| --- | --- |
| Account | Username and password login, SMS code login (optional, requires an SMS provider), WeChat login, sign-up, profile, shipping addresses |
| Products | Home page, categories, product details, variant selection, search, trending searches |
| Checkout | Cart, order confirmation, payment page (WeChat Pay, Alipay), payment result |
| Orders | Order list, order details, cancel unpaid orders, confirm receipt |

### Admin console

| Module | Features |
| --- | --- |
| Products | Product publishing, variants / SKUs, categories, brands, inventory, media library |
| Orders | Order search, order details, shipping |
| Members | Member list, member details |
| Content | Home page banners, trending search terms |
| Reports | Basic order and sales reports |
| Access control | Admins, roles, menus, organizations, dictionaries |
| Settings | Store settings, system parameters, payment configuration |

### Not included in the open-source edition

These are available in the commercial editions:

- After-sales and refunds, coupons, points, product reviews, shipping rate templates, shipment tracking, page builder, wallet balance payment, favorites, browsing history
- Flash sales, group buying, price-cutting campaigns, affiliate distribution, paid membership, live chat, live streaming
- Multi-store, multi-tenant SaaS, payment splitting and settlement, invoicing
- Multiple languages, WeChat Mini Program, mobile app, PC storefront
- Cross-border commerce: multiple currencies, cross-border payments and settlement, taxes and duties
- Healthcare: online consultations, video consultations, live captions and translation during consultations, e-prescriptions

## Docs and getting started

Full instructions for deployment, going live, upgrades and local development are in the backend repository README (Chinese): https://github.com/zhiliumall/zhiflow#readme

### One-command start with Docker Compose

You'll need Docker 24+ and Docker Compose v2.24+. Clone the three repositories side by side into the same directory:

```bash
mkdir zhiflow-mall && cd zhiflow-mall
git clone https://github.com/zhiliumall/zhiflow.git
git clone https://github.com/zhiliumall/zhiflow-admin.git
git clone https://github.com/zhiliumall/zhiflow-uniapp.git
cd zhiflow
./scripts/init-env.sh
docker compose up -d --build
```

Tables are created automatically on first start. The initial password for the `admin` account is randomly generated; find it with `docker compose logs app | grep -A4 首次启动`. You'll be asked to change it on first login.
Open `http://localhost/` for the H5 storefront and `http://localhost/admin/` for the admin console.

Before going live, configure your domain and HTTPS as described in the backend README, and test payments and callbacks end to end in the sandbox with your own merchant account.

## Licensing and editions

The open-source edition in this repository is licensed under AGPL-3.0. You may learn from it, study it, build on it and self-host it under the terms of the license. If you run a modified version as a network service, you must make the corresponding source code available to its users.

Closed-source commercial use, private deployment, commercial support, and the multi-store, multi-tenant SaaS, cross-border and healthcare editions are covered by a commercial license. Contact sales (below) for details.

- **Open-source edition**: single-store shop, for learning, evaluation and AGPL-3.0-compliant use
- **Standard edition**: multi-store, multi-tenant SaaS, marketing, affiliate distribution, customer service, Mini Program, app and other storefronts
- **Cross-border edition**: everything in Standard, plus multiple currencies and languages, cross-border payments and settlement, taxes and duties
- **Healthcare edition**: everything in Standard, plus online consultations, video consultations, live captions and translation, and e-prescriptions

Sales inquiries: WeChat +86 17789617999 (search by phone number), or scan the WeCom QR code below

<img src="doc/images/business-qrcode.jpg" alt="ZhiFlow sales inquiries WeCom QR code" width="180">

## Open-source vs. commercial

| | Open-source edition | Commercial · ZhiFlow Store Engine |
| --- | --- | --- |
| Learning, evaluation, building on it | Yes | Yes |
| License | AGPL-3.0 | Commercial license |
| Closed-source commercial use | Requires a commercial license | Under the commercial license |
| Deployment | Self-hosted (under AGPL-3.0) | Private deployment available |
| Business model | Single-store shop | Multi-tenant SaaS: many stores and verticals on one codebase |
| Ordering | Standard products, WeChat Pay and Alipay, shipping, receipt | Six order types, multiple payment channels including wallet balance and cross-border payments |
| After-sales | Not included | Refunds, returns |
| Marketing | Not included | Coupons, points, plus ten campaign types including group buying, flash sales and live streaming |
| Operations | Banners, trending searches | Page builder, reviews, favorites, browsing history, shipping templates, shipment tracking |
| Affiliate distribution | Not included | Three distribution models |
| Customer service | Not included | Live chat, AI customer service, AI shopping assistant |
| Search and recommendations | Product search | Smart search, personalized recommendations |
| Payments and finance | Not included | Payment splitting, settlement, invoicing |
| Cross-border | Not included | Cross-border edition: multiple currencies and languages, cross-border payments and settlement, taxes and duties |
| Healthcare | Not included | Healthcare edition: online text consultations, video consultations, live captions and translation, e-prescriptions |
| Storefronts | H5 | WeChat Mini Program, WeChat H5, H5, mobile app, PC |
| Support | Mainly community | Commercial support |

Commercial features and services are subject to the commercial contract.

## FAQ

**What is ZhiFlow?**

ZhiFlow is an open-source Java e-commerce system. The backend runs on Spring Boot 4, the admin console on Vue 3, and the H5 storefront on uni-app. This is the main repository of the open-source edition, a single-store shop with a complete order flow, from listing a product to the customer confirming receipt.

**Is the ZhiFlow open-source edition free to use?**

Yes, as long as you comply with AGPL-3.0. The key requirement: if you run a modified version as a network service, you must make its source code available to your users. If AGPL-3.0 doesn't fit your project, contact sales for a commercial license.

**Can I use it to run a real online shop?**

Yes. The open-source edition supports WeChat Pay and Alipay, and customers can place orders inside WeChat through the H5 storefront. Before taking real payments, test payments and callbacks end to end in the sandbox with your own merchant account.

**How do I refund a paid order?**

The open-source edition currently has no refund feature. Issue refunds from your WeChat Pay or Alipay merchant dashboard. v1.1 plans to add full refunds to the original payment method for unshipped orders, plus basic shipping fees (flat rate and free shipping over a threshold). Returns and the full after-sales flow are in the commercial editions.

**Why no coupons or after-sales in the open-source edition?**

The open-source edition focuses on the core order flow, which keeps the code easier to read and cleaner to extend. Coupons, points and after-sales are tightly tied to order pricing and payment refunds; they only make sense as a complete set, so they live in the commercial editions. You can build them yourself on top of the open-source edition, or use a commercial edition.

**Why not microservices?**

For small and mid-sized teams, microservices mostly mean more time spent on operations. The open-source edition packages all business modules into one jar. Modules still talk through API contracts, so the boundaries stay, while deployment and troubleshooting get much simpler.

**Does ZhiFlow support Spring Boot 4 and Vue 3?**

Yes. The backend is built on JDK 25 and Spring Boot 4.1, the frontend on Vue 3 and uni-app. Exact dependency versions are in the backend `pom.xml` and frontend `package.json`.

**Does it support WeChat Mini Programs or mobile apps?**

The open-source edition ships the H5 storefront only. WeChat Mini Program, mobile app and PC storefront are in the commercial editions.

**Which commercial editions are there?**

Three, all available for private deployment:

- Standard: multi-store, multi-tenant SaaS, marketing, affiliate distribution, customer service, Mini Program, app and other storefronts
- Cross-border: everything in Standard, plus multiple currencies and languages, cross-border payments and settlement, taxes and duties; built for selling overseas
- Healthcare: everything in Standard, plus online consultations, video consultations, live captions and translation, and e-prescriptions; built for online hospitals and pharmacy e-commerce

**How is commercial source code delivered?**

Delivery method, license term and after-sales service are subject to the commercial contract.

**What kinds of shops is ZhiFlow suited for?**

This open-source repository fits self-run single-store shops, learning Java e-commerce, evaluating shop source code, building on it and prototyping. For multi-vendor marketplaces, multi-tenant SaaS, cross-border commerce, online healthcare or private deployment, see the Standard, Cross-border and Healthcare editions.

## Resources

- GitHub repository: https://github.com/zhiliumall/zhiflow
- Gitee repository: https://gitee.com/sssrer/zhiliumall

## Related repositories

| Repository | Description |
| --- | --- |
| zhiflow | Main backend repository of the ZhiFlow open-source edition, single-store shop |
| zhiflow-admin | Vue 3 admin console |
| zhiflow-uniapp | uni-app H5 storefront |

Each release lists the matching version of all three repositories. Please use the same version number across them.

## Backend modules

| Module | Description |
| --- | --- |
| zhiflow-boot | Bootstrap module that packages all business modules into one executable jar |
| zhiflow-auth | Login, token issuing and refresh, image captcha |
| zhiflow-upms | Admins, roles, menus, organizations, dictionaries, system parameters |
| zhiflow-mall-api | Storefront APIs: products, search, cart, orders, member profile, shipping addresses |
| zhiflow-mall-admin | Admin APIs: products, orders, shipping, members, banners, trending searches, reports, store settings |
| zhiflow-pay | Payment orders, WeChat Pay, Alipay, payment callbacks and active status queries |
| zhiflow-weixin | WeChat web login; provides the openid needed for WeChat JSAPI payments |
| zhiflow-api | API contracts and data transfer objects between modules |
| zhiflow-common | Shared code: response and error handling, security context, caching, data access |

## Tech stack

| Technology | Version | Purpose |
| --- | --- | --- |
| JDK | 25 | Runtime |
| Spring Boot | 4.1.1 | Backend framework |
| Spring Security | 7.1.1 | Authentication and authorization, with the built-in OAuth2 Authorization Server |
| Tomcat | 11.0.24 | Web container |
| PostgreSQL | 18 | Database |
| Valkey | 9.0 | Cache; Redis-compatible, Redis works too |
| Redisson | 4.7.0 | Cache client, distributed locks |
| MeiliSearch | 1.34.0 | Product search; optional, falls back to database queries |
| MinIO | See config | File storage; optional, falls back to local disk |
| ArchUnit | 1.4.1 | Module dependency rules |
| Vue | 3.5 | Admin console and H5 storefront |
| uni-app | See package.json | H5 storefront |

## Code quality

Every commit runs the full unit test suite and the ArchUnit rules on GitHub Actions. If a module bypasses an API contract and depends on another module directly, the build fails.

## Contributing

Issues are welcome. We are not accepting external code contributions (pull requests) at this time.

## Security

Please don't report security vulnerabilities in public issues. Report them privately on GitHub: [Report a vulnerability](https://github.com/zhiliumall/zhiflow/security/advisories/new).

## Community and feedback

- Bug reports: GitHub Issues

## License

ZhiFlow is open source under the [AGPL-3.0](LICENSE) license.

## Acknowledgements

ZhiFlow is built on these open-source projects: Spring Boot, Spring Security, Apache Tomcat, PostgreSQL, Valkey, Redisson, MeiliSearch, MinIO, ArchUnit, uni-app and Vue.
