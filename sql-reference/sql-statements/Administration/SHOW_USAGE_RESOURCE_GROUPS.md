# SHOW USAGE RESOURCE GROUPS

## 功能

展示所有资源组在各 BE 上的使用信息。此功能从 v3.1.4 开始支持。

## 语法

```SQL
SHOW USAGE RESOURCE GROUPS
```

## 返回

- `Name`：资源组的名称。
- `Id`：资源组的 ID。
- `Backend`：BE 的 IP 或 FQDN。
- `BEInUseCpuCores`：该资源组在该 BE 上正在使用的 CPU 核数，该值为一个估计近似值。
- `BEInUseMemBytes`：该资源组在该 BE 上正在使用的内存字节数。
- `BERunningQueries`：该资源组在该 BE 上还未结束的查询数量。

## 使用说明

- 这些资源使用信息由 BE 周期性汇报给 Leader FE，汇报周期为 `report_resource_usage_interval_ms`，默认 1s。
- 结果中只会展示 BEInUseCpuCores/BEInUseMemBytes/BERunningQueries 至少一个为正数的行，即只有一个资源组在一个 BE 上使用了某种资源时，才会在结果中进行展示。

## 示例

```Plain
MySQL [(none)]> SHOW USAGE RESOURCE GROUPS;
+------------+----+-----------+-----------------+-----------------+------------------+
| Name       | Id | Backend   | BEInUseCpuCores | BEInUseMemBytes | BERunningQueries |
+------------+----+-----------+-----------------+-----------------+------------------+
| default_wg | 0  | 127.0.0.1 | 0.100           | 1               | 5                |
+------------+----+-----------+-----------------+-----------------+------------------+
| default_wg | 0  | 127.0.0.2 | 0.200           | 2               | 6                |
+------------+----+-----------+-----------------+-----------------+------------------+
| wg1        | 0  | 127.0.0.1 | 0.300           | 3               | 7                |
+------------+----+-----------+-----------------+-----------------+------------------+
| wg2        | 0  | 127.0.0.1 | 0.400           | 4               | 8                |
+------------+----+-----------+-----------------+-----------------+------------------+
```
