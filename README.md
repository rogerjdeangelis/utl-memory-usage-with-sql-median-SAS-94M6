# utl-memory-usage-with-sql-median-SAS-94M6
SAS Memory usage with sql median
    SAS Memory usage with sql median

    github
    https://tinyurl.com/vftophh
    https://github.com/rogerjdeangelis/utl-memory-usage-with-sql-median-SAS-94M6

    Note the growth in OS memory when running the same code repeatedly?

    Loop
    Number   OS Memory (mb)

       1       20,604 mb     (this is total and includes non SAS processes in background)
    1000    1,156,632 mb     ( it is the differnce that is important)


    Growth  1,136,028 mb =  1156632 - 20604

    Ran ok on my laptop in 11 seconds  ( I have 16gb on my Dell E7 6420 - may be an issue in EG VM with only 1gb ram)

    Not sure at what point SAS decides to clear the windows OS memory cache.

    SAS Forum
    https://communities.sas.com/t5/SAS-Programming/SQL-Memory-Usage/m-p/627688

    *
     _ __  _ __ ___   ___ ___  ___ ___
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    ;


    %utlopts;  * turn everthong off;

    %let beg=%sysfunc(time());

    %macro loop(n);
          %do i = 1 %to &n.;
                proc sql;
                      create table out as select
                      median(AgeCHDdiag)
                      from sashelp.heart;
                quit;
          %end;
    %mend;

    %loop(1000);

    %let end=%sysfunc(time());

    %put %sysevalf(&end - &beg);

    Elapsed time 10.9050002097937

    WORK.OUT total obs=1

    bs    _TEMG001

    1        63

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;

    First Iteration

    NOTE: PROCEDURE SQL used (Total process time):
          real time           0.01 seconds
          user cpu time       0.00 seconds
          system cpu time     0.00 seconds
          memory              6666.06k

          OS Memory           20604.00k

          Timestamp           03/06/2020 12:57:28 PM
          Step Count                        16  Switch Count  0

    Last iteration

    NOTE: PROCEDURE SQL used (Total process time):
          real time           0.01 seconds
          user cpu time       0.00 seconds
          system cpu time     0.00 seconds
          memory              6551.31k

          OS Memory           1156632.00k

          Timestamp           03/06/2020 12:57:52 PM
          Step Count                        1015  Switch Count  0



