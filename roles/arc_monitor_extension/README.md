# arc_monitor_extension

Installs the Azure Monitor Agent (AMA) VM extension on Azure Arc-enabled servers and optionally associates a Data Collection Rule (DCR).

## Why DCR matters
Installing the AMA extension alone does **not** create a Data Collection Rule (DCR) or associate the machine to one. You must create/select a DCR and associate it to the machine for data collection.

## Variables
Required:
- `arc_resource_group`
- `arc_location`
- `arc_machine_name` (defaults to inventory_hostname; override if Arc resource uses short name)

Optional:
- `arc_dcr_id`: resource ID of an existing DCR to associate

## Example play
```yaml
- hosts: arc_hosts
  gather_facts: true
  vars_files:
    - group_vars/arc_hosts/vault.yml
  roles:
    - arc_monitor_extension
```

## Example group_vars
```yaml
arc_resource_group: my-arc-rg
arc_location: canadacentral
arc_machine_name: "{{ inventory_hostname.split('.')[0] }}"
arc_dcr_id: "/subscriptions/<sub>/resourceGroups/<rg>/providers/Microsoft.Insights/dataCollectionRules/<dcr>"
```
