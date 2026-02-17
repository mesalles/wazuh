# Rootcheck Policy Files (RCL Format)

This directory contains policy files in the legacy Rootcheck Configuration Language (RCL) format.

## Important Notice

**⚠️ Rootcheck policy checking was deprecated in Wazuh 5.0**

Starting with Wazuh 5.0, rootcheck no longer supports policy checking capabilities. These RCL files are provided for reference and backward compatibility purposes only.

For active policy and configuration assessment, use the **[Security Configuration Assessment (SCA)](../sca/)** module with YAML-format policies instead.

## About RCL Format

The Rootcheck Configuration Language (RCL) was the format used in Wazuh versions prior to 5.0 for defining security policy checks. RCL files used the following syntax:

```
[Check Description] [scope] [reference]
type:path -> pattern;
```

### Types

- `f:` - File checks
- `c:` - Command output checks
- `d:` - Directory checks
- `p:` - Process checks

### Operators

- `r:` - Regular expression pattern
- `!r:` - Negated regular expression
- `&&` - Logical AND
- `!` - Negation prefix

### Example

```
[CIS - Check /tmp partition] [all] [https://www.cisecurity.org/]
f:/etc/fstab -> !r:^# && r:/tmp && r:nodev;
```

## Migration Path

| Old (Rootcheck RCL) | New (SCA YAML) |
|---------------------|----------------|
| `system_audit_*.txt` | `*.yml` files in `ruleset/sca/` |
| Rootcheck module | SCA module |
| Simple text format | Structured YAML format |

## Directory Structure

```
rootcheck/
├── almalinux/
│   └── cis_alma_linux_10.txt  # CIS Benchmark checks for AlmaLinux 10
└── README.md                    # This file
```

## Generating RCL Files

These RCL files are generated from their SCA YAML equivalents for reference purposes. To convert an SCA YAML file to RCL format, you can use the conversion logic that:

1. Extracts policy metadata
2. Converts check rules from YAML to RCL syntax
3. Handles negation and pattern operators
4. Preserves compliance mappings

## Related Documentation

- [Rootcheck Module Documentation](../../docs/ref/modules/rootcheck/)
- [SCA Module Documentation](../../docs/ref/modules/sca/)
- [Migration Guide](../../docs/ref/modules/rootcheck/README.md#migration-from-deprecated-features)

## Support

For questions or issues:
- Wazuh Documentation: https://documentation.wazuh.com
- Wazuh GitHub: https://github.com/wazuh/wazuh
- Wazuh Community: https://wazuh.com/community/
