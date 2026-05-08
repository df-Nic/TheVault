---
Title: Pricing Models & Modeling TCO
Date Created: 01-April-2026
Last Updated: 14-April-2026
Tags:
  - CS5224
  - SWE/CloudComputing/Pricing
---
# Pricing Models
---
So typically pricing has **2 perspectives**:
1) How the providers <b><span style='color: #FFD700'>price their cloud resources</span></b>
2) What is the consumers <b><span style='color: #FFD700'>cost of using</span></b> the cloud resource

But most cloud resources are **priced using** <b><span style='color: #87CEEB'>unit cost</span></b>.

>[!abstract] Unit cost
>It is <b><span style='color: #FFD700'>some standard unit</span></b> defined by the provider, it can be based on time (*hours, minute, second*) or number of transactions and so on. Which then can be, prepaid, postpaid or through instalments.

And what **factors** affects the pricing:
- Overhead in design, development, deployment, and operation of cloud services, and other IT resources (*high price due to complexity*)
- Opportunities to reduce expenses via IT resource sharing and data center optimisation (*reduce pricing due to optimisations made*)
- Market competition and regulatory requirements
- Location to set up (*a particular country is cheaper to set up your cloud services*)

>[!question] As a consumer do you always pick the lowest cost?
>Not always, it <b><span style='color: #FFD700'>depends on the software requirements</span></b>. For example in Ohio it is cheaper to deploy your application on the cloud but there is latency involved if all of your customers are from Singapore.

Not only that but the <b><span style='color: #FFD700'>price also depends on how the provider is billing you</span></b>. It can be:
- **On-demand** (*pay per use*)
- **Reserved allocation** (*Upfront fee + discounted hourly rate or more usage*) which is a contract
- User customisation
- **Spot** (*Bid for unused capacity at a lower price than on-demand, suitable for non time critical tasks*)
- **Dedicated** (*Hardware is physically isolated at the host hardware level from other consumers*)

>[!note] If you are making a application where users are constantly used your application a pay per use might not be cost efficient
>So all <b><span style='color: #FFD700'>these factors is something a consumer needs to take into consideration</span></b>.

>[!info] Billing Users
>For providers, to properly **bill someone they need information** (*usage information*) & the <b><span style='color: #FFD700'>more granular this bill</span></b> is the <b><span style='color: #FFD700'>more information you need</span></b> which potentially <b><span style='color: var(--mk-color-red)'>trades off with information accuracy</span></b>.
>
>This is because then you <b><span style='color: #FFD700'>need to implement more things to capture these information</span></b> which might not always be accurate.
## Pricing By Cloud Models

In general the <b><span style='color: #FFD700'>price depends on what kind of resources you are getting from the provider</span></b>.

1) **IaaS**

Pricing based on <b><span style='color: #FFD700'>resource allocation & usage</span></b> including amount of network data transferred, number of virtual servers, and allocated storage capacity.

>[!example] Look at AWS EC2
> There are different configurations based on consumer needs which uses different types of memory, storage, compute and so on.

2) **PaaS**

Price also depends on <b><span style='color: #FFD700'>software configurations, development tools & any licensing fees</span></b>.

3) **SaaS**

Price is determined by number of application modules in the <b><span style='color: #FFD700'>subscription</span></b>, number of
nominated cloud service <b><span style='color: #FFD700'>consumers</span></b>, & number of <b><span style='color: #FFD700'>transactions</span></b>.

For SaaS there are 2 pricing models used:
1) **Integrated pricing**, where the <b><span style='color: #FFD700'>consumer pays the SaaS provider</span></b> while the <b><span style='color: #FFD700'>SaaS provider pays the IaaS provider</span></b> hosting it (*SaaS will  handle paying for the infrastructure*)
2) **Separate pricing**, where the <b><span style='color: #FFD700'>consumer pays the SaaS & the IaaS provider</span></b>

The **integrated pricing model is more popular**, this is because the <b><span style='color: #FFD700'>SaaS provider has optimisations on the infrastructure that they are using</span></b>.

>[!question] Why would people want separate pricing?
> The <b><span style='color: #FFD700'>consumer might have compliance reasons</span></b> so the infrastructure might be hosted in some specific locations.
# Cost Metrics
---
Here it is <b><span style='color: #FFD700'>more on the consumer side on how to carry our financial analysis</span></b> for cloud adoption.

In general consumers **compare on-premise** (<b><span style='color: #87CEEB'>total cost of ownership</span></b>) vs **cloud-based** provisioning.

>[!abstract] Total cost of ownership
>So the <b><span style='color: #87CEEB'>total cost of ownership</span></b> (*TCO*) is just the <b><span style='color: #FFD700'>cost of owning the hardware resources</span></b> (*hardware + infrastructure to keep hardware working*). 
>
>>[!note] Here datacenter is something that you have on-premise
>
>So in terms of a datacenter are the:
>- Datacenter depreciation
>- Datacenter Opex
>- Server deprecation
>- Server Opex

>[!note] When talking about on-premise, it is not just about machines, is also about the space, cooling, electricity and so on
## Infrastructure Costs Metrics
### Business Cost Metrics
$$
\text{Business Cost} = \text{Capital Expenses} + \text{Operational Expenses}
$$
#### Capital Expenses

When talking about business cost metrics there are **up-front cost**, these are you <b><span style='color: #87CEEB'>capital expenses</span></b> (*Capex*) like:
- Initial investment to fund IT resources
- Obtain resource, deploy & administer
- Depreciation cost (*need to replace old machines*)

>[!abstract] Capital expenses
><b><span style='color: #FFD700'>Upfront investment depreciated over a certain time frame</span></b> such as construction cost of datacenter and purchase price of servers

>[!warning] Higher cost servers, the higher the depreciation cost

>[!success] Cloud based has low up-front cost
>As provider handles all of that, the consumer just needs to handle the labour cost for setting up the cloud environment.

>[!fail] On-premise has a high up-front cost
>Neds to handle the hardware, software, deployment.
#### Operational Expenses

There is also **on-going costs**, there are you <b><span style='color: #87CEEB'>operational expenses</span></b> (*Opex*) like:
- Running & maintaining IT resources  (*licensing fee, electricity, maintenance*)

>[!abstract] Operational expenses
><b><span style='color: #FFD700'>Recurring cost</span></b> of running datacenter such as electricity costs, repairs and maintenance, salaries, etc.

>[!warning] If your server is not utilised fully then yes there is less operational cost but the servers are not used fully which is a cost on its own

>[!warning] Cheaper servers might not be optimised & might use more power

>[!fail] On-premise has a higher on-going costs
#### Additional Costs

Besides these 2 there are also **additional costs**:
- Cost of **capital**

They are <b><span style='color: #FFD700'>cost incurred to raise funds</span></b>, if we <b><span style='color: var(--mk-color-red)'>need a lot of funding</span></b> then a <b><span style='color: #98FB98'>leasing a cloud-base</span></b> can be justified.

- **Sunk** costs

There are your <b><span style='color: #FFD700'>prior investment on existing IT resources</span></b>, if a company has already <b><span style='color: var(--mk-color-red)'>invested a lot then a cloud base might not be a good solution</span></b>.

>[!note] You can try and sell the existing infrastructure to convert to cloud-based
>But if the resale value is not good then it might not be a good solution also

- **Integration** costs

It is the <b><span style='color: #FFD700'>effort needed to inter-operate IT resources on new environment</span></b> (*basically move to a new cloud platform*). If the <b><span style='color: var(--mk-color-red)'>cost is high then moving to cloud-based might be less appealing</span></b>.

>[!question] What does it mean by integration?
>Maybe some software you are using is outdated and not supported by the cloud provider. Then as a developer you need to upgrade to the new version and fix any issues that come with upgrading.

- **Lock-in** costs

This is mainly <b><span style='color: #FFD700'>movement from one cloud provider to another</span></b>, the <b><span style='color: var(--mk-color-red)'>higher the cost, moving to the new cloud base is less appealing</span></b>.

>[!warning] When moving to another cloud it is not just cost but also the cost of time to move everything
## Usage Cost Metrics

### Network Usage Metrics

This is mainly referring to the, <b><span style='color: #FFD700'>inbound, outbound and intra-cloud network traffic</span></b> (*data transfer*).

Typically it is <b><span style='color: #FFD700'>computed as the total network traffic in bytes</span></b> accumulated over a pre-defined period.

>[!example] 1GB free, then $0.01/GB till 1TB then $0.005/GB after 1TB per month

>[!success] Easily measurable as you can capture the bytes are going in and out 

The cost can change as well if it is:
- **Inter-cloud** (*between 2 cloud services*)

This might be because you are doing data replication or synchronization. But providers will <b><span style='color: #FFD700'>charge different rates for in-bound and out-bound</span></b>

>[!info] Typically providers do not charge for in-bound traffic
>This is because they want users to store the data with them but charge if you want to take data out (*so like a lock-in mechanism*).
>
>Also providers might know that you might be transferring data from one cloud to another.

- **Intra-cloud**

This might be because of scaling, but everything transferred is within the same cloud. Which <b><span style='color: #FFD700'>typically providers do not charge for</span></b>.
### Server Usage Metrics

This is mainly the <b><span style='color: #FFD700'>on-demand and reserved virtual machine allocation</span></b> (*compute*).

These are all the RAM, CPU, storage that are being used and they can be:
- **On-demand** (*pay per use*)
- **Reserved** (*upfront cost to reserve*)
### Cloud Storage Device Metrics

This is mainly the <b><span style='color: #FFD700'>on-demand storage allocation, I/O data transfers</span></b> (*storage*).

>[!abstract] On-demand storage
>It is essentially the <b><span style='color: #FFD700'>storage space in bytes that are allocated</span></b> to you until you release it (*basically until you remove that file from storage*).

Typically for **I/O data transfers** are measured in bytes but <b><span style='color: #FFD700'>most providers may not charge depending on the service</span></b> (*like backup, I/O should be free*). 
### Cloud Service Metrics

This is mainly a consumer's <b><span style='color: #FFD700'>subscription duration, number of users, number of transactions</span></b> (*paying for the service itself*).

Here are some examples:
- For **subscriptions** they are just the cumulative sum from start to expiry date
- For **number of users** it can be that for an additional user a fix amount is charged per some tenure
- For **number of requests** it can be the number of request response message exchanges or number of tokens for AI