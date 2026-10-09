# On-Premise Agent Global Updates — Summary

**Data as of:** 9 Oct 2026 (live Snowflake, `SILVER.MONGODB.AGENTS`; last heartbeat ingested 09 Oct 03:28 UTC)
**Program baseline:** 13 Jul 2026 (per Confluence program hub)
**Sources:** [Confluence — On Premise Agents Migrations: Global Updates](https://celigo.atlassian.net/wiki/spaces/IO/pages/2300346371/On+Premise+Agents+Migrations+-+Global+Updates) · [Snowflake — Agents Global Updates dashboard](https://app.snowflake.com/nsqaufd/uua36379/#/streamlit-apps/DATA_ROOM_DEV.INFLUXDB.AGENTS_GLOBAL_UPDATES)
**Owner:** Prudhvi Vemulapati (Product) · **Epic:** [IO-161076](https://celigo.atlassian.net/browse/IO-161076) · **CIP:** [CIP-2440](https://celigo.atlassian.net/browse/CIP-2440)

---

## Term dictionary

Every number in this document uses these definitions. All counts exclude Celigo-internal accounts.


| Term                 | Definition                                                                                    |
| -------------------- | --------------------------------------------------------------------------------------------- |
| **Legacy agent**     | Agent reporting a version **below 4.6.0**                                                     |
| **Latest agent**     | Agent reporting version **5.7.1 or above** (the current supported release)                    |
| **Not on latest**    | Agent reporting **any version below 5.7.1** — this includes legacy agents                     |
| **Active agent**     | Agent whose **last heartbeat was within the past 3 months** (on or after 11 Jul 2026)         |
| **Non-active agent** | Agent whose **last heartbeat was more than 3 months ago**, or that has never sent a heartbeat |
| **Total agents**     | Active agents + non-active agents — every agent record ever created                           |


**Active fleet (today):** **398** active agents · **282** customers. Success metrics below use this active population only.

---

## Headline

**Active fleet — are agents on the latest release (5.7.1+)?**


|               | Program start (Jul 2026) | Today (Oct 2026)             |
| ------------- | ------------------------ | ---------------------------- |
| On latest     | 134 of 347 active agents | **293 of 398** active agents |
| Not on latest | 213 of 347 active agents | **105 of 398** active agents |


In plain terms: at start, about **2 in 5** active agents were on latest; today about **3 in 4** are. The count still on older releases **dropped by more than half** (213 → 105).

**Legacy program (< 4.6.0 → latest)**


| Outcome                                     |                                   |
| ------------------------------------------- | --------------------------------- |
| Moved off legacy (of 150 targeted at start) | **48 / 150** (32%)                |
| Still legacy and active today               | **102** agents · **91** customers |


The Jul–Sep email cohort upgraded about **1 in 3** targeted agents; the rest are the Oct 2026 carry-over. Further progress likely needs **auto-update / targeted rollout**, not email alone.

---

## 1. v3.7.0 cohort — the slice we actually ran


| Measure                          | Agents  | % of targeted agents | Customers | % of targeted customers |
| -------------------------------- | ------- | -------------------- | --------- | ----------------------- |
| Targeted (13 Jul baseline)       | **110** | 100%                 | **89**    | 100%                    |
| Still on v3.7.0 and active today | **73**  | 66.4%                | **65**    | 73.0%                   |
| Converted to latest              | **37**  | **33.6%**            | **24**    | **27.0%**               |


A customer counts as converted only when **every** one of their v3.7.0 agents has moved, which is why customer conversion trails agent conversion.

## 2. Phase-2 legacy tail


| Agent version | Targeted (Jul baseline) | Active agents today | Customers today   |
| ------------- | ----------------------- | ------------------- | ----------------- |
| v4.5.0        | 11                      | 11                  | 10                |
| v4.3.0        | 17                      | 10                  | 10                |
| v3.6.0        | 3                       | 2                   | 2                 |
| v3.5.0        | 2                       | 2                   | 2                 |
| v3.4.0        | 7                       | 4                   | 4                 |
| **Total**     | **40**                  | **29**              | **28** (distinct) |


The drop from 40 to 29 happened organically through customer-initiated upgrades and decommissions, not through program outreach.

---

## 3. Fleet position — active agents

Percentages are the **share of the 398 active agents** (or of the 282 active customers, where stated).


|                                 | Jul 2026 baseline | Today (9 Oct 2026) | Agents today as % of active agents | Customers today | Customers as % of active customers |
| ------------------------------- | ----------------- | ------------------ | ---------------------------------- | --------------- | ---------------------------------- |
| Active agents                   | 347               | **398**            | 100%                               | **282**         | 100%                               |
| On latest (5.7.1+)              | 134               | **293**            | **73.6%**                          | **205**         | **72.7%**                          |
| Not on latest (below 5.7.1)     | 213               | **105**            | **26.4%**                          | **94**          | 33.3%                              |
| *of which legacy (below 4.6.0)* | *150*             | ***102***          | ***25.6%***                        | ***91***        | *32.3%*                            |


---

## 4. Active legacy agents remaining, by version

Legacy agents only (below 4.6.0). **Agents (3 mo)** = heartbeat in the past 3 months (active per term dictionary). **Heartbeat in last 1 month** = subset with heartbeat in the past 30 days. **Online now** = agent marked online in platform data at query time (`OFFLINE` = false).


| Agent version | Agents (3 mo) | Heartbeat in last 1 month | Online now | Customers         |
| ------------- | ------------- | ------------------------- | ---------- | ----------------- |
| v4.5.0        | 11            | 11                        | 11         | 10                |
| v4.3.0        | 10            | 10                        | 9          | 10                |
| v3.7.0        | 73            | 60                        | 59         | 65                |
| v3.6.0        | 2             | 2                         | 2          | 2                 |
| v3.5.0        | 2             | 2                         | 1          | 2                 |
| v3.4.0        | 4             | 4                         | 4          | 4                 |
| **Total**     | **102**       | **89**                    | **86**     | **91** (distinct) |


v3.7.0 holdouts are 72% of what is left. Everything else is a long thin tail of 2–11 agents per version.

---

## 5. Forced update (legacy GitHub path)

### Impact (legacy, online now)

- **Impact radius (150 → 86 online):** The Jul 2026 legacy program targeted **150 active agents** (Confluence program baseline). After cohort outreach, conversions, and organic drop, a **forced GitHub release applies to 86 legacy agents · 78 customers** (**online now** — next update check ~every 4 hours). **102** agents · **91** customers remain legacy-**active (3 mo)**; only **online now** agents are in the forced-update radius (§4).
- **One shot, not phased:** all legacy agents on the old GitHub feed see the **same** release — we **cannot** cohort or throttle a forced update the way we did with emails; one publish applies to every agent that polls that repo.
- **Staging:** forced GitHub auto-update tested on staging ([IO-163749](https://celigo.atlassian.net/browse/IO-163749)) for **v3.7.0, v4.3.0, v4.5.0, and v3.6.0** (Desktop + Service) through to current stable.

### Procedure

- **Build** production Electron release for **v5.7.1** (`.exe`, `.blockmap`, `latest.yml`).
- **Publish once** to [celigo/integrator-on-premise-agent releases](https://github.com/celigo/integrator-on-premise-agent/releases) — all eligible legacy agents pick it up on their shared GitHub feed (~every 4 hours).
- **Fallback:** failed auto-update leaves the agent on its current version; CS can use portal manual install or **older agent installers we retain internally** if a customer needs their previous version back ([CS Runbook](https://celigo.atlassian.net/wiki/spaces/IO/pages/2247983125/On-Premise+Agent+Update+CS+Team+Runbook+FAQ)).

---

## 6. Process and communication

([Program hub](https://celigo.atlassian.net/wiki/spaces/IO/pages/2300346371/On+Premise+Agents+Migrations+-+Global+Updates) · [Cohort strategy](https://celigo.atlassian.net/wiki/spaces/IO/pages/2248704016/Cohort+based+On-Premise+Agent+Global+Update+Strategy))

- **Scope:** legacy agents first (**v3.7.0** — 110 agents / 89 customers); **manual update** from the portal (pause flows → download installer → verify **v5.7.1**), not a GitHub forced push in this phase.
- **Rollout:** internal **Cohort 0**, then **six customer cohorts** (simple → multi-agent/EU → Premier → tail); **13 Jul – 30 Sep 2026**.
- **Comms:** **three emails** per cohort (Day **0 / 10 / 21**), **30-day** deadline per cohort; cohorts started **one week apart** ([templates](https://celigo.atlassian.net/wiki/spaces/IO/pages/2247131201/Customer+Communications)).
- **Support:** [CS runbook & FAQ](https://celigo.atlassian.net/wiki/spaces/IO/pages/2247983125/On-Premise+Agent+Update+CS+Team+Runbook+FAQ), macros, and [Help Center guide](https://docs.celigo.com/hc/en-us/articles/52212447854875-Update-your-on-premise-agent); **direct CS outreach** for Premier (Cohort 4).
- **Readiness:** **v3.7.0 staging validated** before first customer email; review gate between cohorts.
- **Tracking:** [Snowflake](https://app.snowflake.com/nsqaufd/uua36379/#/streamlit-apps/DATA_ROOM_DEV.INFLUXDB.AGENTS_GLOBAL_UPDATES) + [Splunk](https://celigo.splunkcloud.com/en-US/app/search/agent_offline_and_errors) dashboards.

