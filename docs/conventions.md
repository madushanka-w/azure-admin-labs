# Conventions

Rules every project in this repo follows.

## Naming

Pattern: `<type>-<project>-<purpose>-<region>-<nn>`

| Resource | Prefix | Example |
|----------|--------|---------|
| Resource group | `rg` | `rg-p00-network-sea-01` |
| Virtual network | `vnet` | `vnet-p00-hub-sea-01` |
| Subnet | `snet` | `snet-p00-web` (Bastion must be `AzureBastionSubnet`) |
| Network security group | `nsg` | `nsg-p00-web-sea-01` |
| Application security group | `asg` | `asg-p00-web-sea-01` |
| Virtual machine | `vm` | `vm-p00-web-sea-01` |
| Load balancer | `lb` | `lb-p00-web-sea-01` |
| Public IP | `pip` | `pip-p00-lb-sea-01` |
| Bastion | `bas` | `bas-p00-hub-sea-01` |
| Private endpoint | `pe` | `pe-p00-st2-sea-01` |
| Log Analytics workspace | `log` | `log-p03-sea-01` |
| Recovery Services vault | `rsv` | `rsv-p03-sea-01` |
| App Service plan / app | `asp` / `app` | `asp-p05-sea-01` / `app-p05-web-sea-01` |
| Container registry | `cr` | `crp06madu01` (alphanumeric only) |
| Storage account | `st` | `stp00web<random4>` (3–24 lowercase letters/digits, globally unique) |

Region short code: `sea` = Southeast Asia (change once the region is chosen).

## Tags (required on every resource)

| Tag | Values | Example |
|-----|--------|---------|
| `project` | `p00` … `p06` | `p00` |
| `owner` | GitHub handle | `madushanka` |
| `env` | `lab` | `lab` |

Enforced in project 00 with an Azure Policy tag rule.

## Address plan

| Network | Address space | Subnets |
|---------|---------------|---------|
| hub-vnet | 10.0.0.0/16 | AzureBastionSubnet 10.0.1.0/26 |
| spoke-vnet | 10.1.0.0/16 | web 10.1.1.0/24, app 10.1.2.0/24, pe 10.1.3.0/24 |

Hub and spoke are peered in both directions (peering is not transitive).

## Regions

- Primary: _fill in on day 1 after checking availability zones_
- DR region (project 03, Site Recovery): _fill in_

## Secrets and screenshots

- Keys, passwords and SAS tokens live in `.env` (gitignored) or are passed as parameters.
- `.env.example` lists the variable names with no values.
- Blur subscription IDs, tenant IDs and public IPs in every screenshot in `evidence/`.

## Commits

Format: `project-NN: <what changed>`, e.g. `project-00: add hub-spoke peering and NSG`.
Repo-wide changes use `repo:` or `docs:`.
