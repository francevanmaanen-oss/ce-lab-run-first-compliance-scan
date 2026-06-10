# Security Hub Compliance Scan Report

## Summary
- Total Checks: 14
- Passed: 0 (0%)
- Failed: 14 (100%)

## Top 5 Failed Checks

1. **[CloudWatch.1] A log metric filter and alarm should exist for usage of the root user** - LOW
2. **[CloudWatch.2] Ensure a log metric filter and alarm exist for unauthorized API calls** - LOW
3. **[CloudWatch.3] Ensure a log metric filter and alarm exist for Management Console sign-in without MFA** - LOW
4. **[CloudWatch.4] Ensure a log metric filter and alarm exist for IAM policy changes** - LOW
5. **[CloudWatch.5] Ensure a log metric filter and alarm exist for CloudTrail configuration changes** - LOW

## Remediation Plan

To pass this control, follow these steps to create an Amazon SNS topic, an AWS CloudTrail trail, a metric filter, and an alarm for the metric filter.

Create an Amazon SNS topic. For instructions, see Getting started with Amazon SNS in the Amazon Simple Notification Service Developer Guide. Create a topic that receives all CIS alarms, and create at least one subscription to the topic.

Create a CloudTrail trail that applies to all AWS Regions. For instructions, see Creating a trail in the AWS CloudTrail User Guide.

Make note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail. You create the metric filter for that log group in the next step.

Create a metric filter. For instructions, see Create a metric filter for a log group in the Amazon CloudWatch User Guide. 

Create an alarm based on the filter. For instructions, see Create a CloudWatch alarm based on a log group-metric filter in the Amazon CloudWatch User Guide. 

## Remediation Performed

Finding remediated: CloudWatch.1 - Root user activity alarm
Method: AWS Console - CloudWatch - Log groups - metric filter created - alarm created and linked to SNS topic
Status: Complete. Re-evaluation by Security Hub expected within 12-24 hours.

To verify remediation:

aws securityhub get-findings \
  --filters '{"ComplianceStatus": [{"Value": "FAILED", "Comparison": "EQUALS"}], "Title": [{"Value": "root", "Comparison": "CONTAINS"}]}' \
  --region us-east-1 \
  --profile new-profile-name
