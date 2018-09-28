# utl-encrypting-sas-datasets
Problem encrypt and operate on encrypted SAS datasets.  
    Problem encrypt and operate on encrypted SAS datasets

    Does not work in EG but does in the 1980s Classic SAS workstation?

    Workstation is more secure?

    github
    https://github.com/rogerjdeangelis/utl-encrypting-sas-datasets

    There are many reasons why a classic SAS workstation when off the net has less risk
    then the supposedly super secure EG servers?

    SAS Forum
    https://communities.sas.com/t5/SAS-Enterprise-Guide/Encrypt-in-data-step/m-p/499883

    INPUT
    =====

       sashelp.class


    EXAMPLE OUTPUT
    --------------

    ENCRYPTED CLASS DATASET

     The CONTENTS Procedure

    Data Set Name        WORK.CLASS                    Observations          19
    Member Type          DATA                          Variables             5
    Engine               V9                            Indexes               0
    Created              09/28/2018 11:55:28           Observation Length    40
    Last Modified        09/28/2018 11:55:28           Deleted Observations  0
    Protection                                         Compressed            NO
    Data Set Type                                      Sorted                NO

    Encrypted            AES    *** ENCRYPTED ****

    Label
    Data Representation  WINDOWS_64

    14    proc print data=work.class(encrypt=aes encryptkey=XXXXXXX);
    15    run;

    NOTE: There were 19 observations read from the data set WORK.CLASS.

       NAME       SEX    AGE    HEIGHT    WEIGHT

       Alfred      M      14     69.0      112.5
       Alice       F      13     56.5       84.0
       Barbara     F      13     65.3       98.0
       Carol       F      14     62.8      102.5
       Henry       M      14     63.5      102.5
       James       M      12     57.3       83.0
       Jane        F      12     59.8       84.5
     ....


    PROCESS
    =======

    data class(encrypt=aes encryptkey='green');
     set sashelp.class;
    run;quit;

    NOTE: If you lose or forget the ENCRYPTKEY, there will be no way to open the file and recover the data.
    NOTE: There were 19 observations read from the data set SASHELP.CLASS.
    NOTE: The data set WORK.CLASS has 19 observations and 5 variables.
    NOTE: DATA statement used (Total process time):
          real time           0.41 seconds
          cpu time            0.39 seconds


    proc contents data=class position(encrypt=aes encryptkey='green');
    run;quit;

    proc print data=class(obs=10 encrypt=aes encryptkey='green');
    run;quit;


    OUTPUT
    ======

    see above

