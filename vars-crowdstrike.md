## CrowdStrike

##### System Extension Status
```bash
systemextensionsctl list com.apple.system_extension.endpoint_security | awk -F"\t" '/com.crowdstrike.falcon.Agent/{gsub(/[\[\]]/,""); print $NF}'
```

##### Connectivity to Falcon Console
```bash
/Applications/Falcon.app/Contents/Resources/falconctl stats | awk '/State:/{print $NF}'
```

##### Launch Agent Status
```bash
launchctl print gui/"${console_uid}"/com.crowdstrike.falcon.UserAgent | awk '/^\tstate/{print $NF}'
```
