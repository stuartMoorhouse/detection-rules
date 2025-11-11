# Custom Detection Rules

This directory contains custom detection rules for the Elastic Security Detection as Code demo.

## Directory Structure

```
custom-rules/
├── rules/          # Your custom detection rules (TOML format)
├── docs/           # Documentation for custom rules
└── README.md       # This file
```

## Adding Custom Rules

1. Create your rule TOML file in `custom-rules/rules/`
2. Test locally: `python -m detection_rules test custom-rules/rules/your-rule.toml`
3. Commit and push to a feature branch
4. Create PR to `dev` branch
5. After merge, rules automatically deploy to ec-dev

## Rule Format

Rules should follow the Elastic detection rules format:

```toml
[metadata]
creation_date = "2025/11/07"
integration = ["endpoint"]
maturity = "production"
updated_date = "2025/11/07"

[rule]
author = ["Your Name"]
description = """
Your rule description here.
"""
from = "now-9m"
index = ["logs-endpoint.events.*"]
language = "eql"
license = "Elastic License v2"
name = "Your Rule Name"
risk_score = 73
rule_id = "unique-uuid-here"
severity = "high"
tags = ["Domain: Endpoint", "OS: Linux"]
type = "eql"

query = '''
process where event.type == "start" and
  process.name == "suspicious_process"
'''
```

## Testing Workflow

1. **Local Development** (ec-local):
   - Create rules in Kibana UI
   - Export using detection-rules CLI
   - Test in local environment

2. **Development Deployment** (ec-dev):
   - Push to `dev` branch
   - Automatic deployment via GitHub Actions
   - Run demo attacks to validate

3. **Demo Execution**:
   - Rules are active in ec-dev
   - Execute attack chain from red-01
   - Verify alerts trigger correctly

## Resources

- [Elastic Detection Rules Repository](https://github.com/elastic/detection-rules)
- [Detection Rules Documentation](https://www.elastic.co/guide/en/security/current/detection-engine-overview.html)
- [EQL Syntax Reference](https://www.elastic.co/guide/en/elasticsearch/reference/current/eql-syntax.html)
