# utl-saving-repairing-listing-and-restoring-sas-classic-editor-function-keys
Saving repairing listing and restoring sas classic editor function keys
    %let pgm=utl-saving-repairing-listing-and-restoring-sas-classic-editor-function-keys;

    Saving repairing listing and restoring sas classic editor function keys

    I have tried to edit the sasuser.profile.keys programatically but the
    catalog entry is very complex?

     What you can and cannot do with function keys

       1 Restoring function keys from another catalog
       2 Listing your function keys
       3 Repair profile
       4 SOAPBOX what used to work
       5 my keys (tied to command macros and mouse actions)
       6 related repos

    github
    https://tinyurl.com/wsx32x4k
    https://github.com/rogerjdeangelis/utl-saving-repairing-listing-and-restoring-sas-classic-editor-function-keys

    /*                 _                   _
    / |  _ __ ___  ___| |_ ___  _ __ ___  | | _____ _   _ ___
    | | | `__/ _ \/ __| __/ _ \| `__/ _ \ | |/ / _ \ | | / __|
    | | | | |  __/\__ \ || (_) | | |  __/ |   <  __/ |_| \__ \
    |_| |_|  \___||___/\__\___/|_|  \___| |_|\_\___|\__, |___/
                                                    |___/
    */

    Restoring a copy of you function keys from another catalog

    If you are using the classic editor, go to the
    keys window and
    type (untested code but I used to do this)

    copy backup.profile.keys

    Or

    proc catalog cat=sasuser.profile;
    copy out=work.profile;
      select  dmkeys.keys ;
    run;quit;

    * delete keys;
    proc catalog cat=sasuser.profile;
      delete dmkeys.keys;
    run;quit;

    /*___    _ _     _     _
    |___ \  | (_)___| |_  | | _____ _   _ ___
      __) | | | / __| __| | |/ / _ \ | | / __|
     / __/  | | \__ \ |_  |   <  __/ |_| \__ \
    |_____| |_|_|___/\__| |_|\_\___|\__, |___/
                                    |___/
    */

    Saving a list of your function keys

    filename key catalog "sasuser.profile.dmkeys.keys";
    data key;
      length key $8 val $132;
      infile key dlm='09'x;
      input;
      if _n_>1;
      key=compress(_infile_,'09'x);
      if compress(key)='F10' then stop;
      input;
      val=_infile_;
      output;
    run;
    proc print data=key;
    run;

    /*____                        _        _
    |___ /   _ __ ___ _ __   __ _(_)_ __  | | _____ _   _ ___
      |_ \  | `__/ _ \ `_ \ / _` | | `__| | |/ / _ \ | | / __|
     ___) | | | |  __/ |_) | (_| | | |    |   <  __/ |_| \__ \
    |____/  |_|  \___| .__/ \__,_|_|_|    |_|\_\___|\__, |___/
                     |_|                            |___/
    */
    libanme etc "c:/etc";   /* has to a backup catalog with your keys */
    proc datasets lib=etc;
    repair profile;
    run;quit;

    /*  _                           _                                    _  _                             _
    | || |    ___  ___   __ _ _ __ | |__   _____  __  _   _ ___  ___  __| || |_ ___   __      _____  _ __| | __
    | || |_  / __|/ _ \ / _` | `_ \| `_ \ / _ \ \/ / | | | / __|/ _ \/ _` || __/ _ \  \ \ /\ / / _ \| `__| |/ /
    |__   _| \__ \ (_) | (_| | |_) | |_) | (_) >  <  | |_| \__ \  __/ (_| || || (_) |  \ V  V / (_) | |  |   <
       |_|   |___/\___/ \__,_| .__/|_.__/ \___/_/\_\  \__,_|___/\___|\__,_| \__\___/    \_/\_/ \___/|_|  |_|\_\
                           _ |_|
     ___  ___   __ _ _ __ | |__   _____  __   ___  _ __
    / __|/ _ \ / _` | `_ \| `_ \ / _ \ \/ /  / _ \| `_ \
    \__ \ (_) | (_| | |_) | |_) | (_) >  <  | (_) | | | |
    |___/\___/ \__,_| .__/|_.__/ \___/_/\_\  \___/|_| |_|
                    |_|
    */

    Unfortunately, over the years SAS has removed functionality
    from the classic editor. I have asked for the
    functinality to be brought back, but to no avail.
    I have even annoyed 'enhanced' editor developers.
    Maybe object oriented programming and the conversion of
    SAS to C had limitations or made a the development
    of powerfull editors too dificult?

    Back in the day these commands work but no longer does

    Some of the missing functionality

    tf ts - work intermittantly
    when sas allowed the ibm ISPF you could use
    mnay usefull prefix commands
    xx
    x
    flip
    cursor (very important gets postion of cursor - ISPF also had templates)

    over the years sas has removed functionality for the classic edito

    dm "keydef  F7 'vt _last_'";
    no longer supported

    %KEYDEF F7 'conx';
    NOTE: %KEYDEF is obsolete in this version of the SAS System.

    dm 'wedit "keydef F7 clear"'
    dm "wdedit 'keydef  ''F7'' vt _last_;edit ' wedit";

    no longer supported

    dm 'keydef  "CTL G"    "filename"';               run;quit;
    dm 'keydef  "CTL H"    "note H.H"';               run;quit;
    dm 'keydef  "CTL I"    "note I.I"';               run;quit;
    dm 'keydef  "CTL J"    "~c:\oto\IML XMPL utliml1..3 utlimlab met_t_arcsin"';   run;quit;
    dm 'keydef  "CTL K"    ":ucl"';    run;quit;
    dm 'keydef  "CTL L"    ":mcl"';    run;quit;
    dm 'keydef  "CTL M"    "~PROC FORMAT;VALUE $A;PROC CATALOG CAT=WORK.FORMATS;MODIFY A.FORMATC(DESC=DEA);"';          run;quit;
    dm 'keydef  "CTL Q"    "~PROC TABULATE DATA=CLASS;CLASS SEX AGE;TABLE AGE,SEX*(N PCTN<AGE>)/RTS=8"';                run;quit;
    dm 'keydef  "CTL R"    "~redo"';   run;quit;
    dm 'keydef  "CTL T"    "~CREATE TABLE D(S INT,T DATE);INSERT INTO D VALUES(1,01JAN99 D)"';    run;quit;
    dm 'keydef  "CTL U"    "~update s as m set x=(select x from c as h where s.n=h.n)"';          run;quit;
    dm 'keydef  "CTL W"    "~where exists (select 1 from c as h where m.x is null and s.n=h.n)"'; run;quit;
    dm 'keydef  "CTL Y"    "~****** assign as needed ******"';              run;quit;
    dm "keydef  'F3'       'left 3'";  run;quit;
    dm "keydef  'F4'       'right 3'";                run;quit;
    dm "keydef  'F5'       'end'";     run;quit;
    dm "keydef  'F6'       'log'";     run;quit;
    dm "keydef  'F7'       'out'";     run;quit;
    dm "keydef  'F8'       'rfind'";   run;quit;
    dm "keydef  'F9'       'rchange'";                run;quit;
    dm "keydef  'F10'      'redo'";    run;quit;
    dm 'keydef  "F1"       "%nrstr(pgm;file &pgm..sas;file c:\ver\&pgm.&_q..sas;%let _q=%eval(0&_q +1);)"';             run;quit;
    dm "keydef  'SHF F1'   'note;notesubmit ''%nrstr(%unxcon;)''' " ;       run;quit;
    dm "keydef  'CTL F1'   'store;note;notesubmit ''%nrstr(%uxpcon;)''' " ; run;quit;
    dm "keydef  'ALT F1'   'store;home;paste'";       run;quit;
    dm "keydef  'RMB'      'log;clear;out;clear;pgm;submit;rec;home;log;'" ;run;quit;
    dm "keydef  'SHF RMB'  'note;notesubmit ''%nrstr(%last;)'' " ;          run;quit;
    dm "keydef  'CTL RMB'  'store;note;notesubmit ''%nrstr(%uxp;)'' ";      run;quit;
    dm "keydef  'SHF F2'   'note;notesubmit ''%nrstr(%lastall;)''' " ;      run;quit;
    dm "keydef  'CTL F2'   'store;note;notesubmit ''%nrstr(%uxpall;)''' " ; run;quit;
    dm "keydef  'ALT F2'   'wattention;'";            run;quit;
    dm "keydef  'ALT F3'   '%nrstr(~dountil last.x;set x;by x;z+w;;end;s=z;dountil last.x;set x;by x;otpt;end;z=0)'";   run;quit;
    dm "keydef  'F11'      '~run;quit;'";             run;quit;
    dm "keydef  'SHF F11'  'vt _last_ colnames=names'";      run;quit;
    dm "keydef  'CTL F11'  'store;note;notesubmit ''%nrstr(%viewt;)''' " ;  run;quit;
    dm "keydef  'ALT F11'  'libn;'";   run;quit;
    dm "keydef  'F12'      'dir work;'";              run;quit;
    dm "keydef  'SHF F12'  'store;note;notesubmit ''%nrstr(%snx;)''' " ;    run;quit;
    dm 'keydef  "CTL F12"  "%nrstr(log;file c:\utl\&pgm..log ;note zx;notesubmit ''%utl_logchk(c:\utl\&pgm..log));'')"';run;quit;;
    dm "keydef  'ALT F12'  'inc c:\oto\box.sas'";     run;quit;
    dm "keydef  'CTL B'    '~data;infile in recfm=n;file ot recfm=n;input b $char1. @@;put b $char1. @@;' " ;           run;quit;
    dm "keydef  'CTL D'    'note;notesubmit ''%nrstr(%dmp;)'' " ;           run;quit;
    dm "keydef  'CTL E'    'store;note;notesubmit ''%nrstr(%dmph;)'' ";     run;quit;
    dm "keydef  'SHF F6'   '%nrstr(~macro a(x);%if %sysfunc(ifc(%sysevalf(%superq(x)=,boolean),1,0)) = 0 %then %do)'" ; run;quit;
    dm "keydef  'SHF F7'   'keys' " ;  run;quit;
    dm "keydef  'SHF F8'   '~proc report data=c nowd named list wrap;columns _all_;run;quit;' " ; run;quit;
    dm "keydef  'SHF F9'   '%nrstr(~options minoperator;^macro t(x=a)/minoperator;^if @x in (a b c) ^then)'" ;          run;quit;
    dm "keydef  'SHF F10'  '~style={cellwidth=32pct  just=c pretext= \qj\tqdec\tx500 }'" ;        run;quit;
    dm "keydef  'CTL F3'   '~%nrstr(%substr(%sysfunc(putn(%sysfunc(datetime()),datetime22.)),1,15))'";   run;quit;
    /*                     _                        __  __
     ___  ___   __ _ _ __ | |__   _____  __   ___  / _|/ _|
    / __|/ _ \ / _` | `_ \| `_ \ / _ \ \/ /  / _ \| |_| |_
    \__ \ (_) | (_| | |_) | |_) | (_) >  <  | (_) |  _|  _|
    |___/\___/ \__,_| .__/|_.__/ \___/_/\_\  \___/|_| |_|
                    |_|
    */

    /*___                      _
    | ___|   _ __ ___  _   _  | | _____ _   _ ___
    |___ \  | `_ ` _ \| | | | | |/ / _ \ | | / __|
     ___) | | | | | | | |_| | |   <  __/ |_| \__ \
    |____/  |_| |_| |_|\__, | |_|\_\___|\__, |___/
                       |___/            |___/
    */

    see sas.saspac.sas in

    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories
    Mappings for G\logitech G-502 Hero mouse


                    _______________________________
                    /                               \              _____________
                   /             TOP VIEW            \            /             \
                  /   Can use with SHF CTL & ALT      \          /               \
                 /                                     \        /  SIDE VIEW      \
                |                                       |      /                   \
                |                            ___        |     |                     |
                |                           /   \       |     |    ___              |
                |                          | RMB |      |     |   /   \             |
                |                           \___/       |     |  | F11 |            |
                |                   SAS direct mapping  |     |   \___/             -\
                |                                       |     |        Scroll Wheel - |
                |                                       |     |           ___       - /
                |                                       |     |          /   \      |/
                |                                       |     |         | F5  |     |
                |    ___                                |     |          \___/      |
                |   /   \                               |     |                     |
                |  | F11 |                              |     |    ___              |
                |   \___/                               |     |   /   \             |
                |                                       |     |  | F4  |            |
                |           ___       ___      ___      |     |   \___/             |
                |          /   \     /   \    /   \     |     |                     |
                |         | F5  |   | F1  |  | F6  |    |      \                    /
                |          \___/     \___/    \___/     |       \                  /
                |                                       |        \                /
                |    ___                                |         \              /
                |   /   \                               |          \____________/
                |  | F4  |                              |
                |   \___/                               |
                |                     ___               |
                |                    /   \              |
                |                   | F2  |             |
                |                    \___/              |
                 \                                      /
                  \                                    /
                   \                                  /
                    \                                /
                     \______________________________/


    Note most of these call autocall command macros in my autocall library
    d:/oto  (several hundred autocall performance macros

    bs    KEY        VAL

     1    F1         _sv
     2    F2         home;copy cmt;
     3    F3         ~run;quit;
     4    F4         notesubmit;
     5    F5         conh
     6    F6         dmph
     7    F7         con
     8    F8         rfind
     9    F9         rchange
    10    F11        sumv
    11    F12        ~;;;;%end;%mend;/*'*/ *);*};*];*/;/*"*/;run;quit;%end;end;run;endcomp;%utlfix;
    12    SHF F1     lsa
    13    SHF F2     unvh
    14    SHF F6     ~proc datasets lib=sd1 nolist mt=data mt=view nodetails;delete want; run;quit;
    15    SHF F7     log;file "c:\log\&pgm..log";note z;notesubmit '%utl_logcurchk;';
    16    SHF F8     lsh
    17    SHF F9     avgh
    18    SHF F10    debugh
    19    SHF F11    lsfh
    20    SHF F12    parh
    21    CTL F1     lsah
    22    CTL F2     cuth
    23    CTL F3     sqldesh
    24    CTL F11    evlh
    25    CTL F12    tail
    26    ALT F1     rpth
    27    ALT F2     xlrh
    28    ALT F3     sasbatch
    29    ALT F11    unvh
    30    ALT F12    tailh
    31    CTL B      wattention
    32    CTL D      ~proc tabulate;var a b;table a(n)*f=5.*b(n)*f=5.;run;
    33    CTL E      ~n ? "hil";n=*"P Jone";n gt:"Phil";n le "Eva";sql- eqt gtt ltt get let net
    34    CTL G      note g.g;home;resize;
    35    CTL H      note h.h;home;resize
    36    CTL I      note i.i;home;resize
    37    CTL J      ~/*----                                                                   ----*/
    38    CTL K      :mcu
    39    CTL L      :mcl
    40    CTL M      ~proc format;value $a;proc catalog cat=formats;modify a.formatc(desc='OK');run;
    41    CTL Q      ~options minoperator;%macro t(x=a)/minoperator;%if &x in (a b c) %then
    42    CTL R      ~proc report data=sashelp.class named list wrap;run;quit;
    43    CTL T      ~proc tabulate data=class;class sex age;table age,sex*(n pctn<age>)/rts=8
    44    CTL U      xpad
    45    CTL W      ~x 'tree "c:/temp" /F /A | clip'
    46    CTL Y      ~where name like "B_B" "%B%" "B%B"
    47    RMB        log;clear;out;clear;pgm;submit;home;log;z;z;
    48    SHF RMB    ls4
    49    CTL RMB    lsh
    50    MMB        ~assigned to f1;
    51    SHF MMB    ~assigned to shf f1 lsa all obs last datasets
    52    CTL MMB    ~assigned to cnt fl ldah all obs highlighed dataset

    /*__              _       _           _
     / /_    _ __ ___| | __ _| |_ ___  __| |  _ __ ___ _ __   ___  ___
    | `_ \  | `__/ _ \ |/ _` | __/ _ \/ _` | | `__/ _ \ `_ \ / _ \/ __|
    | (_) | | | |  __/ | (_| | ||  __/ (_| | | | |  __/ |_) | (_) \__ \
     \___/  |_|  \___|_|\__,_|\__\___|\__,_| |_|  \___| .__/ \___/|___/
                                                      |_|
    */

    REPO
    -------------------------------------------------------------------------------------------------------------------------------

    https://github.com/rogerjdeangelis/utl_sas-classic-editor-point-and-shoot-a-proc-freq
    https://github.com/rogerjdeangelis/utl_sas_classic_editor
    https://github.com/rogerjdeangelis/utl_soapbox_001_classic_sas_and_the_programmer
    https://github.com/rogerjdeangelis/utl-how-to-set-up-the-classic-1980s-classic-editor
    https://github.com/rogerjdeangelis/utl-sas-classic-editor-function-keys-for-comment

    https://github.com/rogerjdeangelis/utl-setting-your-classic-editor-dms-function-keys-mouse-actions-and-command-line
    https://github.com/rogerjdeangelis/utl_classic_editor_pfkeys_prefix_mouse
    https://github.com/rogerjdeangelis/utl_performance_package_SAS_classic_editor
    https://github.com/rogerjdeangelis/Creating-command-macros-for-the_1980s-DMS-Classic-Editor
    https://github.com/rogerjdeangelis/utl-are-classic-editor-command-macros-fsview-and-fsedit-more-useful-than-viewtable
    https://github.com/rogerjdeangelis/utl-classic-editor-comment-out-a-block-of-text
    https://github.com/rogerjdeangelis/utl-classic-editor-commnand-macro-to-repair-sas-satement-with-uunbalanced-quotes
    https://github.com/rogerjdeangelis/utl-comment-out-a-block-og-code-in-the-classic-1980s-dms-editor
    https://github.com/rogerjdeangelis/utl-how-to-set-up-the-classic-1980s-classic-editor
    https://github.com/rogerjdeangelis/utl-latest-command-macros-for-the-sas-classic-editor
    https://github.com/rogerjdeangelis/utl-location-of-program-folder-and-classic-editor-program-versioning
    https://github.com/rogerjdeangelis/utl-never-lose-your-program-poor-mans-version-control-using-the-classic-l980s-sas-editor
    https://github.com/rogerjdeangelis/utl-repairing-the-calssic-l980s-display-manager-editor
    https://github.com/rogerjdeangelis/utl-sas-classic-editor-function-keys-for-comments
    https://github.com/rogerjdeangelis/utl-sas-scripting-commands-only-available-in-the_1980s-classic-editor
    https://github.com/rogerjdeangelis/utl-setting-the-path-of-the-executing-program-in-the-1980s-sas-editor
    https://github.com/rogerjdeangelis/utl-setting-your-classic-editor-dms-function-keys-mouse-actions-and-command-line
    https://github.com/rogerjdeangelis/utl-setup-notepad--editor-for-use-with-wps-altair-sas
    https://github.com/rogerjdeangelis/utl-spell-check-words-in-any-classic-editor-window-ie-pgm-note-log-output
    https://github.com/rogerjdeangelis/utl-trimming-padded-lines-in-the-classic-editor
    https://github.com/rogerjdeangelis/utl-very-simple-export-and-import-for-csv-files-in-the-classic-l980s-sas-dms-editor
    https://github.com/rogerjdeangelis/utl_classic_editor_command_macro_performance_package
    https://github.com/rogerjdeangelis/utl_classic_editor_hilite_and_evaluate_math_functions
    https://github.com/rogerjdeangelis/utl_classic_editor_keyboard_macros_and_abbreviations
    https://github.com/rogerjdeangelis/utl_classic_editor_part_II
    https://github.com/rogerjdeangelis/utl_classic_editor_pfkeys_prefix_mouse
    https://github.com/rogerjdeangelis/utl_classic_editor_place_comment_box_at_cursor_location_with_single_keystroke
    https://github.com/rogerjdeangelis/utl_classic_editor_programatic_cursor_positioning_with_store_cut_and_paste
    https://github.com/rogerjdeangelis/utl_classic_editor_seemless_connection_workstation_unix_server
    https://github.com/rogerjdeangelis/utl_classic_editor_using_a_prefix_mask_to_facilitate_fixed_column_data_entry
    https://github.com/rogerjdeangelis/utl_classic_sas_editor_display_manager_commands_improved
    https://github.com/rogerjdeangelis/utl_fun_with_line_printer_graphics_editor
    https://github.com/rogerjdeangelis/utl_performance_package_SAS_classic_editor
    https://github.com/rogerjdeangelis/utl_sas-classic-editor-point-and-shoot-a-proc-freq
    https://github.com/rogerjdeangelis/utl_sas_classic_editor


    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
