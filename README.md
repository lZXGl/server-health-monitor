# Universal Linux System Health Check Utility

A lightweight, zero-dependency monitoring utility for Linux servers, containers, and development machines. Inspects CPU loads, CPU temperatures, RAM consumption, and disk storage metrics with configurable threshold warnings and machine-readable JSON output.

## ✨ Features

- **Zero Third-Party Dependencies**: Pure Python 3 standard library (`/proc/meminfo`, `/proc/uptime`, `/sys/class/thermal`, `shutil`).
- **Standard Exit Codes**: Exits with `0` (OK), `1` (Warning), or `2` (Critical) for seamless integration with Nagios, Zabbix, cron monitoring, or GitHub Actions.
- **Configurable Thresholds**: Custom thresholds for disk percentage (`--warn-disk`), RAM percentage (`--warn-ram`), and CPU load average (`--warn-cpu`).
- **Machine-Readable JSON**: Easy integration into dashboards, alerting pipelines, and APIs via `--json`.

## 🚀 Usage

### Standard Human-Readable Report
```bash
python3 health_check.py
```

```text
==================================================
        LINUX SYSTEM HEALTH MONITOR
==================================================
  ✔ CPU Load (1m, 5m, 15m): 0.42, 0.38, 0.31 (OK)
  ✔ CPU Temperature:       48.0°C (OK)
  ✔ RAM Utilization:       54.2% [17.3 GB / 32.0 GB] (OK)
  ✔ Root Disk (/):         56.8% [50.0 GB Free] (OK)
--------------------------------------------------
Overall System Status: HEALTHY (Exit Code: 0)
==================================================
```

### JSON Output
```bash
python3 health_check.py --json
```

### Custom Alerts and Multiple Disk Paths
```bash
python3 health_check.py \
  --warn-disk 80 \
  --warn-ram 85 \
  --paths / /var /mnt/storage
```

### Automated Monitoring in Crontab (Sends alert email on non-zero exit)
```bash
*/15 * * * * /usr/bin/python3 /path/to/health_check.py --quiet || echo "Server alert detected!" | mail -s "Server Alert" admin@example.com
```

## 📄 License
MIT License.