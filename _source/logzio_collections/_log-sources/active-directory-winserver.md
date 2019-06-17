---
title: Ship Active Directory logs from Windows Server
logo:
  logofile: windows.svg
  orientation: vertical
data-source: Active Directory (Windows Server)
contributors:
  - imnotashrimp
shipping-tags:
  - server-app
  - security
---

## Setup

###### Configuration

**You'll need**:
[Winlogbeat 7](https://www.elastic.co/downloads/beats/winlogbeat) or
[Winlogbeat 6](https://www.elastic.co/guide/en/beats/winlogbeat/6.8/winlogbeat-installation.html)

1.  Download the Logz.io certificate

    Download the [Logz.io public certificate](https://raw.githubusercontent.com/logzio/public-certificates/master/COMODORSADomainValidationSecureServerCA.crt) to your machine.
    We'll place the certificate in `C:\ProgramData\Filebeat\COMODORSADomainValidationSecureServerCA.crt` for this example.

2.  Configure Windows applications as an input

    In the Winlogbeat configuration file (C:\Program Files\Winlogbeat\winlogbeat.yml by default), add this code block to the root level.

    {% include log-shipping/replace-vars.html token=true %}

    <div class="branching-container">

    * [Winlogbeat 7](#winlogbeat-7-code)
    * [Winlogbeat 6](#winlogbeat-6-code)
    {: .branching-tabs }

    <div id="winlogbeat-7-code">

    ```yaml
    # Winlogbeat 7 configuration

    winlogbeat.event_logs:
      - name: Application
        ignore_older: 72h
      - name: Security
      - name: System

    fields:
      logzio_codec: json
      token: <<SHIPPING-TOKEN>>
      type: wineventlog
    fields_under_root: true

    processors:
      - add_host_metadata: ~
      - add_cloud_metadata: ~
      - rename:
          fields:
          - from: "agent"
            to: "beat_agent"
          ignore_missing: true
      - rename:
          fields:
          - from: "log.file.path"
            to: "source"
          ignore_missing: true
      - rename:
          fields:
          - from: "log"
            to: "log_information"
          ignore_missing: true
    ```

    </div>

    <div id="winlogbeat-6-code">

    ```yaml
    # Winlogbeat 6 configuration

    winlogbeat.event_logs:
      - name: Application
        ignore_older: 72h
      - name: Security
      - name: System

    fields:
      logzio_codec: json
      token: <<SHIPPING-TOKEN>>
      type: wineventlog
    fields_under_root: true
    ```

    </div>

    </div>

3.  Add Logz.io as an output

    If Logz.io is not an output in the Winlogbeat configuration file (C:\Program Files\Winlogbeat\winlogbeat.yml by default), add it now.

    {% include log-shipping/replace-vars.html listener=true %}

    ```yaml
    output.logstash:
      hosts: ["<<LISTENER-HOST>>:5015"]
      ssl:
        certificate_authorities: ['C:\ProgramData\Filebeat\COMODORSADomainValidationSecureServerCA.crt']
    ```

4.  Remove remaining default blocks

    If the `output.elasticsearch` and `setup.template.settings` blocks are still in the configuration file, remove them.

    ```yaml
    # Remove this block if it's still in the config file
    setup.template.settings:
      index.number_of_shards: 3
    ```

    ```yaml
    # Remove this block if it's still in the config file
    output.elasticsearch:
      hosts: ["localhost:9200"]
    ```

5.  Restart Winlogbeat

    ```powershell
    PS C:\Program Files\Winlogbeat> Restart-Service winlogbeat
    ```

6.  Check Logz.io for your logs

    Give your logs some time to get from your system to ours, and then open [Kibana](https://app.logz.io/#/dashboard/kibana).

    If you still don't see your logs, see [log shipping troubleshooting]({{site.baseurl}}/user-guide/log-shipping/log-shipping-troubleshooting.html).
{: .tasklist .firstline-headline }