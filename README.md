# utl-very-simple-export-and-import-for-csv-files-in-the-classic-l980s-sas-dms-editor
Very simple export and import for csv files in the classic 1080s sas dms editor
    %let pgm=utl-very-simple-export-and-import-for-csv-files-in-the-classic-l980s-sas-dms-editor;

    Very simple export and import for csv files in the classic 1080s sas dms editor

    github
    https://tinyurl.com/3zdh4a27
    https://github.com/rogerjdeangelis/utl-very-simple-export-and-import-for-csv-files-in-the-classic-l980s-sas-dms-editor

    Note other file types supported (also works on clssic command line

    dm "dexport sashelp.class 'c:\temp\tmp.csv' replace";
    dm "dimport 'c:\temp\tmp.csv' class  replace";

    /*
    | | ___   __ _ ___
    | |/ _ \ / _` / __|
    | | (_) | (_| \__ \
    |_|\___/ \__, |___/
             |___/
      _____  ___ __   ___  _ __| |_
     / _ \ \/ / `_ \ / _ \| `__| __|
    |  __/>  <| |_) | (_) | |  | |_
     \___/_/\_\ .__/ \___/|_|   \__|
              |_|
    */

    dm "dexport sashelp.class 'c:\temp\tmp.csv' replace";


        data _null_;
        %let _EFIERR_ = 0; /* set the ERROR detection macro variable */
        %let _EFIREC_ = 0;     /* clear export record count macro variable */
        file 'c:\temp\tmp.csv' delimiter=',' DSD DROPOVER lrecl=32767;
        if _n_ = 1 then        /* write column names or labels */
         do;
           put
              "NAME"
           ','
              "SEX"
           ','
              "AGE"
           ','
              "HEIGHT"
           ','
              "WEIGHT"
           ;
         end;
       set  SASHELP.CLASS   end=EFIEOD;
           format NAME $8. ;
           format SEX $1. ;
           format AGE best12. ;
           format HEIGHT best12. ;
           format WEIGHT best12. ;
         do;
           EFIOUT + 1;
           put NAME $ @;
           put SEX $ @;
           put AGE @;
           put HEIGHT @;
           put WEIGHT ;
           ;
         end;
        if _ERROR_ then call symputx('_EFIERR_',1);  /* set ERROR detection macro variable */
        if EFIEOD then call symputx('_EFIREC_',EFIOUT);
        run;

    /*                            _
    (_)_ __ ___  _ __   ___  _ __| |_
    | | `_ ` _ \| `_ \ / _ \| `__| __|
    | | | | | | | |_) | (_) | |  | |_
    |_|_| |_| |_| .__/ \___/|_|   \__|
                |_|
    */

    dm "dimport 'c:\temp\tmp.csv' class  replace";

        data WORK.CLASS    ;
        %let _EFIERR_ = 0; /* set the ERROR detection macro variable */
        infile 'c:\temp\tmp.csv' delimiter = ',' MISSOVER DSD lrecl=384 firstobs=2 ;
           informat NAME $7. ;
           informat SEX $1. ;
           informat AGE best32. ;
           informat HEIGHT best32. ;
           informat WEIGHT best32. ;
           format NAME $7. ;
           format SEX $1. ;
           format AGE best12. ;
           format HEIGHT best12. ;
           format WEIGHT best12. ;
        input
                    NAME  $
                    SEX  $
                    AGE
                    HEIGHT
                    WEIGHT
        ;
        if _ERROR_ then call symputx('_EFIERR_',1);  /* set ERROR detection macro variable */
        run;

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
