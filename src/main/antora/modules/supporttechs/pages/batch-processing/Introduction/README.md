# Batch processing
* := run batch jobs on computers
* generics are NOT supported           -- Check '/batch/simple' --
  * → you need to cast

# Batch jobs
* := tasks / can be executed — without — user interaction
* uses
  * periodical tasks
  * resource usage is low
* == chunk-oriented steps + task-oriented steps
  * steps
    * := phase of a batch job which
      * independent
      * sequential
  * chunk-oriented steps             -- Check '/batch/phonebilling'  -- 
    * == input retrieval part + business processing part + output writing part
      * input retrieval part
        * read items
          * from a data source
          * 1 by 1 
        * once the chunk is processed → current position is saved
      * business processing part
        * apply business logic 1 by 1 
      * output writing part
        * group results into a chunk
          * once the chunk is processed → current position is saved 
    * once the chunk reaches a configurable size → results are stored 
    * checkpoints
      * := point to restart an interrupted chunk step 
  * task-oriented steps             -- Check '/batch/simple'  --

# Batch artifact
* := part of a                           -- Check '/phonebilling'
  * chunk-oriented step OR
  * task-oriented step OR
  * decision element OR
  * another component

# Parallel Processing
* use cases                 -- Check TODO: project --
  * steps are independent
  * chunk-oriented steps / items are independent
    * by default, it’s 1 by 1

# Status and decision elements
* status                    -- Check TODO: project --
  * valid for
    * step
    * Batch jobs
  * tracked
  * available values
    * running
    * completed
      * successfully
      * interrupted
      * error
* decision elements         -- Check TODO: project --
  * based on the previous step‘s exist — determines —
    * next step or
    * terminate the Batch jobs
              
---

# Notes
* All the related examples are in 'javaee-tutorial examples' under '/batch' folder