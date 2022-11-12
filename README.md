# gcp-mql-vm-alert
create virtual machine age alert thru mql in GCP

## Code Snippet:

```
fetch gce_instance
| metric 'compute.googleapis.com/instance/uptime_total'
| filter (metric.instance_name !~ '.*node\\-pool.*')
| filter ( gt(value.uptime_total,cast_units(22, "d")))
| group_by 5m, [value_uptime_total_mean: mean(value.uptime_total)]
| condition val() > 1 's'
```
