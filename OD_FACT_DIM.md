## Let's study Fact / OD / DM relationship

#### Fact table
- Fact table is used to recored events, transaction
- Contains numeric metrics such as a sales amount, order quality, clicks
##### => Think of it as the core table for analysis because it answers "how much, how many, when"


#### OD table
- A staging area table that stores raw or lightly processed data from operational systems
- Data comes directly from ERP , CRM , or other transactional systems with minimal transformation


#### DM table
- A subject-oriented dataset designed for business users
- Built on top of Fact and Dimension tables; optimized for reporting or BI tools


### Relationship
``` pgsql
Operational DB → OD tables → Fact / Dimension tables → DM tables
```
