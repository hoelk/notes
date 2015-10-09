UNIDO
#####

Indstat2
========


Tasks
-----

Now:

* Measures for Imputation
    * Mean square prediction error
    * Remove EMP, WS, OUT, VA from a year, impute, compare statistics (Visualize?)

Later:

* Minstat Imputation?
    * Report only released every second year
    * No IIP
    * No IMVA (~something similar exists)
    * Contains data at 2 and 3 digit level
* How stable is the structure of an isic branch (eg. the development of a single industrial branch)
* Amelia Cross section time series (lowest priority)


Shorthands
----------

* GO = OUT Gross Output
* VA Value Added
* EMP number of employees
* WS wages and salaries
* IIP Index of industrial production
* Index of Manufacturing Value Added
* CPI Consumer Price Index


Imputation Procedures
---------------------

.. digraph:: foo

    node [shape=egg]; EGO; EVA; EWS;
    node [shape=record];

    "IIP, CPI" -> "EGO";
    "VA, VA/GO" -> "EGO";
    "IMVA, CPI" -> "EGO";

    "GO, VA" -> "EVA";
    "VA, WS/VA" -> "EWS";
    "realVA, EMP/realVA" -> "EWS";
