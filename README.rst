Operating System From Scratch
-----------------------------

Step 03: x86 Protect Mode
`````````````````````````

If our OS supports only one architecture, I'll choose x86.
You won't be surprised by this.
Now let's study how the cpu works and, most importantly, how x86 protect mode works.

We're going to write some code when learning protect mode.
Soon you'll find a 512-byte boot sector is too small for us.
My solution to this problem is to test our code in FreeDOS_:

1. compile the assembly code to COM format::

     $ nasm foo.asm -o foo.com

2. `create a new floppy image`_ (say ``pm.img``) and copy the COM file to it::

     $ sudo mount -o loop pm.img /mnt
     $ sudo cp foo.com /mnt
     $ sudo umount /mnt

4. run FreeDos::

     $ qemu-system-i386 -fda freedos.img -fdb pm.img

5. run our code::

     A:\>B:\foo.com

You can try the instructions above in directory ``b``.
Remember to replace ``foo.asm`` with the true source file name and unzip the image files first.

`‹prev`_   `next›`_

.. _FreeDos: http://www.freedos.org/
.. _`‹prev`: https://github.com/chenxiex/osfs02
.. _`next›`: https://github.com/chenxiex/osfs04
.. _`create a new floppy image`: https://github.com/chenxiex/osfs00/blob/qemu/Tips%26Tricks.md#%E5%A6%82%E4%BD%95%E5%88%9B%E5%BB%BA%E4%B8%8E%E6%8C%82%E8%BD%BD%E8%BD%AF%E7%9B%98
