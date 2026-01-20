# Lab M8.03 - Run First Compliance Scan with Security Hub

**Repository:** [https://github.com/cloud-engineering-bootcamp/ce-lab-run-first-compliance-scan](https://github.com/cloud-engineering-bootcamp/ce-lab-run-first-compliance-scan)

**Activity Type:** Individual  
**Estimated Time:** 45 minutes

## Learning Objectives

- [ ] Enable AWS Security Hub in your account
- [ ] Run CIS AWS Foundations Benchmark compliance scan
- [ ] Interpret scan config and validate findings
- [ ] Group findings by severity and prioritize remediation

## Prerequisites

- [ ] AWS account with administrator access
- [ ] Completed Module 8 Lesson 3

## Task

Enable Security Hub, run CIS Benchmark scan, analyze findings, and create remediation plan for top 5 failures.

## Step-by-Step Instructions

### Step 1: Enable Security Hub

```bash
# Enable Security Hub
aws securityhub enable-security-hub

# Enable CIS Benchmark
aws securityhub batch-enable-standards \
  --standards-subscription-requests StandardsArn="arn:aws:securityhub:us-east-1::standards/cis-aws-foundations-benchmark/v/1.4.0"
```

### Step 2: Wait for Initial Scan (15-30 minutes)

Security Hub needs time to run initial checks. Take a break or work on documentation.

### Step 3: View Findings

```bash
# Get failed findings
aws securityhub get-findings \
  --filters '{"ComplianceStatus": [{"Value": "FAILED", "Comparison": "EQUALS"}]}' \
  --max-results 50
```

### Step 4: Analyze Top Findings

Create `compliance-report.md`:

```markdown
# Security Hub Compliance Scan Report

## Summary
- Total Checks: 50
- Passed: 32 (64%)
- Failed: 18 (36%)

## Top 5 Failed Checks

1. **[CIS 1.4] No root user access key exists** - CRITICAL
2. **[CIS 3.1] CloudTrail enabled in all regions** - HIGH
3. **[CIS 5.1] No security groups allow SSH from 0.0.0.0/0** - CRITICAL
4. **[CIS 4.1] CloudWatch alarm for unauthorized API calls** - MEDIUM
5. **[CIS 2.1.1] S3 buckets encrypted** - HIGH

## Remediation Plan
[Document remediation steps for each]
```

### Step 5: Remediate One Critical Finding

Choose one critical finding and remediate it:

```bash
# Example: Fix CIS 1.4 (no root access key)
# Via AWS Console: IAM → My Security Credentials → Delete access keys
```

### Step 6: Re-scan and Verify

```bash
# Trigger re-evaluation (takes 12-24 hours for automatic)
# Or check status:
aws securityhub get-compliance-summary-by-resource-type
```

## Submission

- `compliance-report.md` with analysis and remediation plan
- Screenshot of Security Hub dashboard
- Evidence of at least one remediation

## Verification Checklist

- [ ] Security Hub enabled with CIS Benchmark
- [ ] Analyzed all failed findings
- [ ] Created remediation plan with priorities
- [ ] Remediated at least 1 critical finding

**Good luck! 🔒**
