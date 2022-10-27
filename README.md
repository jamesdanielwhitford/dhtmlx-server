# dhtmlx-server
```sql
CREATE DATABASE bryntum;
```
```sql
USE bryntum;
```
```sql
CREATE TABLE `tasks` (
  `id` varchar(80) NOT NULL,
  `parentId` varchar(80) DEFAULT NULL,
  `name` varchar(255) DEFAULT NULL,
  `startDate` datetime DEFAULT NULL,
  `endDate` datetime DEFAULT NULL,
  `effort` float(11, 2) DEFAULT NULL,
  `effortUnit` varchar(255) DEFAULT 'hour',
  `duration` float(11, 2) unsigned DEFAULT NULL,
  `durationUnit` varchar(255) DEFAULT 'day',
  `percentDone` float(11, 2) unsigned DEFAULT 0,
  `schedulingMode` varchar(255) DEFAULT NULL,
  `note` text,
  `constraintType` varchar(255) DEFAULT NULL,
  `constraintDate` datetime DEFAULT NULL,
  `manuallyScheduled` tinyint DEFAULT 0,
  `effortDriven` tinyint DEFAULT 0,
  `inactive` tinyint DEFAULT 0,
  `cls` varchar(255) DEFAULT NULL,
  `iconCls` varchar(255) DEFAULT NULL,
  `color` varchar(255) DEFAULT NULL,
  `parentIndex` INT(11) DEFAULT 0,
  `expanded` tinyint DEFAULT 0,
  `calendar` int(11) DEFAULT NULL,
  `deadline` datetime DEFAULT NULL,
  `direction` varchar(255) DEFAULT NULL,
  `$PhantomId` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`),
  INDEX (`parentId`),
  CONSTRAINT `fk_tasks_tasks` FOREIGN KEY (`parentId`) REFERENCES `tasks`(`id`),
  INDEX (`calendar`),
  CONSTRAINT `fk_tasks_calendars` FOREIGN KEY (`calendar`) REFERENCES `calendars`(`id`)
) ENGINE=MyISAM AUTO_INCREMENT=1;
```
```sql
CREATE TABLE `dependencies` (
  `id` varchar(80) NOT NULL,
  `fromEvent` varchar(80) DEFAULT NULL,
  `toEvent` varchar(80) DEFAULT NULL,
  `type` int(11) DEFAULT 2,
  `cls` varchar(255) DEFAULT NULL,
  `lag` float(11, 2) DEFAULT 0,
  `lagUnit` varchar(255) DEFAULT 'day',
  `$PhantomId` varchar(255) DEFAULT NULL,
  `active` boolean,
  `fromSide` varchar(255) DEFAULT NULL,
  `toSide` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`),
  INDEX (`fromEvent`),
  CONSTRAINT `fk_dependencies_tasks` FOREIGN KEY (`fromEvent`) REFERENCES `tasks`(`id`),
  INDEX (`toEvent`),
  CONSTRAINT `fk_dependencies_tasks1` FOREIGN KEY (`toEvent`) REFERENCES `tasks`(`id`)
) ENGINE=MyISAM AUTO_INCREMENT=1;
```
```sql
INSERT INTO `tasks` (`id`, `name`, `expanded`, `iconCls`, `percentDone`, `startDate`, `endDate`, `parentId`, `effort`, `duration`, `parentIndex`) VALUES
(1000, 'Launch SaaS Product', 1, '', 34.248366013071895, '2022-11-14 00:00:00', '2022-11-29 00:00:00', NULL, 153.00, 45.00, 0),
("1", 'Setup web server', 1, '', 42.30769230769231, '2022-11-14 00:00:00', '2022-11-29 00:00:00', "1000", 13.00, 5.00, 0),
("11", 'Install Apache', 0, '', 50.00, '2022-11-14 00:00:00', '2022-11-17 00:00:00', "1", 3.00, 3.00, 0),
("12", 'Configure firewall', 0, '', 50.00, '2022-11-20 00:00:00', '2022-11-29 00:00:00', "1", 3.00, 3.00, 1);
```
```sql
INSERT INTO `dependencies` (`id`, `fromEvent`, `toEvent`, `lag`) VALUES
("1","11","12",2);
```
