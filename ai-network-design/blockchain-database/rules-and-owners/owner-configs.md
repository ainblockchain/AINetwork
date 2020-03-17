# Owner Configs

## Syntax

Owner configs are stored as a ".owner" property on a path  in the database using SET\_OWNER operation.

```text
{
  <path>: {  // path cannot include a variable like $key 
    <to>: {
      <target_node>: {
        .owner: {
          inherit: [
            "<ref1>",  // ref1 should be an ancestor node
            "<ref2>"   // ref2 should be an ancestor node
            ...
          ],
          owners: {
            "*": {
              write_owner: true | false,
              write_rule: true | false,
              branch_owner: true | false,
            },
            "<1st address>": {
              write_owner: true | false,
              write_rule: true | false,
              branch_owner: true | false,
            },
            "<2nd address>": {
              write_owner: true | false,
              write_rule: true | false,
              branch_owner: true | false,
            },
            ...
          }
        }
      }
    }
  }
}
```

Meaning of the syntax keywords can be summarized as follows:

| Keyword | Semantic | API Version |
| :--- | :--- | :--- |
| write\_owner | Property of users in owner configs. If this value is true, the user can write the owner config itself. Default value: false. | 1.0 |
| write\_rule | Property of users in owner configs. If this value is true, the user can write the rule config. Default value: false. | 1.0 |
| branch\_owner | Property of users in owner configs. If this value is true, the user can add a branching owner config, e.g. a user in /apps/afan/.owner can add branching owner rule /apps/afan/community/.owner. Default value: false. | TBD |
| inherit | Property of owner configs. Its value is given as an array of paths to owner configs. If it’s set, the owners on the specified paths are included in the owners. Ownership inheritance is allowed only from ancestors’ owner configs and, if there are conflicts, the descendant's owners have precedence over ancestor's owners. Default value: undefined. | TBD |

## Examples

Owner configs can be set as the following examples:

```text
{
  apps: {
    .owner: {
      owners: {
        "*": {
          write_owner: false,
          write_rule: false,
          branch_owner: true
        }
      }
    },
    afan: {
      .owner: {
        owners: {
          "0x12345678901234567890123456789012345678": {
              write_owner: true,
              write_rule: true,
              branch_owner: true
          }
        }
      }
    }
  }
}
```

## Application of Owner Configs

Write permission on a rule or owner path is check as follows:

* When there are no owner configs on the requested path, closest ancestor owner config is applied
* Owner config always overrides its ancestors' owner configs

