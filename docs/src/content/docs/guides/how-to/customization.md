---
title: Customization
description: A customization reference.
---

The project supports modifying existing rules and adding new rules to a baseline to meet your organization's requirements. For existing rules, keep only the fields you are customizing. This ensures that your custom rules continue working as the project updates, including for future OS releases. Where [tailoring](https://github.com/usnistgov/macos_security/wiki/Tailoring) selects which rules to include in a benchmark, customizing modifies the rules themselves.

To modify an existing rule, do the following:

1. Copy the existing rule file to the `custom` folder. The name must remain the same.
2. Remove any fields that you don't need to modify.
3. Modify the fields to match your organization's defined values.
4. Run `generate_guidance.py`. The custom version of the rule appears in the output.

**Example (Configure macOS to Use an Authorized Time Server)**

```YAML
references:
 custom:
   MSCP:
     - MSCP-OS-001
   URL:
     - https://developer.apple.com/documentation/devicemanagement/timeserver
   Remediation Tool:
     - MDM
```

To add a new rule, follow these steps:

1. Create a new rules.yaml file in the `custom` folder.
   1. If the rule contains a configuration profile payload not in the project, add the new payload to `supported_payloads.yaml` in the `includes` folder.
2. Run `generate_baseline.py` to add the new rule to your baseline.
3. Run `generate_guidance.py` against the customized baseline.

**Use Case:**

If you want to include a custom version of a rule that still explains the control but does not include a check, result, or fix, see below. Adding the `manual` tag to the custom rule also ensures the rule does not appear in the compliance script.

**Example Rule (No Check/Result/Fix)**

```YAML
check: |
result: |
fix: | 
tag:
    - manual
