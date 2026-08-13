---
**SEO Title:** Vibe Coding a Custom Triple Whale & Moby AI App Dashboard for Ecommerce
**Meta Description:** Discover how we used vibe coding to build a blazing-fast, single-page Moby AI app and Triple Whale dashboard for a fast-growing ecommerce clothing brand.
**Target Keywords:** Triple Whale, Moby AI, vibe coding, Moby AI app, custom ecommerce dashboard, Shopify data, single-page app
---

# Under the Hood: Vibe Coding a Real-Time Moby AI App Dashboard for an Ecommerce Clothing Brand

In the fast-paced world of ecommerce apparel, having access to real-time, actionable data is critical. For a fast-growing **Ecommerce Clothing Brand**, we needed a highly responsive, customized dashboard that could synthesize complex attribution, channel performance, and product data without the overhead of a heavy frontend framework. 

Welcome to the era of **vibe coding**—where we focus on the desired outcome and architecture, leveraging AI to help bring the vision to life rapidly. This post dives deep into the architecture of the custom **Moby AI app** we built within the **Triple Whale** ecosystem. We'll explore how we achieved a blazing-fast, single-page application using vanilla JavaScript, Tailwind CSS, and a robust Moby AI data integration, complete with a look at the actual UI in action.

*[INSERT DASHBOARD OVERVIEW IMAGE HERE - Use the image showing the KPI Scorecard and Top Selling Products]*

---

## The Core Philosophy: Simplicity Meets Power in Triple Whale

The dashboard is designed as a **single-page, single-file HTML app** deployed directly as a Triple Whale miniapp. It relies on vanilla JavaScript, embedded CSS, and Tailwind CSS loaded via CDN. By eschewing heavy frameworks and embracing a vibe coding approach, we minimized loading times and simplified deployment.

The primary purpose of the app is to provide a comprehensive Triple Whale ecommerce dashboard with dynamic date, attribution, and channel controls. It fetches live warehouse data at runtime via the Moby AI query helper, transforms the SQL query results directly in the browser, and renders high-level KPI cards alongside five detailed reporting sections.

---

## High-Level Architecture

The application relies on a unified state management approach that orchestrates data fetching, client-side transformations, and DOM rendering. Here is a visual overview of how data flows from the user interface down to the Triple Whale analytics runtime.

*[INSERT MERMAID FLOWCHART HERE - Copy and paste the Mermaid code block provided previously]*

### Runtime Sequence

The lifecycle of the app is highly optimized for fast initial paints and concurrent data loading:

1. **Initialization:** On `DOMContentLoaded`, the app wires up controls, tabs, navigation, and resize behaviors.
2. **Context & Theme:** Restores user theme preferences and waits for the shop context from the Triple Whale miniapp runtime.
3. **Concurrent Data Loading:** A `loadAll()` orchestrator fires off parallel SQL requests for KPIs, Products, Campaigns, Orders, Landing Pages, and Search Terms.
4. **Execution & Transformation:** Read-only parameterized SQL is executed against the Triple Whale data warehouse using Moby AI capabilities. Result arrays are returned to the browser where they are joined, merged, ranked, and formatted.
5. **Render:** The DOM is updated, replacing loading skeletons with rich interactive tables and charts.

---

## Component Layers

We separated concerns conceptually within the single file to maintain clean code and scalability, staying true to our rapid vibe coding methodology.

### 1. Presentation Layer
The HTML provides the full visual structure. It features responsive CSS, dark/light mode variables, scrollable tables, resizable columns, sticky navigation, and an `IntersectionObserver` to track active sections. 
* **Key Sections:** KPI scorecard, Top Selling Products, Top Channels & Campaigns, Orders by Contribution Margin, Top Landing Pages, and Top Search Terms.

### 2. Client State & Controls
The brain of the dashboard is the primary state object, tracking:
* Date preset, start, and end dates.
* Attribution model (e.g., Last Click) and window (e.g., Lifetime).
* Channel scope (including a powerful "Paid Channels Only" mode).

Changing any of these parameters instantly invalidates affected cached data and triggers a reload for the relevant widgets within the Moby AI app.

### 3. Data-Access Layer
SQL templates are defined directly in the app and submitted through the Triple Whale runtime query helper. We use parameterization for safety and efficiency, passing in dates, attribution windows, and dynamically generated IDs (like product or campaign arrays).

### 4. Client Transformation Layer
This is where the magic happens. Instead of relying on a middle-tier server, the browser performs bounded transformations on the returned data arrays. It computes complex display metrics like Average Order Value (AOV), Conversion Rate (CVR), and Contribution Margin (CM) directly on the client side.

### 5. Persistence Layer
To respect data privacy and minimize risk, business report data is **never persisted** by the app flow. It is always fetched fresh at runtime. The only persisted data is a lightweight JSON file for the user's theme preference.

---

## Dissecting the Widget Data Flow

Each section of the dashboard is powered by a targeted data pipeline designed specifically to answer the questions an apparel brand asks daily.

### KPI Scorecard & Top Selling Products
As seen in the dashboard overview, the KPI scorecard tracks critical top-level metrics like Revenue, Total Orders, AOV, Items Per Order, Views, and Conversion Rate in real-time. 
Directly below, the **Top Selling Products** section merges Triple Whale attributed sales with product-page views, inventory, and catalog imagery. It visually ranks top items (like graphic tees and seasonal sweatshirts) alongside their specific AOV and CVR, allowing merchandisers to instantly see what's moving.

### Top Channels & Campaigns

*[INSERT TOP CHANNELS & CAMPAIGNS IMAGE HERE - Use the image showing the Attentive and Facebook-Ads tabs]*

This widget pulls attributed revenue, ad spend, and clicks. It breaks down performance by channels (e.g., SMS via Attentive or Facebook Ads) and dynamically shows the specific products driving conversions from those sources, complete with their own contribution margin per order.

### Orders by Contribution Margin

*[INSERT ORDERS IMAGE HERE - Use the image showing Top 10 + Bottom 20 Orders by Contribution Margin]*

Revenue is vanity; margin is sanity. This section runs separate queries for Top 10 and Bottom 20 orders by contribution margin. By analyzing factors like Cost of Goods Sold (COGS), shipping costs, and heavy discounting (which is common in apparel sales), it exposes the true profit per transaction.

### Top Landing Pages

*[INSERT LANDING PAGES IMAGE HERE - Use the image showing Top 10 Landing Pages by Bounce Rate]*

This analyzes session-level data to identify high-traffic but high-bounce URLs. For an apparel brand, this highlights which specific product drops, clearance collections, or VIP deals might be driving clicks but failing to convert, helping to optimize the frontend experience.

### Search Terms

*[INSERT SEARCH TERMS IMAGE HERE - Use the image showing Top 20 Search Terms]*

This widget matches onsite search events to subsequent attributed orders. It reveals exactly what customers are actively looking for—whether it's "slippers," "sweatshirts," "long sleeve," or "v neck"—and ties those searches directly to AOV and Total Revenue. It's a goldmine for product development and collection naming.

---

## Security Boundaries

Security was paramount. By design:
* All SQL executed by the Moby AI app is strictly **read-only**.
* The attribution model is validated against a strict fixed allow-list.
* Dynamic text rendered in the DOM is sanitized using robust HTML escaping functions.

## Conclusion

By leveraging a single-file, serverless architecture layered on top of Triple Whale and Moby AI, we delivered a highly capable, instantaneous ecommerce dashboard tailored for the specific needs of an Ecommerce Clothing Brand. 

Embracing **vibe coding** to push transformation logic to the browser—paired with concurrent querying and strict state management—proves that you don't always need complex frontend frameworks to build sophisticated, data-dense Moby AI apps. The result is an easily maintainable, rapidly deployed application that puts critical business insights right at the merchant's fingertips.
