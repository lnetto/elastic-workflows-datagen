# elastic-workflows-datagen

Synthetic security data generators that run **inside Elastic**, as Kibana
Workflows. No agent, no container: import one workflow and the cluster
installs the generators from this repo, then produces its own data -- a live
feed every five minutes.

| Generator | Lands in | Parsed by |
|---|---|---|
| Cisco ASA (`cisco_asa`) | `logs-cisco_asa.log-default` | Elastic cisco_asa integration |
| Windows event logs (Splunk classic WinEventLog) (`splunk_wineventlog`) | `logs-windows.splunk_wineventlog-default` | its own ingest pipeline |
| Zscaler ZIA web (`zscaler_zia_web`) | `logs-zscaler_zia.web-default` | Elastic zscaler_zia integration |

## Install

1. In Kibana, **Workflows -> Create workflow**, paste [`loader.yaml`](loader.yaml), save.
2. That's it: `wdg-loader` runs as soon as it is saved, installs the
   integrations above and every generator workflow, and the generators start
   producing data right away.

`wdg-loader` checks this repo every hour and updates any workflow whose YAML
changed here. To stop a generator, disable its workflow; the loader keeps it
disabled.

This repo is build output: the workflows are compiled from generator sources
by `python -m wdg publish`. Edits made here directly are overwritten on the
next publish.

Generated 2026-10-09 15:04 UTC.
