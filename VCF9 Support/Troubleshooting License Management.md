#vcf9 

### Authorization

To manage a VCF license in the VCF Business Services Console, you must have sufficient access and entitlements.

If a `Not Authorized` error appears while an administrator logs in, verify that:
- The administrator is correctly registered.
- The administrator has correct access.
- The VCF 9.0 entitlements are available.

### License Management

To license your environment, you must have an installed VCF Operations instance, register it in the VCF Business Services console, and add licenses with available capacity. VCF licenses are centrally managed in VCF Operations.

### Log Files

| Component             | Log File                                                                                                                                           |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| API service           | `/storage/log/vcops/log/api.log`<br>`/storage/log/vcops/log/http_api.log`                                                                          |
| VCF license plug-in   | `/storage/log/vcops/log/vcf-licensing-plugin.log`                                                                                                  |
| License usage plug-in | `/storage/log/vcops/log/vcf-usage-plugin.log`                                                                                                      |
| Analytics service     | `/storage/log/vcops/log/analytics-wrapper.log`<br>`/storage/log/vcops/log/analytics-<id>.log`<br>`/storage/log/vcops/log/analytics.audit-<id>.log` |
| Management Adapter    | `/storage/logs/vcops/log/adapters/ManagementAdapter/ManagementAdapter_XX.log`                                                                      |

---

- If you encounter an issue importing a license file, review API and Management Adapter log files.

- VCF Operations stores license information locally in its central database:
	*Logs*
	- `/storage/log/vcops/log/analytics.audit-<uid>.log` - search for **VCF_ENTITLEMENT_STORE**
	
	*Database*
```sql
SELECT * from vcf_entitlement WHERE allocation_id = ''

SELECT * from vcf_entitlement INNER JOIN vcf_entitlement_subscription ON (vcf_entitlement_subscription.allocation_id = vcf_entitlement.allocation_id) WHERE vcf_entitlement.allocation_id = ''

SELECT * from vcf_entitlement INNER JOIN vcf_entitlement_subscription ON (vcf_entitlement_subscription.allocation_id = vcf_entitlement.allocation_id) INNER JOIN vcf_entitlement_policy_warning ON (vcf_entitlement_policy_warning.allocation_id = vcf_entitlement.allocation_id) WHERE vcf_entitlement.allocation_id = ''
```

- Potential errors in license entitlement
	- Entitlement reports incorrect information
	- Newly added license is not consumed
	- New vCenter cloud account is not consumed
	- Restricted mode is reported
	
	VCF Operations reports these symptoms when the license file cannot be read correctly. Verify that the license file is correct.
	When troubleshooting **license assignment** to vCenter, review the API, license plugin and management adapter logs. Search for "**entitlement**".
	
	Potential vCenter licensing failures:
	- Security validation failure:
		- Error - **JwsSecurityException**
	- License content validation failure:
		- Error - **Entitlement has expired**
	- License has insufficient capacity:
		- Error - **Insufficient Entitlement capacity**

#### Setting Log Level

*GUI*
1. Navigate to **Administrator > Control Panel > Support Logs**
2. Select Collector in tree view
3. Click **Edit Properties**
4. Add `com.vmware.adapter.management` log name and set desired value.

*CLI*
Edit `/usr/lib/vmware-vcops/user/conf/analytics/plugins/log4j2.properties` and set desired level.


### ESX Commands

```bash

# Current license state of a host
/bin/vim-cmd vimsvc/license --show

# Retrieve license information from the ESX config store
/bin/configstorecli config current get -c esx -g licensing -k entitlements
/bin/configstorecli config current get -c esx -g licensing -k state

# Retrieve the host license information with the esxcli command
/bin/esxcli licensing entitlement list
/bin/esxcli licensing credential list

```