## 1. Dataset Description


This failure dataset contains the injected faults, the workload, the effects of failure (both the user-side impact and our own in-depth correctness checks), and the error logs produced by the OpenStack cloud management system.
Please refers to the paper "`How Bad Can a Bug Get? An Empirical Analysis of Software Failures in the OpenStack Cloud Computing Platform`" accepted for presentation at the ESEC-FSE 2019 conference (doi>` 10.1145/3338906.3338916`). 

Please, **cite the paper** if you use the tools for your research:

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

There is a total of 911 tests: 439 for Nova, 269 for Cinder, and 203 for Neutron. The log of each experiment is saved in a folder named "`Test_id`", where "`id`" is an incremental number that identifies the test. 


### 2.1 Structure of the test folders

Every test folder contains the file "`fp_info.data`", which contains information about the fault injected in the experiment (including the fault type, the target component, the target class, the target function, and the fault injection point).

The subfolder "`Test_<id>`"/logs contains the raw logs of the executions of both the faulty round ("`round_1`" subfolder) and the fault-free round ("`round_2`" subfolder).

In each round subfolder, there are more subfolders representing different sub-systems of OpenStack (e.g., "`nova`", "`cinder`", "`neutron`", "`glance`", etc.) containing the log messages generated during the tests.

For example, the directory "`Nova/Test_1/logs/round_1/cinder`" contains the log messages from the Cinder sub-system during the faulty execution of "Test 1", from the fault injection campaign on the Nova sub-system. 

Furthermore, for each round, there is the "`foreground_wl`" subfolder containing the log files of the workload:

* `openstack_demo_workload-timestamp.out.log.bzip2.out` (contains the log messages of the workload execution)

* `openstack_demo_workload-timestamp.err.log.bzip2.out` (contains the error messages during the workload execution, including both API Errors and Assertion Failures).
