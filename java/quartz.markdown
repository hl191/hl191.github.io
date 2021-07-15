---
layout: page
title: Quartz
exclude: true
---

[Quartz](http://www.quartz-scheduler.org/) uses a Scheduler to register Jobs.

We can build a Job using the Quartz API like this:

```java
JobBuilder.newJob()
          .ofType(QuartzTask.class)
          .storeDurably()
          .withIdentity("JOB_NR_1")
          .withDescription("Job nummeros uno ...")
          .setJobData(new JobDataMap(Map.of(QuartzTask.EXECUTION_ID,"1")))
          .build()
```

The job then has to be registered in the Scheduler

```java
scheduler.addJob(job, false); // Second parameter specifies if it is to replace
```

Now that the job is registered, we may define a trigger, which will then execute the job.

```java
TriggerBuilder.newTrigger()
              .forJob(job)
              .startAt(DateBuilder.todayAt(10,0,0))
              .build();
```

Triggers can also be modified by a calendar such as exclusion dates or holidays:

```java
HolidayCalendar holidayCalendar = new HolidayCalendar();
holidayCalendar.addExcludedDate(DateBuilder.newDate().inMonthOnDay(DateBuilder.AUGUST, 1).build());
holidayCalendar.addExcludedDate(DateBuilder.newDate().inMonthOnDay(DateBuilder.DECEMBER, 25).build());
holidayCalendar.addExcludedDate(DateBuilder.newDate().inMonthOnDay(DateBuilder.DECEMBER, 26).build());

// Add the holiday calendar to the scheduler
scheduler.addCalendar("holidayCalendar", holidayCalendar, true, true);

// Modify the trigger with the holidays
Trigger trigger = TriggerBuilder.newTrigger()
                                .forJob(job)
                                .modifiedByCalendar("holidayCalendar")
                                .startAt(DateBuilder.todayAt(10,0,0))
                                .build();
scheduler.scheduleJob(trigger);
```

Triggers configured for a job can be retrieved and even modified later on. When the trigger is fired, it is removed from the data source.

To support a clustered environment we may use the following `application.properties` in Spring:

```java
spring.quartz.job-store-type=jdbc
spring.quartz.properties.org.quartz.jobStore.isClustered=true
spring.quartz.properties.org.quartz.scheduler.instanceId=AUTO
```
