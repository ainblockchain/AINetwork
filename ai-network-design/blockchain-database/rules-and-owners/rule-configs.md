# Rule Configs

## Syntax

Rule configs are stored as a ".write" property on a path in the database using SET\_RULE operation. 

```text
{
  <path>: {  // path can include variables like $key
    <to>: {
      <target_node>: {
        .write: <eval string to determine the write permission>
      }
    }
  }
}
```

Its value is an javascript eval string that will be evaluated true or false to determine users' permission on the path whenever a transaction with value write operations on the path is submitted. 

## Path Variables and Built-in Variables

The path can have path variables like "rules/transfer/$from/$to/value" to allow flexibility of rule expressions. In the same context, built-in variables are also provided by the system:

| Variable | Methods | Semantic | Example | API Version |
| :--- | :--- | :--- | :--- | :--- |
| auth |  | Sender \(signer\) address | auth === '$uid' | 1.0 |
| db | db.get\(&lt;db path&gt;\) | To get the value at the db path. Relative paths such as “.”, “..”, “../..” are supported. | !db.get\('transfer/$from/$to/$key'\) | 1.0 |
| db | db.eval\(&lt;rule config path&gt;\) | To eval the rule config at the rule path. Relative paths such as “.”, “..”, “../..” are supported. | db.eval\('apps/afan/follow/$uid'\) | TBD |
| newData |  | The new data to be set at the given path | db.get\('account/$from/balance'\) &gt;= newData | 1.0 |
| data |  | The existing data at the given path | data !== null | 1.0 |
| now |  | Current timestamp | now &lt;= $time + 24 \* 60 \* 60 | 1.0 |

## Examples

Rule configs can be set as the following examples:

```text
{
  transfer: {
    $from: {
      $to: {
        $key: {
          value: {
            .write: "auth === '$from' && !db.get(`transfer/$from/$to/$key`) && db.get(`account/$from/balance`) >= newData",
          }
        }
      }
    }
  },
  apps: {
    afan: {
      .write: "auth === '0x12345678901234567890123456789012345678'",
      follow: {
        $uid: {
          .write: "auth === $uid",
        }
      }
    }
  }
}
```

There is no ‘read’ permission in data access. It means all network participants can read your data. To secure data on specific node path, users need to encrypt the data with their own private key.

## Application of Rule Configs

Permission of a value write operation \(e.g. SET\_VALUE\) is check as follows:

* When there are no rule configs on the requested path, closest ancestor's rule config is applied
* If there are more than one path matched, the most specific rule config is applied
  * e.g. Among a\) /apps/$app\_id/$service, b\) /apps/afan/$service, c\) /apps/afan/wonny, c\) is applied.
* When the value of the write operation in request is an object, the operation is granted when the permission check succeeds on every path of object. For example, SET\_VALUE operation is requested on /foo/bar with value { abc: "abc\_val", def: "def\_val" }, it should pass the permission check on /foo/bar, /foo/bar/abc, and /foo/bar/def.
* Rule config always overrides its ancestors' rule configs

