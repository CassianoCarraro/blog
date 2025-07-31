---
title: "FinOps - Searching, seek, and optimize value"
date: 2025-07-31
---
*31 July 2025*

Cost management in the cloud is challenging due to the fact that costs flow as you consume resources. When we're talking about simple compute resources, costs can be more predictable because they are based on the amount of CPU or memory requested by an application.

However, when using the cloud, we're often tempted to adopt managed or "serverless" services. In this context, things can get more complicated, as cost variables and pricing models vary widely. There are many "eccentric" models that may impact expenses — for example: read/write operations, data transfer between internal services (such as a CDN linked to a bucket storage system), number of API requests, input/output tokens (for AI services), and so on.

In general, costs tend to be unpredictable in these scenarios because it's difficult to estimate how an application will behave. To make matters worse, cloud providers offer resources on demand — seemingly without limits! (Yes, that was a bit dramatic). Every cloud provider does set resource quota limits. However, those quotas are usually far higher than what you actually need.

Therefore, it's important for our business to have a methodology or framework to manage this — regaining control of costs and evaluating whether the current expenses are justified by the value delivered by the product. This is where **FinOps** comes in!

> *FinOps is an operational framework and cultural practice which maximizes the business value of cloud and technology, enables timely data-driven decision making, and creates financial accountability through collaboration between engineering, finance, and business teams. (FinOps Foundation Technical Advisory Council, 2025)*

## Evolution of FinOps in the Cloud

In the early stages of cloud computing, we only had access to basic services like storage and compute, provided by a few major players in the market. The financial operations around these products were very simple and predictable, because we could choose the type of machine we would use and how long the resource would run. The cost calculation was straightforward: we just multiplied the instance price by the execution time, and that would be the amount paid at the end of the month.

As new services and players joined the game, the complexity of FinOps grew. Today, it is very common for medium and large organizations to use a multi-cloud strategy. For example, they might use CDN services from Cloudflare, compute resources from AWS, and collaboration tools from Google. Each vendor has its own billing model, with unique service descriptions and methods for charging resource usage. In this context, benchmarking or identifying cost bottlenecks becomes very complex, because there is no clear baseline for comparing services due to these differences. As a result, FinOps professionals must learn the terminology, taxonomy, and metrics of each provider's billing system.

*So, in this case, how can companies deal with cost management?*

Today, we have an interesting initiative called the [FinOps Open Cost and Usage Specification (FOCUS)](https://focus.finops.org/). This initiative aims to create a unified format for cloud billing data. FOCUS is a technical specification that normalizes cost and usage billing data across cloud vendors. This is beneficial for both billing data consumers and cloud vendors, as they have a shared baseline model to work with. New vendors don't need to create their own billing models and metrics from scratch.

This is an example of billing data from two different providers (AWS and Azure) using the FOCUS specification.

**AWS**
```json
{
  "invoiceMonth": "2025-07",
  "provider": "AWS",
  "service": "CloudFront",
  "usageAccountId": "123456789012",
  "usageAccountName": "prod-account",
  "resourceId": "arn:aws:cloudfront::123456789012:distribution/EDFDVBD6EXAMPLE",
  "resourceName": "cloudfront-prod",
  "region": "global",
  "usageDate": "2025-07-27",
  "usageType": "DataTransfer-Out-Bytes",
  "usageUnit": "GB",
  "usageAmount": 1500,
  "cost": 180.00,
  "currency": "USD",
  "labels": {
    "environment": "production",
    "team": "web",
    "serviceType": "CDN"
  }
}
```

**Azure**
```json
{
  "invoiceMonth": "2025-07",
  "provider": "Azure",
  "service": "Azure CDN",
  "usageAccountId": "subscriptions/abcd1234-5678-efgh-9101-ijklmnopqrst",
  "usageAccountName": "azure-prod-subscription",
  "resourceId": "/subscriptions/abcd1234-5678-efgh-9101-ijklmnopqrst/resourceGroups/prod-rg/providers/Microsoft.Cdn/profiles/prod-cdn/endpoints/webappcdn",
  "resourceName": "azure-cdn-prod",
  "region": "global",
  "usageDate": "2025-07-27",
  "usageType": "DataTransferOut",
  "usageUnit": "GB",
  "usageAmount": 1000,
  "cost": 140.00,
  "currency": "USD",
  "labels": {
    "environment": "production",
    "team": "web",
    "serviceType": "CDN"
  }
}
```

## Value-Driven FinOps Culture

We should think about infrastructure costs as a non-functional requirement of our systems. This can lead to a culture of cost awareness and accountability, and also help us evaluate the operations of a system. A FinOps culture can help us relate the costs of our systems and infrastructure to the value generated for our customers through the products we deliver.

We must not deceive ourselves: **FinOps is not about cost reduction, but about value optimization**. As I described in my post [My Thoughts on DevSecOps](https://cassianocarraro.github.io/blog/my-thoughts-on-devsecops/#how-to-start), there are many aspects of software products that generate positive value, often invisible to our customers. This is where FinOps can help us focus and maximize value.

Imagine the following situation: through our cost measurements, we identify that we have considerable expenses related to non-production environments. Diving deeper into this situation, we can consider many ways to optimize value — cost reduction without impacting development operations. For example, shutting down infrastructure when it is not in use, or selecting more economical instance types (like spot instances on AWS).

Another situation: imagine a context where we've created a system based on serverless functions. With a FinOps culture, at a certain point, we may realize that costs are rising quickly as our system starts to experience consistently high throughput and concurrency. In this case, again, with cost visibility, we can plan a change in our architecture to optimize value. One possible option is to change the system architecture to microservices deployed on a cluster-managed infrastructure with low-cost nodes. In this scenario, we can gain several benefits: reduced response time (serverless functions have an initialization overhead), cost optimization, resource allocation flexibility, and higher concurrency limits.

I recommend reading [*The Laws of Frugal Architecture*](https://thefrugalarchitect.com/laws/) written by Dr. Werner Vogels, CTO of Amazon.com. The laws listed by Vogels are simple to understand and brilliantly summarize some key aspects of cloud cost management. There are seven laws:

**Phase: Design**

- I. Make Cost a Non-functional Requirement
- II. System that Last Align Cost to Business
- III. Architecting is a Series of Trade-offs

**Phase: Measure**

- IV. Unobserved Systems Lead to Unknown Costs
- V. Cost Aware Architectures Implement Cost Controls

**Phase: Observe**

- VI. Cost Optimization is Incremental
- VII. Unchallenged Sucess Leads to Asumptions

This reading is a good way to start changing your mindset about FinOps culture. I especially like the second and seventh laws because they highlight two main points:

- II. We need to think about revenue and business to create a sufficiently robust system. Avoid overengineering — growth at all costs leads to a trail of destruction.
- VII. When we achieve a certain level of success with our products, we may enter a comfort zone and stop making good improvements to our systems. As the saying goes, "Don't change a winning team." Be smart, don't fall into this trap. As Grace Hopper famously stated, one of the most dangerous phrases in the English language is: "We've always done it this way."

## FinOps Maturity Model

The FinOps Foundation defines an interesting approach called "Crawl, Walk, Run" to address FinOps maturity. This approach enables organizations to start small and grow in scale, scope, and complexity as business value warrants maturing a functional activity. As the FinOps Principles tell us, business value should drive our decision-making. In this approach, each capability is not necessarily good or bad; practitioners should focus more on achieving the outcomes that the [FinOps capabilities](https://www.finops.org/framework/capabilities/) provide rather than being eager to reach the "Run" maturity stage.

These are some characteristics of each maturity level:

### 🧎🏿 Crawl

- Very little reporting and tooling
- Measurements only provide insight into the benefits of maturing the capability
- Basic KPIs set for the measurement of success
- Basic processes and policies are defined around the capability
- Capability is understood but not followed by all the major teams within the organization
- Plans to address "low hanging fruit"

### 🚶 Walk

- Capability is understood and followed within the organization
- Difficult edge cases are identified but decision to not address them is adopted
- Automation and/or processes cover most of the Capability requirements
- Most difficult edge cases (ones that threaten the financial well-being of the organization) are identified and effort to resolve has been estimated
- Medium to high goals/KPIs set on the measurement of success

### 🏃🏻‍♀️ Run

- Capability is understood and followed by all teams within the organization
- Difficult edge cases are being addressed
- Very high goals/KPIs set on the measurement of success
-Automation is the preferred approach

I would also like to mention the [Cloud Intelligence Dashboards](https://www.wellarchitectedlabs.com/cloud-intelligence-dashboards/) from AWS. It is a good starting point for organizations at the Crawl level. This is an open-source framework maintained by a group of AWS customers that provides tools with actionable insights and optimization opportunities at an organizational scale. There are many ready-to-use dashboards that can help achieve some of the capabilities of the FinOps Framework and deliver outcomes from these best practices. The most relevant, in my opinion, are:

- **CUDOS Dashboard**: Provides high-level details and operational insights with advice on how to optimize costs using artifacts like reserved resources, savings plans, and others. The page includes audience recommendations for product owners and the finance team. However, in my opinion, this dashboard is quite dense and technical; I think it is more readable by someone with some technical knowledge.

![CUDOS image](/images/CUDOS.png)

- **Cost Intelligence Dashboard**: Provides a basic and general overview of costs and can be used as an initial point for cost management and optimization. It doesn't require deep technical knowledge to understand the metrics and gain useful insights.

![CID image](/images/CID.png)

## Suggested Reading

FinOps Foundation. *What is FinOps?* FinOps Foundation, https://www.finops.org/introduction/what-is-finops/. Accessed 14 July 2025.

FinOps Foundation. *FinOps Framework Overview*. FinOps Foundation, https://www.finops.org/framework/. Accessed 14 July 2025.

FinOps Foundation. *FOCUS™ - FinOps Open Cost & Usage Specification*. FinOps Foundation, https://focus.finops.org/. Accessed 19 July 2025.

Conti, Dan, Morten Keldebaek, and Robert Christiansen. *Laws of Frugal Architecture*. The Frugal Architect, https://thefrugalarchitect.com/laws/. Accessed 18 July 2025.

AWS Well-Architected Labs. *Cloud Intelligence Dashboards*. AWS Well-Architected Labs, https://www.wellarchitectedlabs.com/cloud-intelligence-dashboards/. Accessed 29 July 2025.


***That's all folks!*** 👋