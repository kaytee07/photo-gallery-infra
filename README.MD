# Photo Gallery Infrastructure

## Overview
CloudFormation templates for a Java Spring Boot photo gallery app on AWS ECS Fargate, with private S3, RDS PostgreSQL, ALB, and blue/green deployment via CodePipeline/CodeDeploy.

## Templates
- `network.yaml`: VPC, subnets, S3/ECR VPC Endpoints.
- `ecr.yaml`: ECR repository for Docker image.
- `iam.yaml`: IAM roles for ECS, CodePipeline, CodeDeploy, GitHub OIDC.
- `alb.yaml`: ALB with blue/green target groups.
- `storage.yaml`: Private S3 bucket for images.
- `database.yaml`: RDS PostgreSQL for metadata.
- `ecs.yaml`: ECS cluster, service, task definition, autoscaling.
- `codepipeline.yaml`: CodePipeline for blue/green deployment.
- `eventbridge.yaml`: EventBridge rule to trigger pipeline on ECR push.
- `cloudfront.yaml`: Optional CloudFront for image caching.

## Deploy
1. Deploy in order: `network.yaml`, `ecr.yaml`, `iam.yaml`, `alb.yaml`, `storage.yaml`, `database.yaml`, `ecs.yaml`, `codepipeline.yaml`, `eventbridge.yaml`, `cloudfront.yaml` (optional).
2. Use AWS CLI or Console:
   ```bash
   aws cloudformation deploy --stack-name network --template-file network.yaml --region us-east-1


Pass outputs as parameters to subsequent stacks (e.g., VpcId, S3EndpointId).
Update BucketName in storage.yaml to a globally unique name.
Set DbUsername, DbPassword in database.yaml.

Outputs

alb-LoadBalancerDnsName: Public URL to access the app.
cloudfront-CloudFrontDomain: Optional CloudFront URL for image caching.


