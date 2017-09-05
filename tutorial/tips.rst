====
Tips
====

* Work in pairs!


rtlwifi
-------

Tips after working through track two.

* Save the output of checkpatch so you don't have to wait for it to run repeatedly.

* grepfoo 

.. code: bash
      
   cat ~/scratch/checkpatch.out | grep WARNING | grep -v 'line over 80' 
 
* Don't do band aid fixes. Fix the root of the problem.

.. code: bash
     
   pci.c:1574: CHECK:PARENTHESIS_ALIGNMENT: Alignment should match open parenthesis
  
  The root problem is that the code is indented too heavily. Function needs refactoring not
  alignment fixing.

* Feel free to mildly violate line over 80 if it makes the code more readable.

.. code: bash
     
   efuse.c:255: WARNING:ALLOC_WITH_MULTIPLY: Prefer kcalloc over kzalloc with multiply
   efuse.c:259: WARNING:ALLOC_WITH_MULTIPLY: Prefer kcalloc over kzalloc with multiply


.. code: bash   

     for (i = 0; i < EFUSE_MAX_WORD_UNIT; i++) {
             efuse_word[i] = kcalloc(efuse_max_section, sizeof(u16), GFP_ATOMIC);
             if (!efuse_word[i])
                     goto done;
     }

* Look up kernel identifiers at free-electrons_

.. _free-electrons: http://elixir.free-electrons.com/linux/latest/ident

  
