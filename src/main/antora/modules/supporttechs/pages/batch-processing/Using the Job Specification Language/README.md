# `JobContext`
* := batch runtime’s context object which
  * allows
    * batch artifacts — can access to — properties       -- Check any repo under '/batch' --

# Job syntax -- `<job>` --
```
<job id=”…” restartable=”…”>
….
<listeners>...</listeners>
<properties>...</properties>
<step>...</step>
...
<flow>...</flow>
<split>...</split>
</job> 
```
* `<properties>`
  * just 1!  element is valid       -- Check '/simple' --
* `<listeners>` & `<step>` & `<flow>` & `<split>`
  * [0,) of these elements are possible to include
* `<listener ref=”BatchArtifactReference”/>`
  * batch artifact
    * implements `JobListener` interface
    * ’s methods are invoked
      * before the execution of the job
      * after the execution of the job
* `<step>`


# Step syntax -- `<step>` --
* can be a child of
  * `<job>` OR
  * `<flow>`
* main attributes
  * `id`
  * `next`
* elements / can contain
  * `<chunk>`
    * 1! for chunk-oriented steps
  * `<batchlet>`
    * 1! for task-oriented steps
  * `<properties>`
    * optional
  * `<listener>` & `<listeners>`
    * optional
    * if there are >1 `listener` → use `listeners`
    * if chunk-oriented steps → batch artifact can be an implementation of
      * `StepListener`
      * `ItemReadListener`
      * `ItemProcessListener`
      * `ItemWriteListener`
      * `ChunkListener`
      * `RetryReadListener`
      * `RetryProcessListener`
      * `RetryWriteListener`
      * `SkipReadListener`
      * `SkipProcessListener`
      * `SkipWriteListener`
    * if task-oriented steps → batch artifact must implement
      * `StepListener`
  * `<partition>`
    * optional
    * 1! for partitioned steps
  * `<end>`
    * 1!
    * set the status to `COMPLETED`
  * `<stop>`
    * optional
    * set the status to `STOPPED`
  * `<fail >`
    * optional
    * set the status to `FAILED`
  * `<next>`
    * if `next` attribute is missing → specify it
    * ≥ 1 are possible to include
   

# Chunk syntax -- `<chunk>` --
* `<step>` ’s child for chunk-oriented steps
* once the results of a chunk are commited → checkpoint is updated
* are processed in global Java EE transaction
  * == if the processing of 1 chunk’s item fails →
    * transaction is rolled back &
    * NO proccesed items from this chunk are stored
* possible attributes
  * `checkpoint-policy`
    * := way to commit the results of processing each chunk
    * possible values
      * `item`
        * after processing `item-count` items → chunk is commited
        * default
      * `custom`
        * depends on `checkpoint-algorithm`
  * `item-count`
    * := # of items to process before
      * committing the chunk
      * taking a checkpoint
    * 10 — default value —
  * `time-limit`
    * := # of seconds before  -- independently if `item-count` items have NOT been processed --
      * committing the chunk
      * taking a checkpoint
    * 0 — default value —
  * `buffer-items`
    * := boolean to indicate if processed items, before taking a checkpoint, are buffered
      * if true — call with buffered items done to → output writing part
    * true — default value —
  * `skip-limit`
    * := # of skippeable exceptions / skip during chunk processing
    * no limit — default value —
  * `retry-limit`
    * := # of attempts to execute this step / if a retryable exception occurs
    * no limit — default value —
* elements / can contain
  * `<reader>`
    * 1!
    * batch artifact — for — input retrieval part
  * `<processor>`
    * 1!
    * batch artifact — for — business processing part
  * `<writer>`
    * 1!
    * batch artifact — for — output writting part
  * `<checkpoint-algorithm>`
    * optional & just 1!
    * batch artifact — for — custom checkpoint policy
    * implements `CheckpointAlgorithm` interface
  * `<skippable-exception-classes>`
    * optional & just 1!
    * := set of exceptions /
      * thrown by `<reader>` | `<processor>` | `<writer>` &
      * are skipped
  * `<retryable-exception-classes>`
    * optional & just 1!
    * := set of exceptions /
      * thrown by `<reader>` | `<processor>` | `<writer>` &
      * are retried
  * `<no-rollback-exception-classes>`
    * optional & just 1!
    * := set of exceptions /
      * thrown by `<reader>` | `<processor>` | `<writer>` &
      * NOT cause that batch runtime rolls back the current chunk
    * if an exception is thrown & NOT specified here → rolled back
        
---

# Notes
* All the related examples are in 'javaee-tutorial examples' OR 'jakartaee-tutorial-examples' OR 'jakartaee-tutorial-examples' under '/batch' folder