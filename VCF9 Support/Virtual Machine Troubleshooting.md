#vcf9 

#### VMware Tools Installation

| Component | Cause                                                                                         |
| --------- | --------------------------------------------------------------------------------------------- |
| VM        | Incorrect guest OS is selected for the Virtual Machine                                        |
| ESX Host  | Correct tools ISO image is not loaded<br>ISO image cannot be found<br>ISO image is corrupted. |

#### VSS / Snapshot Quiescing 
**Troubleshooting snapshots and VSS issues**

- Verify that VMware Tools is running and installed.
- Ensure that all the appropriate OS and application services are running.
- Ensure that you are using the Microsoft Software Shadow Copy.
- Ensure that all VSS writers are stable and are not reporting an error:
	- `vssadmin list writers` on the Windows VM.
