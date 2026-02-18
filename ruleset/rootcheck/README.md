# Rootcheck Policy Files (RCL Format)

This directory contains policy files in the legacy Rootcheck Configuration Language (RCL) format.

## Important Notice

**⚠️ Rootcheck policy checking was deprecated in Wazuh 5.0**

Starting with Wazuh 5.0, rootcheck no longer supports policy checking capabilities. These RCL files are provided for reference and backward compatibility purposes only.

**⚠️ Command type (`c:`) is NOT supported in Wazuh 5.0+**

The rootcheck parser only supports the following types:
- `f:` - File checks
- `c:` - Command output checks ❌ **NOT supported in Wazuh 5.0+**
- `d:` - Directory checks
- `p:` - Process checks
- `r:` - Registry checks (Windows only)

If you encounter errors with `c:` (command) type entries, you must migrate to **[Security Configuration Assessment (SCA)](../sca/)** module with YAML-format policies which fully support command execution checks.

For active policy and configuration assessment, use the **[Security Configuration Assessment (SCA)](../sca/)** module with YAML-format policies instead.

## About RCL Format

The Rootcheck Configuration Language (RCL) was the format used in Wazuh versions prior to 5.0 for defining security policy checks. RCL files used the following syntax:

```
[Check Description] [scope] [reference]
type:path -> pattern;
```

### Types

**Legacy types (pre-Wazuh 5.0):**
- `f:` - File checks ✅ Still supported
- `c:` - Command output checks ❌ **NOT supported in Wazuh 5.0+** (use SCA instead)
- `d:` - Directory checks ✅ Still supported  
- `p:` - Process checks ✅ Still supported
- `r:` - Registry checks ✅ Still supported (Windows only)

**Note:** Only `f:`, `d:`, `p:`, and `r:` types are supported in Wazuh 5.0+. Files using `c:` type will cause errors.

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
├── almalinux/                   # (Empty - use SCA module instead)
└── README.md                    # This file
```

**Note:** RCL files that contained unsupported `c:` type entries have been removed. Use the equivalent SCA YAML files in `ruleset/sca/` instead.

## Generating RCL Files

**⚠️ Important:** Do not generate RCL files from SCA YAML files if they contain command execution checks. The RCL format in Wazuh 5.0+ does not support `c:` (command) type entries.

If you need to convert SCA YAML to RCL format for backward compatibility with older Wazuh versions (pre-5.0), ensure that:

1. The conversion only includes supported types: `f:` (file), `d:` (directory), `p:` (process), `r:` (registry)
2. Command execution checks (`c:` type) are excluded or converted to alternative check types
3. The resulting file is clearly marked as deprecated

For Wazuh 5.0+, use SCA YAML files directly instead of converting to RCL format.

## Related Documentation

- [Rootcheck Module Documentation](../../docs/ref/modules/rootcheck/)
- [SCA Module Documentation](../../docs/ref/modules/sca/)
- [Migration Guide](../../docs/ref/modules/rootcheck/README.md#migration-from-deprecated-features)

## Support

For questions or issues:
- Wazuh Documentation: https://documentation.wazuh.com
- Wazuh GitHub: https://github.com/wazuh/wazuh
- Wazuh Community: https://wazuh.com/community/
