# Dev/Ops
#📥 
%%
#coding #SWE 
#concept

**Related:**
-  [[Development Basics]]

%%

Goal: To automate everything

==Responsiveness:==
==Release Management:==
==Availability:==
==Scalability:==
==Privacy:==
==Authentication:==
==Data Integrity:==

## 3-Tiered Shared-Nothing Architecture
Scaling presentation and application tiers: 
- Add virtual machines
- Reconfigure load balances

Scaling persistence tier: 
- Hard!
	- Sharding: Partition data scross multiple indepndent shards
		- Pros: Scales great if date is evenly divided
		- Cons: Bad if operations touch more than one table
	- Replication: replicate all data everywhere
		- Pros: Multi-table queries are fast 
		- Cons: Writes have to replicate every replica 


## Availability and Responsiveness
5 nines: 99.999% uptime
Hard for SaaS apps to get more than that: Upgrades gone bad, denial of service attacks, exceptions

### Responsiveness
SLO: Service-level objective 
Some quantitative goal for responsiveness
Apdex: Score between 0-1 that summarizes responsiveness according to a latency threshold parameter $T$

Response is:
- Satisfactory if completed within $T$
- Tolerable if completed within $4T$
- Unsatisfactory if > $4T$

$$
\text{Apdex} = (\text{satisfactory} + 0.5(\text{tolerable}))/N
$$

📝 Human threshold of perception is 100-200 milliseconds  
📝 Evidence suggests that response times above 8 seconds lead to users going elsewhere

### Upgrade Troubles
- During upgrade rollout, some instances will have the prev version, some the new
- If requires a destructive DB migration, you can't just drop the DB in production

Naive approach: 
1. Take service offline and apply destructive migration and copy data 
2. Deploy new code
3. Bring service back online

Feature flags:
1. Do non-destructive migration
2. Deploy method protected by feature flag
3. Flip flag on, if disaster, flip off
4. Once all records are moved, deploy the new code without the feature flag
5. Apply migration to remove old columns

Other uses for [[Feature Flags]] - In file