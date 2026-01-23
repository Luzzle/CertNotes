#NSE4 

OFortiAnalyzer stores incoming logs in the following manner:
1. Raw
	- For long term storage purposes.
	- Unable to be viewed in FortiView or Low View.
2. Database
	- Logs are inserted into an SQL database.
	- Logs can be viewed and reported.

FortiGate uses UDP 514 for log transmission by default.

### Operating Modes
#### Analyzer Mode
Central log aggregator for one or more logging devices, or a FortiAnalyzer in collector mode.
![[Pasted image 20251214172935.png|700]]

#### Collector Mode
Collects logs from multiple devices and forwards them to an instance of FortiAnalyzer in analyzer mode. Used for archiving, not analytics.

![[Pasted image 20251214173054.png|700]]