# 数据库设计

没有统一的标准，思路就是怎么将同步报文和新设备内的数据合理地存储。下面提供一下小K智能管家的示例：

```sql
DROP TABLE IF EXISTS "SHController";
DROP TABLE IF EXISTS "SHFloor";
DROP TABLE IF EXISTS "SHDevice";
DROP TABLE IF EXISTS "SHRoom";
DROP TABLE IF EXISTS "SHScene";
DROP TABLE IF EXISTS "SHGroup";
DROP TABLE IF EXISTS "SHIFTTTRule";
DROP TABLE IF EXISTS "SHDevAppArgs";
DROP TABLE IF EXISTS "SHHardwareInfo";
DROP TABLE IF EXISTS "SHGateway";
DROP TABLE IF EXISTS "SHArea";

CREATE TABLE IF NOT EXISTS "SHDevAppArgs" (
"nodeId"        INTEGER NOT NULL,
"type"          INTEGER NOT NULL,
"args"          TEXT,
PRIMARY KEY     ("nodeId","type")
);

CREATE TABLE IF NOT EXISTS "SHGuardSensor" (
"node_id"       INTEGER PRIMARY KEY NOT NULL,
"sensor_type"   INTEGER
);

CREATE TABLE IF NOT EXISTS "SHController" (
"node_id"               INTEGER PRIMARY KEY NOT NULL,
"bind_socket_node_id"   INTEGER,
"buttons"               TEXT
);

CREATE TABLE IF NOT EXISTS "SHDevice" (
"nodeId"        INTEGER NOT NULL,
"roomId"        INTEGER,
"type"          INTEGER NOT NULL,
"name"          TEXT,
"status"        TEXT,
"extralInfo"    TEXT,
"online"        INTEGER,
"realType"      INTEGER,
"gw_mac"        TEXT,
"devMac"        TEXT,
"macLastFour"   TEXT,
PRIMARY KEY     ("nodeId","type")
);

CREATE TABLE IF NOT EXISTS "SHRoom" (
"Id"            INTEGER PRIMARY KEY NOT NULL,
"name"          TEXT,
"icon"          TEXT,
"position"      TEXT,
"all_dnd"       INTEGER,
"areaId"        INTEGER
);

CREATE TABLE IF NOT EXISTS "SHScene" (
"Id"                INTEGER PRIMARY KEY NOT NULL,
"name"              TEXT,
"roomId"            INTEGER,
"image"             TEXT,
"type"              INTEGER,
"timerEnabled"      INTEGER,
"time"              TEXT,
"week"              TEXT,
"pannelIds"         TEXT,
"actions"           TEXT
);

CREATE TABLE IF NOT EXISTS "SHGroup" (
"Id"  INTEGER PRIMARY KEY NOT NULL,
"name"  TEXT,
"nodes" TEXT
);

CREATE TABLE IF NOT EXISTS "SHIFTTTRule" (
"Id"             INTEGER PRIMARY KEY NOT NULL,
"roomId"         INTEGER,
"enabled"        INTEGER,
"notified"       INTEGER,
"name"           TEXT,
"type"           TEXT,
"conditions"     TEXT,
"actions"        TEXT,
"limitCondtions" TEXT
);

CREATE TABLE IF NOT EXISTS "SHHardwareInfo" (
"mac"               TEXT PRIMARY KEY NOT NULL,
"version"           TEXT,
"productId"         INTEGER,
"onlineStatus"      INTEGER,
"optFailedCount"    INTEGER
);

CREATE TABLE IF NOT EXISTS "SHGateway" (
"nodeId"              INTEGER PRIMARY KEY NOT NULL,
"name"                TEXT,
"mac"                 TEXT,
"ip"                  TEXT,
"online"              INTEGER,
"type"                INTEGER,
"runVersion"          TEXT,
"downloadVersion"     TEXT
);

CREATE TABLE IF NOT EXISTS "SHCommonDevices" (
"mac"         TEXT NOT NULL,
"channel"     INTEGER,
"optCount"    INTEGER,
PRIMARY KEY   ("mac","channel")
);

CREATE TABLE IF NOT EXISTS "SHArea" (
"aid"         INTEGER PRIMARY KEY NOT NULL,
"name"        TEXT NOT NULL,
"rooms"       TEXT NOT NULL
);
```