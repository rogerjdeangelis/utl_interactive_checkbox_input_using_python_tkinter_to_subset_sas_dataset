# utl_interactive_checkbox_input_using_python_tkinter_to_subset_sas_dataset
Interactive checkbox input using Python Tkinter to subset SAS dataset. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Interactive checkbox input using Python Tkinter to subset SAS dataset

    The Tkinter packages is part of Python 2.7.
    No need to install anything.

    If you click on the Female checkbox then SAS will print
    the female students in table sashelp.class.

    Tkinter returns a SAS macro variable &sex selected using the interactive checkbox
    
    HAVE sashelp.class dataset
    ==========================

        Up to 40 obs from sashelp.class total obs=19

        Obs    NAME       SEX    AGE    HEIGHT    WEIGHT

          1    Alfred      M      14     69.0      112.5
          2    Alice       F      13     56.5       84.0
          3    Barbara     F      13     65.3       98.0
        ...
         18    Thomas      M      11     57.5       85.0
         19    William     M      15     66.5      112.0


    WORKING CODE
    ============

        def var_states():;
        .   print("male: %d,\nfemale: %d" % (var1.get(), var2.get()));
        Label(master, text="Your sex:").grid(row=0, sticky=W);
        var1 = IntVar();
        Checkbutton(master, text="male", variable=var1).grid(row=1, sticky=W);
        var2 = IntVar();
        Checkbutton(master, text="female", variable=var2).grid(row=2, sticky=W);
        Button(master, text="Quit", command=master.quit).grid(row=3, sticky=W, pady=4);
        Button(master, text="Show", command=var_states).grid(row=4, sticky=W, pady=4);
        mainloop();
        if var1.get() :;
        .    frompy="M";
        elif var2.get() :;
        .    frompy="F";
        else:;
        .    frompy="";
        pyperclip.copy(frompy);


    WANT (Interactive checkbox. I can select males or females from sashelp.class)
    =============================================================================

        +---+---------------+
        |   |  --   []  [X] |
        +---+---------------+
        |                   |
        |  Your Sex:        |
        |                   |
        |  +---+            |
        |  |   |  Male      |
        |  +---+            |
        |                   |
        |  +---+            |
        |  |   |  Female    |
        |  +---+            |
        |                   |
        |  [show]           |
        |                   |
        |  [quit]           |
        |                   |
        +-------------------+

    OUTPUT
    ======

        sashelp.class(where=(sex=F))

        Obs    NAME       SEX    AGE    HEIGHT    WEIGHT

          2    Alice       F      13     56.5       84.0
          3    Barbara     F      13     65.3       98.0
          4    Carol       F      14     62.8      102.5
          7    Jane        F      12     59.8       84.5
          8    Janet       F      15     62.5      112.5
         11    Joyce       F      11     51.3       50.5
         12    Judy        F      14     64.3       90.0
         13    Louise      F      12     56.3       77.0
         14    Mary        F      15     66.5      112.0




    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

     input to SAS is based on a checkbox

     also you need SASHELP.CLASS

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    Note the second argument to utl_submit_py64, return=sex.
    utl_submit_py64 will return a macro variable called sex with
    a M, F or mssing.

    %utl_submit_py64(resolve('
    from tkinter import *;
    import os;
    import pyperclip;
    master = Tk();
    def var_states():;
    .   print("male: %d,\nfemale: %d" % (var1.get(), var2.get()));
    Label(master, text="Your sex:").grid(row=0, sticky=W);
    var1 = IntVar();
    Checkbutton(master, text="male", variable=var1).grid(row=1, sticky=W);
    var2 = IntVar();
    Checkbutton(master, text="female", variable=var2).grid(row=2, sticky=W);
    Button(master, text="Quit", command=master.quit).grid(row=3, sticky=W, pady=4);
    Button(master, text="Show", command=var_states).grid(row=4, sticky=W, pady=4);
    mainloop();
    if var1.get() :;
    .    frompy="M";
    elif var2.get() :;
    .    frompy="F";
    else:;
    .    frompy="";
    pyperclip.copy(frompy);
    '),return=sex);

    data want;
       set sashelp.class(where=(sex="&sex"));
    run;quit;

    p to 40 obs WORK.WANT total obs=10

    bs    NAME       SEX    AGE    HEIGHT    WEIGHT

     1    Alfred      M      14     69.0      112.5
     2    Henry       M      14     63.5      102.5
     3    James       M      12     57.3       83.0
     4    Jeffrey     M      13     62.5       84.0
     5    John        M      12     59.0       99.5
     6    Philip      M      16     72.0      150.0
     7    Robert      M      12     64.8      128.0
     8    Ronald      M      15     67.0      133.0
     9    Thomas      M      11     57.5       85.0
    10    William     M      15     66.5      112.0


