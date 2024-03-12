# `JobOperator`
* := interface which
  * `.start()`
  * `.stop()`
  * `.restart()`
  * `.getJobExecutions()`
  * `.getJobInstance()`

# `JobExecution`
* := interface which
  * `.getBatchStatus()` & `.getExitStatus()`
  * `.getExecutionId()`
  * `.getJobName()`
  * `.getStartTime()` & `.getLastUpdatedTime()` & `.getEndTime()`

# Based on your application → different components — invoke — batch runtime
* EJB
* servlet
* managed bean     -- Check '/phonebilling' & 'webserverlog' --


---

# Notes
* All the related examples are in 'javaee-tutorial examples' under '/batch' folder