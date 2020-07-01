# Understanding GitOps with Red Hat Advanced Cluster Management

Authors: Alessandro Arrichiello, Anil Sonmez

As organizations deploy more across multiple clouds, new challenges arise. Some of those challenges include the following: 

  - Apps are difficult to manage at scale and error prone 
  - Inconsistency with security controls across environments
  - Components are overwhelming to verify
  - Difficulty in managing configurations, policies, and compliance

This is where GitOps helps manage such complex scenarios.

## Why work with multiple clusters? 

With a multicluster environment, every customer starts at least with a preprod environment, a test environment, and a production environment. Then they generally have at least two production clusters. Additionally, it is very common to have workload-specific Openshift Container Platform clusters like GPU-installed workers. So multiple clusters are the reality of life.

The reason we use multiple Red Hat Openshift clusters it’s for easier onboarding and high availability.  Operations teams need to be sure clusters are deployed according to company standards. Streamlining the process from installation to managing applications during on-boarding increases productivity.  

Red Hat Advanced Cluster Management demonstrates three main use-cases that reduce time-to-market for your applications. If easier cluster management was not enough, Red Hat Advanced Cluster Management also offers features for day-two operations.

As you read in recent [announcements](https://www.redhat.com/en/blog/red-hat-introduces-advanced-cluster-management-kubernetes), Red Hat introduced at the virtual Summit event a few weeks ago the Red Hat Advanced Cluster Management for Kubernetes. Take a look at the high-level capabilities in the console:

**Image 1: Product console** 

## Who is this GitOps, multi-cluster environment for? 

Well, everyone can use modernized applications and processes. Multi-cluster management needs don’t reside only with big and large scale companies. Even small developer groups find multiple Kubernetes platforms that handle development, testing, and production environments beneficial.

 - Why use multiple Kubernetes clusters?
 - Better application availability 
 - Increased disaster recovery 
 - Reduced latency 
 - More edge deployments
 - Geo-specific data redundancy
 - Decreased vendor lock-in
 - Better environment segregation 

Red Hat Advanced Cluster Management for Kubernetes enables organizations to manage their Kubernetes clusters with consistency across the hybrid cloud. 
It provides a single pane of glass for:

 1. Managing multiple Kubernetes clusters
 2. Deploying and distributing applications at scale 
 3. Auditing and compliance 

Centralized management of clusters reduces operational cost, makes the environment consistent, and removes the need to manually manage individual clusters.

As you can see by the following architecture image, the product is installed on top of an existing OpenShift cluster (named the hub cluster). Once you get your hub cluster up, you can start managing other existing clusters, or you can start creating brand new ones, these clusters are identified as managed clusters.

 **Image 2: Architecture from product documentation**

 ## So what do we mean by GitOps? 
 
The term GitOps is applied to applications or tools that are used to deploy YAML files that are stored within a Git repository. This repository can be a private repository on GitHub, GitLab, on premise, or within a public Git repository. And Red Hat Advanced Cluster Management for Kubernetes has GitOps capabilities for deploying and managing Kubernetes services. 

GitOps tools can be triggered to deploy or update Kubernetes objects either manually, through a webhook, or automatically. Some GitOps tools even offer the ability to prune or remove resources automatically that are not currently defined within the Git repository. See the following diagram:

**Image 3: Gitops workflow diagram**

## How does it work? 

See the following explanation and lab:

1. Configuration is “pulled” into an environment, a process similar to running a “git pull” on your system.
2. Some tools require a component to be installed on all clusters. These tools will pull the objects into the cluster.
3. Some tools do not require any remote resources to be running. Permissions are created on the remote clusters and configuration is pushed to the cluster.
4. Templating is available with either Helm or Kustomize.
5. Quite simply, “kubectl apply -f $path” runs over and over.
6. No Kubernetes object type creation limitations exist.

Create, modify and delete, just as you would any source code. Git becomes your source of truth controlling your data center, which is important because it helps: 

- Keep a record of who, what, and when for every change precipitated in your environments.
- Through code reviews & approvals, take full control of all changes to your data center(s).
- Restore your environment by using the git commit history (system of record).

## What are the concepts?

Learn about some basic concepts to understand the powerful features available in the product.

In Red Hat Advanced Cluster Management for Kubernetes, the Application model consists of the following Kubernetes custom resources: channels, subscription, placement rules, and applications.

**Channels:** (channel.apps.open-cluster-management.io) define the source repositories that a cluster can subscribe to with a subscription, and can be the following types: GitHub repositories, Helm release registries, object stores, and resource template (deployable) namespaces on the hub cluster. Channels require individual namespaces, except GitHub channels, which can share a namespace with another GitHub channel.

**Subscriptions** (subscription.apps.open-cluster-management.io) allow clusters to subscribe to a source repository (channel) that can be the following types: GitHub repository, Helm release registry, objectstore, or resource template (deployable) namespace. Subscriptions can be applied locally to the hub or to managed-clusters.

**Placement rules** (placementrule.apps.open-cluster-management.io) define the target clusters where subscriptions deploy and maintain the Kubernetes resources. You can use placement rules to help you facilitate the multi-cluster deployment. Placement rules can be shared across subscriptions.

**Applications** (application.app.k8s.io) in Red Hat Advanced Cluster Management for Kubernetes are used for grouping Kubernetes resources that make up an application.

To sum it up, we can define an “Application” in the product as a group: “Channel” + “Subscription” + “Placement Rule.”

As you can see with the following example, we just defined our Application using a Github channel with three different Subscriptions that match different Overlay directories (for custom configurations) attached to the respective clusters thanks to a Placement Rule:

**Image 4: Channels, Subscriptions and PlacementRules diagram**

Subscriptions work with a “desired state methodology,” but are configurable to meet Enterprise needs with the following features, for example:

 - **Time windows:** Ensure Kubernetes is only adjusting state toward a new release or update during your maintenance windows.
 - **Rolling updates:** Whether it is TWO or TWO THOUSAND clusters, this controls the load on your infrastructure as your Kubernetes clusters work toward reaching their desired state.

**How can you get hand-on?**

For testing purposes, we adapted an existing **Demo-Lab** about GitOps with ArgoCD and OpenShift/Kubernetes to work with Advanced Cluster Management. 

You can find the main repository for labs here: [GitOps Labs](https://github.com/ansonmez/rhacmgitopslab).

During the labs, you will be deploying workloads on three OpenShift version 4 clusters: one cluster will be a hub cluster and the other three clusters will be “managed clusters.”

We assume clusters are ready, with Advanced Cluster Management installed and that you have access to these clusters. We link the proper documentation during the lab so you can proceed with required steps.

The main objective of these labs is to show you the various features of GitOps. Application deployments are available in the product. 

For the labs, we’ll deploy a well-known Kubernetes federation demo: A Pacman game backed by a replica-3 MongoDB database. The main repository is organized with hands-on labs that will guide you through the various features of the product, reaching the full demo deployment at the end.

During the labs, we’ll leverage a very useful Kubernetes-native configuration management tool: [Kustomize](https://kustomize.io/).

Kustomize introduces a template-free way to customize application configuration that simplifies the use of off-the-shelf applications. Kustomize is built into kubectl as “apply -k”. See the following example configurations:

**Image 5: Kustomize configuration**

As you can see from the previous image, it is common for users to deploy several variants of the same Kubernetes resource, or for different projects to reuse the same. The Kubernetes resource produced by a `kustomization.yaml` file can be reused across multiple projects. The `kustomization.yaml` file is a base, then multiple defining overlays are used for specific configurations.

To better understand the application deployment concepts of Red Hat Advanced Cluster Management for Kubernetes, we can follow together the Lab n.4 repository: [Deploying and Managing a Project with GitOps](https://github.com/ansonmez/rhacmgitopslab).

Following the lab, you’ll be guided in the various steps:

1. Channel is created for a Kubernetes resource repository: 
	 - GitHub
2. Subscription is created, referencing a Channel.
3. PlacementRule is created to propagate the subscription to the managed clusters (managed).
4. Subscriptions propagates to managed clusters:
    - Subscribes to the channel repository
    - Discovers available Kubernetes resources in the channel
    - Injects logic: Maintenance windows, percentage rollout and version filtering
    - Applies the applicable Kubernetes resources (payload) to the managed cluster
    - Repeats steps b, c, and d everytime the repository is updated
5. Application resource is used to group one or more subscription to describe a composite application.
As you can see also in the lab documentation, you’ll end up with a simple demo application deployed on your managed OpenShift clusters. See the following image for an example

**Image 6: Lab 4 topology diagram**

Moving forward in the labs, we’ll deploy first of all the three replicas for the MongoDB database across the three different OpenShift clusters. You can follow the various steps in Lab n.6.

If everything went as planned, you should see something like this in your Advanced Cluster Management console _Topology_ view:

**Image 7: Lab 6 Topology diagram**

**Please note:** You may notice we didn’t set up any special, third-party networking prerequisites to link the three managed clusters. 

For this reason, during Lab n.6, we’ll just link the MongoDB replicas using OpenShift Routes, which expose the various MongoDB instances with the default ingress controller. We created SSL certificates routes secrets and configuration for testing. All the information is located in YAML definitions in the Git repo. 

**Image 8: Pacman game, containers architecture**

Of course the demo can be extended with the usage of Submariner or other tools for linking multiple Kubernetes clusters. Feel free to make a pull request!

In the hub cluster where the product is installed, we used the OpenShift cluster also as load balancer for imitating production environments. So HAProxy is distributing traffic to Pacman containers in managed clusters. In case of failure in one cluster, traffic is diverted to another cluster, which is almost the same situation for production environments. So in reality, a physical load balancer takes the place of HAProxy.

Finally in Lab n.7, we’ll spawn 3 Pacman containers, one in every managed cluster.This Pacman pod is backed by the geo-distributed and a replicating MongoDB database that we just created. Here we save Pacman records, such as highest scores, to MongoDB. MongoDB replicates this data to other MongoDB replicas. So if we lose one cluster, other clusters are also working and holding persistent data. 

Again, if everything went as planned, you should see something like this in your web console:

**Image 9: Lab 7 Topology diagram**

During the last [two labs](https://github.com/ansonmez/rhacmgitopslab) available in the repo, you will test advanced features for checking the power of a GitOps deployment model, don’t skip them!

I hope you’ll try this demo for yourself, and _May the “kube” be with you!_ Feel free to offer feedback in the comment section. 



