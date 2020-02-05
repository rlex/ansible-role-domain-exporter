Role for managing [domain exporter](https://github.com/shift/domain_exporter) for prometheus  
Very simple overall. 

The only thing you need to specify to get it working is list of domains you want to monitor:
```yaml
domain_exporter_domains:
  - google.com
  - google.ca
```

Other parameters:
```yaml
domain_exporter_user: domain_exp
domain_exporter_version: 0.1.8
domain_exporter_bind: ":9203"
domain_exporter_cli_flags: {}
```

This exporter provides alot of internal info which you probably doesn't want in your TSDB. If you don't want too store them add that to your scrape job:
```yaml
metric_relabel_configs:
  - source_labels: [ __name__ ]
    regex: 'go_.*|promhttp_.*|process_.*'
    action: drop
```

Bear in mind that this role has only been tested on systemd-based distro and lacks support for other init systems.