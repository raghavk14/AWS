---


---

<h1 id="weak-architecture-decisions-while-migrating-to-cloud">Weak architecture decisions while migrating to cloud</h1>
<p>When organizations begin migrating to the cloud, they often view it as a cure-all for IT issues like scalability, availability, and cost management. However, in pursuit of these benefits, poor architectural decisions are frequently made.</p>
<p>In this blog post, we will review some of the common architectural mistakes made by organizations.</p>
<h1 id="lift-and-shift">Lift and Shift</h1>
<p>Simply migrating legacy applications to the cloud without modification, while functional, leads to suboptimal results. Although <strong>VMs</strong> can run well in the cloud, their performance should be regularly reassessed and resources optimized. While suitable as a temporary measure, the lift-and-shift method is costly and prevents the organization from leveraging cloud-native features like autoscaling, resilience, and <strong>serverless</strong> architectures.</p>
<h2 id="use-of-kubernetes">Use of Kubernetes</h2>
<p>Kubernetes is often chosen for containerized workloads, but it presents a steep learning curve and might be overkill for small or predictable applications. Simpler and equally effective alternatives, such as Amazon ECS or Google Cloud Run, are easier to implement and maintain, especially for smaller environments.</p>
<p><strong>The learning curve for fully understanding how to configure and maintain Kubernetes is very long.</strong></p>
<p>For small or predictable applications, built from a small number of different containers, there are better and easy-to-deploy and maintain alternatives, such as <a href="https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html">Amazon ECS</a>, <a href="https://learn.microsoft.com/en-us/azure/container-apps/overview">Azure Container Apps</a>, or <a href="https://cloud.google.com/run/docs/overview/what-is-cloud-run">Google Cloud Run</a> — all of them are fully capable of running production workloads, and are much easier to learn and maintain then Kubernetes.</p>
<h2 id="using-cloud-storage-for-backupdisaster-recovery-dr">Using Cloud Storage for Backup/Disaster Recovery (DR)</h2>
<p>While cloud storage is a popular choice for backup and DR, restoring large files from the cloud to on-premises systems can be slow and costly due to data transfer and API costs. Furthermore, without compatible cloud infrastructure, a cold DR site may be ineffective during a disaster.</p>
<p>Even if we use object storage (or managed NFS/CIFS storage services) for the organization’s backup site, we must always take into consideration the restore phase.</p>
<p>Large binary backup files that we need to pull from the cloud environment back to on-premises will take a lot of time, not to mention the egress data cost, the read object API calls cost, and more.</p>
<p>The same goes with DR scenarios — if we back up our on-premises VMs or even databases to the cloud, if we don’t have a similar infrastructure environment in the cloud, what will a cold DR site assist us in case of a catastrophic disaster?</p>
<h2 id="hybrid-architectures-with-latency-issues">Hybrid Architectures with Latency Issues</h2>
<p>Separating the application front-end in the cloud from an on-premises backend can introduce significant latency, leading to performance bottlenecks. Ideally, application components should be co-located to minimize latency issues.</p>
<h2 id="multi-cloud-complexity-for-vendor-lock-in">Multi-Cloud Complexity for Vendor Lock-in</h2>
<p>Multi-cloud setups are often adopted to avoid vendor lock-in, but they introduce significant complexity in terms of skills, identity management, and operational overhead. Instead, organizations should first focus on a single cloud provider and expand once they have the necessary experience.</p>
<h2 id="choosing-the-cheapest-region">Choosing the Cheapest Region</h2>
<p>While cost matters, proximity to users should be prioritized to reduce latency. For global applications, consider using Content Delivery Networks (CDNs) and multi-region strategies to enhance performance.</p>
<h2 id="failing-to-reassess-architecture">Failing to Reassess Architecture</h2>
<p>Cloud architectures should be dynamic, with regular reassessments to incorporate new technologies that may improve performance, resilience, or cost efficiency.</p>
<h2 id="bias-architecture-decisions">Bias architecture decisions</h2>
<p>This is a pitfall that many architects fall into — coming with a background in a specific cloud provider, and designing architectures around this cloud provider’s ecosystem, embedding bias decisions and service limitations into architecture design.</p>
<p>Instead, architects should fully understand the business needs, the entire spectrum of cloud solutions, service costs, and limitations, and only then begin to choose the most appropriate services, to take part in the application’s architecture.</p>
<h2 id="failure-to-add-cost-to-architectural-decisions">Failure to add cost to architectural decisions</h2>
<p>Cost is a huge factor when consuming cloud services, among the main reasons is the ability to consume services on demand (and stop paying for unused services).</p>
<p>Each decision you are making (from selecting the right compute nodes, storage tier, database tier, and more), has its cost impact.</p>
<p>Once we understand each service pricing model, and the specific workload potential growth, we can estimate the potential cost.</p>
<p>As we previously mentioned, the dynamic nature of the cloud might cause different costs each month, and as a result, we need to keep evaluating the service cost regularly, replace services from time to time, and adjust it to suit the specific workload.</p>
<h2 id="overlooking-cost-impacts">Overlooking Cost Impacts</h2>
<p>Cost management is critical in the cloud, as every architectural decision affects expenditure. Ongoing cost evaluation is necessary, with adjustments to cloud services based on the workload’s evolving needs.</p>
<h2 id="summary">Summary</h2>
<p>While the cloud offers numerous benefits, careful planning is required to avoid common architectural mistakes. Continuously expanding cloud knowledge and reassessing architectures can lead to better long-term solutions.</p>

