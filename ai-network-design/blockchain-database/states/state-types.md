# State Types

Basically there are three types of blockchain states: values, rules, and owners.

| Type | Content |
| :--- | :--- |
| values | Database values e.g. account balance |
| rules | Database rules to determine who has value write permissions |
| owners | Database owners to determine who has ownership to change rules or ownership itself |

All access APIs and internal data structure for each state type are designed to be separate. For example, they use different root nodes in the internal key-value pair tree structure.

