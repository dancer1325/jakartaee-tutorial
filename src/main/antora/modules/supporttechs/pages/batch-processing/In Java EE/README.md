# Batch applications in Java EE
* '.xml' files                                     -- Check any module under '/batch' -- 
  * define the job — based on — batch artifacts
* Java classes                                     -- Check any module under '/batch' --
  * logic of batch artifacts

# Steps to create the batch application
* identify the
  * input sources
  * steps
  * desired final result
* organize, determining the order of
  * steps
  * decision elements
* create the batch artifacts
* define the job

# Properties
* — can be associated to —     
  * jobs
  * steps
* — are defined in — job definition .xml file            -- Check any module under '/batch' --
* - can be accessed — via batch runtime’s context objects — by batch artifacts

# Parameters
* uses
  * partitioned steps         -- TODO: Find one --
  * submitting a job          -- TODO: Find one --
              
---

# Notes
* All the related examples are in 'javaee-tutorial examples' OR 'jakartaee-tutorial-examples' under '/batch' folder