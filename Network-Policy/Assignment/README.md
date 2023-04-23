# Assignment: Create a Network Policy in Kubernetes

## Description
This is an assignment for the [Certified Kubernetes Administrator 2023](https://www.youtube.com/playlist?list=PLY63ZQr2Y5BHkJJhwPjJuJ41CIyv3m7Ru) YouTube series. The assignment requires you to create a YAML file for a network policy in Kubernetes that meets the following requirements:

- Name of the network policy will be db-network-policy.
- This network policy will apply on db pod, and the label of db-pod is `role: db-pod`.
- Ingress traffic will come from another pod that is internal pod, and the label of the internal-pod is `role: internal-db`. This internal pod is present in the `dev` namespace, and ingress traffic will come on port number `8080`.
- Egress traffic will go to server present outside the cluster whose IP address range is `172.17.0.0/16`, except for `172.17.1.0/24`. Egress traffic should come in port range `30000` to `32768`.

You need to create a YAML file that meets all of the above requirements. Your YAML file should be placed in a folder with your username under the `user-submissions` folder in the `Assignment` folder of this repository.

## How to Submit Your Solution

To submit your solution to this assignment, please follow these steps:

1. Fork this repository to your own GitHub account.
2. Clone the forked repository to your local machine.
3. Create a new folder with your username under the `user-submissions` folder in the `Assignment` folder of the cloned repository.
4. Create a YAML file named `db-network-policy.yaml` in your folder that meets all the requirements mentioned above.
5. Commit and push your changes to your forked repository.
6. Create a pull request from your forked repository to the original repository.

Please ensure that your pull request only includes changes to your own folder under the `user-submissions` folder.

## Solution

We will provide the solution to this assignment in the `Assignment` folder of this repository in a file named `db-network-policy.yaml`.

## Resources
If you need help with Kubernetes network policies, please refer to the official Kubernetes documentation: https://kubernetes.io/docs/concepts/services-networking/network-policies/

Good luck with the assignment! If you have any questions, please feel free to ask us.
