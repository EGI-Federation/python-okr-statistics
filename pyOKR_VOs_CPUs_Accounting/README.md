# Calculate the Cloud CPU/h consumed in the specific period

This python client generates the Cloud|HTC CPU/h of the production VOs registered in the [EGI Operations Portal](https://operations-portal.egi.eu/)

Edit the `openrc.sh`, configure the `scope=cloud` and the specify the `ACCOUNTING_METRIC` to be calculated

```bash
export ACCOUNTING_SERVER_URL="https://accounting.egi.eu"

# Available scope: 'cloud', 'egi'
export ACCOUNTING_SCOPE="cloud" # for Cloud Compute

# Available metrics (for scope=cloud):
# 'sum_elap_processors', 'mem-GByte', 'vm_num', 'sum_elap', 'cost', 'net_in', 'net_out', 'disk', 'processors'
export ACCOUNTING_METRIC="sum_elap_processors"

# Google Spreadsheet settings
export SERVICE_ACCOUNT_PATH=${PWD}"/.config/"
export SERVICE_ACCOUNT_FILE=${SERVICE_ACCOUNT_PATH}"service_account.json"
export GOOGLE_SHEET_NAME="OKR_Reports"
export GOOGLE_CLOUD_WORKSHEET="Accounting Cloud CPU/h"

export DATE_FROM="2023/01"
export DATE_TO="2023/06"
```

Source the environment settings and run the client

```bash
]$ source openrc.sh && python3 pyVOs_CPUs_Accounting_v0.2.py

Log Level = INFO

[INFO]     Reporting Period: 2020.01-06
[Cloud]    Total Cloud CPU/h = 12,050,254
[noVOCPUs] VOs with *no* accounting records (3)
[VOCPUs]   VOs with *accounting* records (47)
```

The VO statistics are updated in the Google worksheet `Accounting Cloud CPU/h`
