---
keywords:
  - Adobe I/O
  - Extensibility
  - API Documentation
  - Developer Tooling
contributors:
  - 'https://github.com/duynguyen'
title: 'Lesson 3: Types of Alarm Feed'
---

# Lesson 3: Types of Alarm Feed

Beside the `/whisk.system/alarms/interval` feed in lesson 2, the alarms provider in Adobe I/O Runtime supports other types of feed.

## Firing a trigger once

The `/whisk.system/alarms/once` feed allows you to [fire event once at a specific time](https://github.com/apache/openwhisk-package-alarms#firing-a-trigger-event-once). The only required parameter is `date` to indicate when the trigger is fired. Optional params are `trigger_payload` and `deleteAfterFire`.

```yaml
triggers:
  runMeOnce:
    feed: /whisk.system/alarms/once
    inputs: 
      date: YYYY-MM-DDTHH:mm:ss.sssZ
      deleteAfterFire: true
```

Please note that `YYYY-MM-DDTHH:mm:ss.sssZ` is just the format for this field. You are free to update it with the date and time you want.

## Firing a trigger on a time-based schedule using cron

The `/whisk.system/alarms/alarm` feed allows you to [fire event on a time-based schedule using cron](https://github.com/apache/openwhisk-package-alarms#firing-a-trigger-on-a-time-based-schedule-using-cron). This is more generic than the `interval` and `once` feeds, because you can write crontab to configure the alarm service to trigger at the exact time and interval you want. The only required parameter is `cron`, which is a string based on the [UNIX crontab syntax](http://crontab.org) that indicates when to fire the trigger in UTC. Optional params are `trigger_payload`, `timezone`, `startDate` and `stopDate`. 

This example shows a cron schedule at 2am on Sundays in Central Europe Timezone (CET):

```yaml
triggers:
  sunday2am:
    feed: /whisk.system/alarms/alarm
    inputs: 
      cron: 0 2 * * 7
      timezone: CET
      startDate: 1601918992704
      stopDate: 1651918992704
```

