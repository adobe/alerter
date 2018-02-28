# Alerter

Alerter is a tool to manage Splunk alerts, searches and other operations

## First steps

Edit the config with the APP, SPLUNK_USERNAME, SPLUNK_PASSWORD and SERVER. FILTER sets the default filter to show alerts. JIRA_USERNAME and JIRA_PASSWORD for JIRA integration.

Example:

`
APP="app"
FILTER="Sev"
`

## Examples

### Create an alert sent to alerts with query and the name of the alert.

`./alerter  -s ap-api.serversc.com.com -m "alerts@adobe.com,-dcos-pd-email.7rpjk52x@cloud.pagerduty.com" -q "index=index-prod-*  source=apigateway.* 'Connection refused'" -c 'Sev3: Dev/Stage API connection refused'`

` ./alerter -s us-api.serversc.com.com -m "alerts@adobe.com,stage-splunk-based-index-stage-alert.myadwrbo@cloud.pagerduty.com" -q "index=index-dev-* OR index-stage-* source=service* m=bstr_internal_health lvl=error l=103" -e "*" -b "5" -x "50" -c 'Sev3: Dev/Stage Proactive Service Monitoring'`

### Show alerts

`sancheza-macOS:alerter sancheza$ ./alerter -s ap-api.serversc.com.com -a
Sev3: Dev/Stage API blockembargoips.conf not found
Sev2: Prod API connection refused
Sev2: Prod API blockembargoips.conf not found
Sev1: Prod Flight is Leaderless
Sev3: Dev/Stage API connection refused
Sev3: Dev API Service Upstream Server
Sev3: Dev/Stage API no memory in vhost_traffic_status_zone
Sev3: Dev/Stage API LUA worker error
Sev2: Prod API no memory in vhost_traffic_status_zone
Sev2: Prod API Service Upstream Server`

### Run a query

`./alerter -s ap-api.serversc.com.com -f 'search=search index=index-dev-* source=apigateway.* "Connection refused"'`

### Support webhook

`./alerter -s ap-api.serversc.com.com -m "sancheza@adobe.com" -q "index=index-prod-* source=service* m=bstr_internal_health lvl=error l=103" -e "*/15" -b "5" -x "30" -w 'http://www.google.es' -c 'Sev2: Prod Proactive Service Monitoring Example'`

### Delete alert

`./alerter -s ap-api.serversc.com.com -d 'Sev2: Prod Proactive Service Monitoring Example'`

### Create Jira

`./alerter -j`

## Author

Alejandro Sanchez Acosta <sancheza@adobe.com>
