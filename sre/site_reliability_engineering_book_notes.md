# Site Reliability Engineering by Betsy Beyer et. al

## Chapter 1 - Introduction

### SysAdmin system

Traditionally **system administrators** in the ‘ops’ team. But in this system **team size scales with system load** (cost/time of manual intervention).

Tension develops between development and ops team due to: 

1. *Sysadmins* and *developers* are from different backgrounds: Use different vocab
2. Different ideas of problem solutions
3. Different idea of target product stability

**Incentive battle**: Dev team wants to push new features **vs.**  ops team wants to keep product stable

### Introducing SRE

SRE team consists of:

1. 50% Software Engineers
2. 50% Engineers who have same skills as above and *in adddition* master skills like **UNIX internals and networking**

Main motivation for this is to have a team who 

- Gets bored doing manual work
- Has skills to develop **automation**

#### SRE team must be focused on engineering

Enforce 50% cap of time spent on 'ops' work. Rest must be spent on engineering. This is enforced by time tracking. If 50% is exceeded, redirect ops load to dev team until it drops under 50% again.

## Chapter 3 - Embracing Risk

Increasing reliability (number of 9's) has costs in 2 dimensions

1. Redundant machines
2. Opportunity cost (engineers could have spent time on new revenue-generating products)

**Reliability Metrics:**

- Unplanned downtime
- Request success rate (makes sense for large distributed systems)

### Risk of Consumer Services

Consider:

- Service level users expect
- Does different types of failures have different effect (constant low-key failures vs rare full-blown outages)
- Is service directly tied to revenue?
- Competitor's service level?
- Consumers vs. enterprise
- Is cost of one more 9 paid for by increased revenue?

#### Background noise

ISP noise estimated around 0.01-1%

### Risk of InfrastructureServices
