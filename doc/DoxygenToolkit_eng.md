
created by
Mathias Lorente
 
script type
utility
 
## description

Currently five purposes have been defined : 

* Generates a doxygen license comment.  The tag text is configurable. 

* Generates a doxygen author skeleton.  The tag text is configurable. 

* Generates a doxygen comment skeleton for a C, C++ or Python function or class, 
including @brief, @param (for each named argument), and @return.  The tag 
text as well as a comment block header and footer are configurable. 
(Consequently, you can have \brief, etc. if you wish, with little effort.) 

* Ignore code fragment placed in a block defined by #ifdef ... #endif (C/C++).  The 
block name must be given to the function.  All of the corresponding blocks 
in all the file will be treated and placed in a new block DOX_SKIP_BLOCK (or 
any other name that you have configured).  Then you have to update 
PREDEFINED value in your doxygen configuration file with correct block name. 
You also have to set ENABLE_PREPROCESSING to YES. 

* Generate a doxygen group (begining and ending). The tag text is 
configurable. 

## Use: 
- Type of comments (C/C++: /// or /** ... */, Python: ## and # ) : 
  In vim, default C++ comments are : /** ... */. But if you prefer to use /// 
  Doxygen comments just add 'let g:DoxygenToolkit_commentType = "C++"' 
  (without quotes) in your .vimrc file 

- License : 
  In vim, place the cursor on the line that will follow doxygen license 
  comment.  Then, execute the command :DoxLic.  This will generate license 
  comment and leave the cursor on the line just after. 

- Author : 
  In vim, place the cursor on the line that will follow doxygen author 
  comment.  Then, execute the command :DoxAuthor.  This will generate the 
  skeleton and leave the cursor just after @author tag if no variable 
  define it, or just after the skeleton. 

- Function / class comment : 
  In vim, place the cursor on the line of the function header (or returned 
  value of the function) or the class.  Then execute the command :Dox.  This 
  will generate the skeleton and leave the cursor after the @brief tag. 

- Ignore code fragment (C/C++ only) : 
  In vim, if you want to ignore all code fragment placed in a block such as : 

    #ifdef DEBUG 
    ... 
    #endif
 
  You only have to execute the command :DoxUndoc(DEBUG) ! 
   
- Group : 
  In vim, execute the command :DoxBlock to insert a doxygen block on the 
  following line. 

## Limitations: 
- Assumes that the function name (and the following opening parenthesis) is 
  at least on the third line after current cursor position. 
- Not able to update a comment block after it's been written. 
- Blocks delimiters (header and footer) are only included for function 
  comment. 
- Assumes that cindent is used. 
- Comments in function parameters (such as void foo(int bar /* ... */, baz)) 
  are not yet supported. 


##Example: 

     Given: 
    int 
      foo(char mychar, 
          int myint, 
          double* myarray, 
          int mask = DEFAULT) 
    { //... 
    } 

Issuing the :Dox command with the cursor on the function declaration would 
generate 


    /** 
    * @brief 
    * 
    * @param mychar 
    * @param myint 
    * @param myarray 
    * @param mask 
    * 
    * @return 
    */ 


To customize the output of the script, see the g:DoxygenToolkit_* 
variables in the script's source.  These variables can be set in your 
.vimrc. 

For example, my .vimrc contains: 

    let g:DoxygenToolkit_briefTag_pre="@Synopsis  " 
    let g:DoxygenToolkit_paramTag_pre="@Param " 
    let g:DoxygenToolkit_returnTag="@Returns   " 
    let g:DoxygenToolkit_blockHeader="--------------------------------------------------------------------------" 
    let g:DoxygenToolkit_blockFooter="----------------------------------------------------------------------------" 
    let g:DoxygenToolkit_authorName="Mathias Lorente" 
    let g:DoxygenToolkit_licenseTag="My own license"   <-- !!! Does not end with "\<enter>"
 
## install details
Copy to your '~/.vim/plugin' directory
