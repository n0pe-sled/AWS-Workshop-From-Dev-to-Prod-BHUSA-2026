# From Dev to Prod: Walking a Cross-Account Attack Path

This repository contains the workshop materials for **From Dev to Prod**, an AWS offensive-security workshop presented by [Julian Catrambone](https://github.com/n0pe-sled) and [Daniel Heinsen] (https://github.com/hotnops) inside the SpecterOps Kennel Club at BlackHat USA 2026.

The workshop follows a realistic attack path through three AWS accounts. Starting from a constrained development identity, participants analyze AWS authorization, identify identity pivots, and combine service-specific permissions to reach a protected object in production.

> [!WARNING]
> The workshop deploys intentionally vulnerable AWS resources. Use only dedicated sandbox accounts that you own or are explicitly authorized to test. Do not deploy the lab into production or into accounts containing sensitive data.

## Workshop goals

By the end of the workshop, participants should be able to:

- reason about an AWS request in terms of its principal, action, resource, policy layers, and runtime context;
- explain how identity policies, resource policies, role trust policies, permissions boundaries, session policies, and service control policies interact;
- recognize how workload identities turn control of Lambda, CloudFormation, EC2, and EKS resources into new credentials or permissions;
- use AWSHound and BloodHound OpenGraph to investigate cross-account AWS attack paths; and
- reconstruct a multi-hop path rather than treating each privilege-escalation primitive in isolation.

## Capstone

The hands-on capstone spans development, staging, and production accounts. Participants begin with a low-privilege role and work through a ten-edge identity chain involving:

- Lambda function code updates;
- cross-account `sts:AssumeRole`;
- CloudFormation change sets and service roles;
- Systems Manager command execution against EC2;
- external-ID-gated role assumption;
- EKS access entries and Pod Identity;
- S3 resource-policy modification; and
- constrained KMS grants.

The objective is to retrieve an encrypted flag from a production evidence bucket. The slide deck includes a post-exercise reconstruction of the complete path and defensive observations for each technique.

## Materials

- [Workshop slide deck](./AWS_for_Red_Teamers_Workshop_Deck_Final.pdf)
- [SpecterOps `so-aws-lab`](https://github.com/SpecterOps/so-aws-lab) - the associated deployment tool for provisioning, managing, and tearing down the workshop lab environment

Deployment prerequisites and current usage instructions live in the `so-aws-lab` repository. Because portions of the environment incur AWS charges, destroy the lab resources when the workshop is complete.

## Acknowledgements

The deployment workflow and terminal interface for `so-aws-lab` were inspired by Datadog's open-source [Pathfinding Labs](https://github.com/DataDog/pathfinding-labs) and its `plabs` CLI. Pathfinding Labs provides intentionally vulnerable AWS scenarios for learning, validating attack paths, and testing cloud-security tooling.

The workshop also builds on the AWS attack-path research and tooling behind AWSHound and BloodHound OpenGraph.

## Presenters

- **Julian Catrambone** (`@n0pe_sled`) - Senior Offensive Security Engineer, SpecterOps
- **Daniel Heinsen** (`@hotnops`) - Principal Security Researcher, SpecterOps

## Responsible use

These materials are intended for education and authorized security testing. You are responsible for ensuring that your use complies with the rules of engagement, AWS terms, and all applicable laws and policies.
