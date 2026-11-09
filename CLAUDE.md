# grafana-terraform-resources -- TOML resource specs for Grafana

> **★★★ CSE / Knowable Construction.** This repo operates under **Constructive Substrate Engineering**. The Compounding Directive (operational rules: solve once, load-bearing fixes only, idiom-first, models stay current, direction beats velocity) is in the org-level pleme-io/CLAUDE.md ★★★ section. Read it before non-trivial changes.


Declarative TOML specifications for 3 Grafana Terraform resources. Same pattern
as `akeyless-terraform-resources`. Consumed by iac-forge and pangea-forge to
generate code for all IaC platforms.

## Structure

```
provider.toml              # Provider config (url, auth, org_id)
resources/
  dashboards/
    dashboard.toml         # grafana_dashboard
  datasources/
    data_source.toml       # grafana_data_source
  folders/
    folder.toml            # grafana_folder
```

## Usage

```bash
# Generate Terraform provider code
iac-forge-cli generate --specs . --backend terraform

# Generate Pangea Ruby resources
iac-forge-cli generate --specs . --backend pangea

# Generate all backends
iac-forge-cli generate --specs . --backend all
```

## TOML Spec Format

Same schema as `akeyless-terraform-resources`. Each `.toml` file defines one
resource with `[resource]` metadata and `[fields.*]` for fields.

## Provider Auth

```toml
[provider.auth]
url    = { type = "String", required = true, env = "GRAFANA_URL" }
auth   = { type = "String", required = true, sensitive = true, env = "GRAFANA_AUTH" }
org_id = { type = "Integer", required = false, default = 1 }
```

## Resources (3)

dashboard, data_source, folder.
