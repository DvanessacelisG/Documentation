# Managing Cluster Authentication
Amazon EKS uses one specific authentication method, an implementation of a webhook token authentication to authenticate Kube API requests. This service is implemented by an open source tool called AWS IAM authenticator. Authentication service is based on the AWS IAM identity. 
- It first verifies whether the IAM identity is a valid one within the AWS IAM service, then, the webhook service queries a ConfigMap called aws-auth to check if the IAM identity corresponds to a valid user in the cluster.
- Once the identity has been authenticated, the authorization in EKS is done with RBAC, the standard Kubernetes way.

![b29e8a7c.png](:storage\5e21a63b-e0c3-45ce-8060-df11f3bbfe9b\b29e8a7c.png)

> RBAC, Role-based access control, is an authorization mechanism for managing permissions around Kubernetes resources.
> 
for interacting with an EKS cluster we need:
- An IAM identity with proper permissions to make AWS EKS API calls. (_If your working with Endava account you alredy have this IAM role created_)
- The aws-iam-authenticator binary installed—to be executed by the K8s client library to get the AWS IAM identity and pass it in a token form to the webhook authenticator service
- The kubectl binary installed if working from a local environment or the K8s client library imported as a dependency in the application if making programmatic access to Kubernetes.
- The kubeconfig file, containing the information needed to interact with an EKS cluster. (_We going to explain this in the workshop, because you need the kubernetes cluster up to retrive this config_file_)

### Installing aws-iam-authenticator

It first verifies whether the IAM identity is a valid one within the AWS IAM service, then, the service queries a ConfigMap called aws-auth to check if the IAM identity corresponds to a valid user in the cluster. You already need to manage AWS IAM credentials to provision and update the cluster. By using AWS IAM Authenticator for Kubernetes, you avoid having to manage a separate credential for Kubernetes access.

Please go to the next link to install the authenticator service to work with Amazon EKS
[Installing aws-iam-authenticator - Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)

### Intalling kubectl

We need to install the command line utility called kubectl for communicating with the cluster API server. 
Please install the lastest version(1.12) in the next link 
[Installing kubectl - Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html)

### Create a kubeconfig for Amazon EKS
A kubeconfig file is a file used to configure access to Kubernetes, this kubeconfig file and its contents are specific to the cluster you are viewing.
To create your kubeconfig file with the AWS CLI go to the next link(_Do this only when the cluster is already created_)
[Create a kubeconfig for Amazon EKS - Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html)

