## 1. Dataset Description


This failure dataset contains the injected faults, the workload, the effects of failure (both the user-side impact and our own in-depth correctness checks), and the error logs produced by the OpenStack cloud management system.
Please refers to the paper [How Bad Can a Bug Get? An Empirical Analysis of Software Failures in the OpenStack Cloud Computing Platform](https://dl.acm.org/doi/10.1145/3338906.3338916) accepted for presentation at the ESEC-FSE 2019 conference. 

Please, **cite the paper** if you use the dataset for your research:

```
@inproceedings{cotroneo2019bad,
  title={How bad can a bug get? an empirical analysis of software failures in the OpenStack cloud computing platform},
  author={Cotroneo, Domenico and De Simone, Luigi and Liguori, Pietro and Natella, Roberto and Bidokhti, Nematollah},
  booktitle={Proceedings of the 2019 27th ACM Joint Meeting on European Software Engineering Conference and Symposium on the Foundations of Software Engineering},
  pages={200--211},
  year={2019}
}
```


## 2. Project Organization

The **failure dataset** includes the raw logs from fault injection experiments in OpenStack. The tests are grouped per injected sub-system (i.e., Nova, Cinder, and Neutron). 

There is a total of 911 tests: 439 for Nova, 269 for Cinder, and 203 for Neutron. The logs of each experiment are saved in a folder named "`Test_id`", where "`id`" is an incremental number that identifies the test. 

The files "`cinder.tsv`", "`neutron.tsv`" and "`nova.tsv`" are tsv file containing the failure analysis of the experiments. The csv files consist of three fields: 

*  **Test**: It is the name of the folder that contains the specific test;
*  **Fault_Type**: It is the type of the injected fault from the list described in the paper;
*  **Component**: It is the name of the source code file to be mutated;
*  **Class**: It is the name of the class which contains the mutated statement;
*  **Function**: It is the name of the function which contains the mutated statement;
*  **Fault_Point**: It is the target statement;
*  **Round_1** is "FAILURE" if the experiment failed in the faulty round, "NO_FAILURE" otherwise;
*  **Assertion_R1**: if it exists, this field contains the assertion failure during the faulty round;
*  **API_R1**: if it exists, this field contains the api error occurred during the faulty round;
*  **Round_2** is "FAILURE" if the experiment failed in the fault-free round, "NO_FAILURE" otherwise;
*  **Assertion_R2**: if it exists, this field contains the assertion failure during the fault-free round;
*  **API_R2**: if it exists, this field contains the api error occurred during the fault-free round.



In this [Github repository](https://github.com/dessertlab/OpenStack-Fault-Injection-Environment) you can find the tools to reproduce these experiments.


### 2.1 Structure of the test folders

Every test folder contains the following files:
* "`fp_info.data`": It contains information about the fault injected in the experiment (including the fault type, the target component, the target class, the target function, and the fault injection point);
* "`orig_file`": It contains the target component before the mutation;
* "`mutated_file`": It contains the target component after the mutation;
* "`diff`": It is the diff file between the orig_file and mutated_file;




The subfolder "`Test_<id>/logs`" contains the raw logs of the executions of both the faulty round ("`round_1`" subfolder) and the fault-free round ("`round_2`" subfolder).

In each round subfolder, there are more subfolders representing different sub-systems of OpenStack (e.g., "`nova`", "`cinder`", "`neutron`", "`glance`", etc.) containing the log messages generated during the tests.

For example, the directory "`Nova/Test_1/logs/round_1/cinder`" contains the log messages from the Cinder sub-system during the faulty execution of "Test 1", from the fault injection campaign on the Nova sub-system. 

Furthermore, for each round, there is the "`foreground_wl`" subfolder containing the log files of the workload:

* `openstack_demo_workload-timestamp.out.log.bzip2.out` (contains the log messages of the workload execution)

* `openstack_demo_workload-timestamp.err.log.bzip2.out` (contains the error messages during the workload execution, including both API Errors and Assertion Failures).

Each subfolder "`Test_<id>/logs/round_number`" contains also the file "`trace_Test_<id>_round_number`". This file is a JSON file containing all the messages exchanged in OpenStack during the execution of the workload. These messages are collected with the distributed tracing system [Zipkin](https://zipkin.io/). For further details about the information collected, please refer to the paper [Enhancing Failure Propagation Analysis in Cloud Computing Systems](https://ieeexplore.ieee.org/document/8987476).

Finally, in the subfolder "`Test_<id>/logs/round_1`", you can find the file "`trigger_log`" containing the timestamp of the fault activation during the workload execution.
