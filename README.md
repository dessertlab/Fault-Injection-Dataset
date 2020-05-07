# README


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


## Dataset Description
The **failure dataset** includes the raw logs from fault injection experiments in OpenStack. The tests are grouped per injected sub-system (i.e., Nova, Cinder, and Neutron). 

There is a total of 480 tests: 231 for Nova, 125 for Cinder, and 124 for Neutron. The log of each experiment is saved in a folder named "Test_id", where "id" is an incremental number that identifies the test. See the `README.txt` file in the `dataset` directory for more details about the dataset. 
