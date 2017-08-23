=========
Track One
=========

In this track we will be working on an old kernel. The patch series you create here will not be able
to be submitted to the kernel. The process, however, to do a real patch set is the same. See Track
Two if you would like to jump straight into doing a series that can be submitted to the kernel.

1. Set up the tree
------------------

 	KERNEL=path/to/gregKH/staging/tree
   
 - Check out the 4.9 kernel

   	git checkout -b tutorial 69973b8

 - Verify the following (`grep FOO $KERNEL/.config`)

   	CONFIG_STAGING=y
   	CONFIG_KS7010=m

 - Verify the ks7010 module builds (see shell-utils.sh).

  	$ make -j9 M=drivers/staging/ks7010
        
2. Checkpatch
-------------

 - You may like to define a shell alias

	alias checkpatch="$KERNEL/scripts/checkpatch.pl -f"

 - Run `checkpatch` on the C source files in the ks7010 driver
        
  	checkpatch --terse --strict --show-types drivers/staging/ks7010/*.c

 - Pick 3 types of warnings to fix. (All checkpatch output CHECK/WARNING/ERROR referred to as warnings).

 - Typically you would fix all instances of a warning type in a single patch. For the sake of
   brevity you may prefer to just fix a few of them.

 - Write a thorough, descriptive commit log. You may like to read

        Documentation/process/submitting-patches.rst (Section 2 - Describe your changes)

 - Here is an example git log for a simple checkpatch fix.
        
	staging: ks7010: remove unnecessary parenthesis

	Checkpatch emits CHECK: Unnecessary parentheses.

	Remove unnecessary parentheses.

 - Build the module. All patches to the kernel must build cleanly. This means every patch within a
   series must build cleanly, not just the last one.

 - Repeat for the other two warning types you picked.

3. Patch Set
------------
    
By this stage you should have three commits in your git index, each fixing a specific 'warning'
type. Each commit is described fully in the commit log and each commit builds cleanly.

 - Read through the diff of all three commits checking for any mistakes.

  	git log --color=always --patch --reverse HEAD~~~.. | less

 - Now use git to output a patch series

	git format-patch -3 -o path/to/patch/dir --cover-letter

 - Write the cover letter. For a simple series like this a brief sentence describing the series will
   suffice.

 - Email the patch set to your self. This is a useful step when getting started so you can verify
   that everything looks good.

Now (in Real Life) you would email this patch set to the device driver mailing list. Well done. Now
(or later) you can repeat this process on top of the current staging-next branch and submit your
first patch set to the Linux kernel (see Track Two for more specifics).
  