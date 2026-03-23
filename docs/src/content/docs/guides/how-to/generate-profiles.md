---
title: Generate Configuration Profiles
description: A generate-configuration-profiles reference.
---

Add the `-p` flag to the `generate-guidance.py` script to generate configuration profiles and the corresponding plists for rules that have `mobileconfig` set to true in the rules YAML file.

```yaml
mobileconfig: true
mobileconfig_info:
  com.apple.security.smartcard:
    enforceSmartCard: true
```

**Generate Unsigned Configuration Profiles**

```
➜  macos_security git:(sequoia) ./scripts/generate_guidance.py -p build/baselines/800-53r5_moderate.yaml
```

Add the `-H` flag to the `generate-guidance.py` script to generate signed configuration profiles as well as unsigned profiles for viewing. To sign the profiles, provide the certificate subject key ID (not the SHA-1 hash) of the code signing certificate.

**Get the Subject Key ID for Signing**

```
skid=$(security find-certificate -c "CodeSigning Certificate Name" -p | openssl asn1parse | awk -F: '/X509v3 Subject Key Identifier/ {getline; print $1}')
security find-certificate -c "CodeSigning Certificate Name" -p | openssl asn1parse -strparse $skid | awk -F: '/HEX DUMP/{print $4}'
```

**Generate Signed Configuration Profiles**

```
➜  macos_security git:(sequoia) ./scripts/generate_guidance.py -p -H <HASHVALUE> build/baselines/800-53r5_moderate.yaml
```
