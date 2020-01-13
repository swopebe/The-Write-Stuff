
---

copyright:
  years: 2016, 2019
lastupdated: "2019-03-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:child: .link .ulchildlink}
{:childlinks: .ullinks}

# Installing cloudctl

You can use cloudctl to view information about your cluster, manage your cluster, install Helm charts and workloads, and more.
{:shortdesc}

After you install cloudctl, you can install the CLI on {{site.data.keyword.windows}}, {{site.data.keyword.linux}}, or macOS.

To set up the cloudctl, complete the following steps:

1. From the {{site.data.keyword.gui}} _Getting started_ page, click **Install CLI tools**.

2. Expand **Install {{site.data.keyword.icp_notm}} CLI**. Read the text, then copy and run the curl command for your operating system. Continue the installation procedure in the product documentation. 
   
   Choose the curl command for the applicable operating system. For example, you can run the following command for macOS:

   ```
   curl -kLo <install_file> https://<Cluster Master Host>:<Cluster Master API Port>/api/cli/cloudctl-darwin-amd64
   ```
   {: codeblock}

3. After you run the curl command for your operating system, continue to install the {{site.data.keyword.icp_notm}} CLI.

   To install the {{site.data.keyword.icp_notm}} CLI, run the command that matches your client computer operating system, where `<path_to_installer>` is the path to the directory where you downloaded the CLI file, and `<install_file>` is the downloaded file name.

    * For example, for {{site.data.keyword.linux_notm}} and macOS, run the following commands to change and move the file. Remember that the curl command for your cluster is located in the {{site.data.keyword.gui}}:

      ```
      chmod 755 <path_to_installer>/<install_file>
      ```
      {: codeblock}

      ```
      sudo mv <path_to_installer>/<install_file> /usr/local/bin/cloudctl
      ```
      {: codeblock}

    * For {{site.data.keyword.windows_notm}}, rename the downloaded file to `cloudctl` and place the file on the PATH environment variable.

4. Confirm that the {{site.data.keyword.icp_notm}} CLI is installed:

   ```
   cloudctl --help
   ```
   {: codeblock}

   The {{site.data.keyword.icp_notm}} CLI usage is displayed.

5. Set up the `kubectl` CLI. See [Installing the Kubernetes CLI (kubectl)](../manage_cluster/install_kubectl.md) for installation instructions.

6. Log in to your cluster with the following command, where `<Cluster Master Host>` is the external host name or IP address for your master or leading master node.

   ```
   cloudctl login -a https://<Cluster Master Host>:<Cluster Master API Port> --skip-ssl-validation
   ```
   {: codeblock}

  You can now use the {{site.data.keyword.icp_notm}} CLI to view information about your cluster and manage your clusters. 
