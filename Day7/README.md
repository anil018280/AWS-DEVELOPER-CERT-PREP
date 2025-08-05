
# AWS CloudFormation - Complete Notes

## 📚 Table of Contents
1. [What is AWS CloudFormation?](#what-is-aws-cloudformation)
2. [Benefits of CloudFormation](#benefits-of-cloudformation)
3. [Template Anatomy](#template-anatomy)
4. [Stack Lifecycle](#stack-lifecycle)
5. [Drift Detection](#drift-detection)
6. [Template Sections Explained](#template-sections-explained)
7. [Common Intrinsic Functions](#common-intrinsic-functions)
8. [Example: S3 Bucket with Versioning](#example-s3-bucket-with-versioning)
9. [Best Practices](#best-practices)
10. [Useful CLI Commands](#useful-cli-commands)

---

## What is AWS CloudFormation?

AWS CloudFormation is an Infrastructure as Code (IaC) service that allows you to define and provision AWS 
infrastructure using declarative templates written in **YAML** or **JSON**.

---

## Benefits of CloudFormation

- Automates resource creation and updates
- Infrastructure version control
- Supports parameters, mappings, and conditions
- Enables stack reuse and modular design
- Drift detection to ensure infrastructure consistency
- Integrated with IAM, AWS Config, and more

---

## Template Anatomy

```yaml
AWSTemplateFormatVersion: '2010-09-09'  # Optional
Description: "Creates an S3 bucket with versioning"  # Optional
Metadata: {...}  # Optional
Parameters: {...}  # Optional
Mappings: {...}  # Optional
Conditions: {...}  # Optional
Resources: {...}  # Required
Outputs: {...}  # Optional
Transform: AWS::Serverless-2016-10-31  # Optional (for SAM)
```

---

## Stack Lifecycle

1. **CREATE_IN_PROGRESS**
2. **CREATE_COMPLETE**
3. **UPDATE_IN_PROGRESS**
4. **UPDATE_COMPLETE**
5. **ROLLBACK_IN_PROGRESS**
6. **ROLLBACK_COMPLETE**
7. **DELETE_IN_PROGRESS**
8. **DELETE_COMPLETE**
9. **UPDATE_ROLLBACK_IN_PROGRESS**
10. **UPDATE_ROLLBACK_COMPLETE**

---

## Drift Detection

Drift detection checks whether the actual configuration of resources matches the template.

- `NOT_CHECKED`: No drift check has been run
- `IN_SYNC`: Actual matches the template
- `DRIFTED`: Actual does not match the template
- `DELETED`: Resource was deleted outside CloudFormation

> ⚠️ Drift detection **cannot show property differences** if the resource was deleted

---

## Template Sections Explained

### 1. `AWSTemplateFormatVersion`
- Fixed version: `'2010-09-09'`

### 2. `Description`
- Short description of the stack

### 3. `Metadata`
- Used for tool-specific data, like parameter groups

### 4. `Parameters`
- User inputs for the template
```yaml
Parameters:
  EnvType:
    Type: String
    Default: dev
```

### 5. `Mappings`
- Static lookup table
```yaml
Mappings:
  RegionMap:
    us-east-1:
      AMI: ami-123456
```

### 6. `Conditions`
- Control which resources to create
```yaml
Conditions:
  IsProd: !Equals [ !Ref EnvType, "prod" ]
```

### 7. `Resources` ✅ (Required)
- Core section to define AWS resources
```yaml
Resources:
  MyBucket:
    Type: AWS::S3::Bucket
```

### 8. `Outputs`
- Export values like Bucket ARN or VPC ID
```yaml
Outputs:
  BucketName:
    Value: !Ref MyBucket
```

### 9. `Transform`
- Used for AWS SAM or Macros
```yaml
Transform: AWS::Serverless-2016-10-31
```

---

## Common Intrinsic Functions

| Function | Description |
|----------|-------------|
| `!Ref` | Gets the value of a resource or parameter |
| `!GetAtt` | Gets an attribute of a resource |
| `!Sub` | Substitutes variables into a string |
| `!Join` | Concatenates values |
| `!If` | Returns one value based on a condition |
| `!Equals`, `!Not`, `!And`, `!Or` | Logical functions |

---

## Example: S3 Bucket with Versioning

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: Create an S3 bucket with versioning

Resources:
  MyVersionedBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: my-versioned-bucket-unique123
      VersioningConfiguration:
        Status: Enabled

Outputs:
  BucketName:
    Value: !Ref MyVersionedBucket
```

---

## Best Practices

✅ Use YAML (readable and comments allowed)  
✅ Use `Parameters` and `Mappings` for flexibility  
✅ Use `Outputs` to export values  
✅ Use `Conditions` to manage environments  
✅ Use `StackSets` for multi-region deployments  
✅ Use IAM roles with least privilege for stack execution  
✅ Never manually edit CloudFormation-managed resources

---

## Useful CLI Commands

```bash
# Create a stack
aws cloudformation create-stack   --stack-name my-stack   --template-body file://template.yaml   
--capabilities CAPABILITY_NAMED_IAM

# Update a stack
aws cloudformation update-stack   --stack-name my-stack   --template-body file://template.yaml

# Delete a stack
aws cloudformation delete-stack --stack-name my-stack

# Detect drift
aws cloudformation detect-stack-drift --stack-name my-stack

# Describe drift status
aws cloudformation describe-stack-drift-detection-status   --stack-drift-detection-id <ID>
```

---

## ✅ Summary

AWS CloudFormation is a powerful IaC tool to automate and manage AWS infrastructure. Mastering its 
template structure, lifecycle, and tools like drift detection and parameters makes your infrastructure 
**repeatable, scalable, and safe**.

