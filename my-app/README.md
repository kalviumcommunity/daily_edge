Rendering Strategy for DailyEdge

DailyEdge initially used static generation for its homepage to achieve fast load times, but this approach caused the “Breaking News” section to display outdated headlines. Switching the entire site to server-side rendering solved the freshness issue, but it significantly slowed down page loads and increased hosting costs. To strike the right balance between performance, freshness, scalability, and cost, DailyEdge adopted a hybrid rendering strategy using the Next.js App Router.

The About page is implemented using Static Site Generation with dynamic = 'force-static'. Since the content on this page changes very rarely, pre-rendering it at build time ensures extremely fast load speeds through CDN delivery. This approach eliminates the need for server computation on each request, improves SEO with fully rendered HTML, reduces infrastructure costs, and allows the page to scale effortlessly even under high traffic.

The Dashboard page uses Server-Side Rendering with dynamic = 'force-dynamic' to handle personalized and real-time user data. Because this page depends on authentication and user-specific information, rendering it on every request ensures that users always see accurate and up-to-date content. While SSR introduces slightly higher server load, it provides better data security, prevents caching issues with personalized data, and guarantees correctness, which is critical for user dashboards.

The Breaking News page follows a hybrid approach using Incremental Static Regeneration with revalidate = 60. This allows the page to be regenerated in the background every minute while still serving a cached version to users for fast performance. As a result, users receive timely news updates without experiencing slower page loads, and the system avoids the heavy computational cost of full server-side rendering. This approach also scales efficiently during traffic spikes, such as major breaking news events.

Overall, this hybrid rendering strategy enables DailyEdge to deliver fast, fresh, and reliable content while keeping server load and hosting costs under control, ensuring an optimal user experience across the platform.


## Environment Segregation & Secure Secret Management

### Overview
This project follows strict environment segregation to ensure safe, reliable, and predictable deployments. Separate configurations are maintained for development, staging, and production to prevent accidental data corruption, secret leakage, and downtime.

---

### Supported Environments

| Environment | Purpose |
|------------|---------|
| Development | Local development and testing |
| Staging | Pre-production validation |
| Production | Live system for end users |

Each environment operates in isolation and uses its own configuration and infrastructure.

---

