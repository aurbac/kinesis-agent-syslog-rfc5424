# Kinesis Agent - Example configuration to support syslog RFC5424

/etc/aws-kinesis/agent.json

``` json
{
  "cloudwatch.endpoint": "monitoring.us-east-1.amazonaws.com",
  "cloudwatch.emitMetrics": true,
  "firehose.endpoint": "firehose.us-east-1.amazonaws.com",
  "checkpointFile": "/opt/aws-kinesis-agent/run/checkpoints",
  "flows": [
    {
      "filePattern": "/var/log/systemd.log",
      "initialPosition": "START_OF_FILE",
      "deliveryStream": "syslog",
      "dataProcessingOptions": [
              {
                      "maxBufferAgeMillis": "2000",
                      "optionName": "LOGTOJSON",
                      "logFormat": "SYSLOG",
                      "matchPattern": "^<(\\d{1,3})>([1-9]{0,1}) (\\d{4}\\-\\d{2}\\-\\d{2}T\\d{2}:\\d{2}:\\d{2}(?:\\.\\d{1,6}){0,1}(?:Z|[\\-+]\\d{2}:{0,1}\\d{2})) ([\\-\\.:%_a-zA-Z0-9]{1,255}) (-|\\p{Graph}{1,48}) (-|\\p{Graph}{0,128}) (-|\\p{Graph}{1,32}) (-|\\[.*?\\]) (.+?)",
                      "customFieldNames": ["priority", "version", "timestamp", "hostname", "appname", "procid", "msgid", "structured_data", "message"]
              }
      ]
    }
  ]
}
```
