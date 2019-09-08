#    Yojimbo
#
#    Your-OS-Just-Interprets micro Bash Obfuscator
#
#    Version 1.2 ~ Zalgo Noise ~ Nothing Works 2019
#
#    https://github.com/ZalgoNoise/yojimbo
#
#
#***************************************************
###
###     #  INDEX
###     1. Introduction
###     2. Platforms & Dependencies
###     3. Features and ...features
###     4. Known issues
###     5. Thank you
###

#***************************************************
#
#    1. Introduction
#
#***************************************************


The Yojimbo script idea began with a 30 minute YouTube video from the maker of the Bashfuscator, Andrew LeFevre. Link below. I was looking for means to provide some obfuscation to specific lines of code, when working with completely open source systems (where you can open a text editor and see how the script is written). This is a script written in the perspective of someone who has watched his lecture but never seen the original source code to base myself on.

This is also a technique used to exploit service and application calls when providing malcious payloads.

When written in a script, if you run with debug mode, you will be able to see the command (or the string of the command) in its entirety, so be aware this isn't 100% bulletproof on its own, as even on its raw form it is easily translatable with some time to spare.

When used in conjunction with other methods, though, it can be a very powerful technique. Bash will always read this input as if it wasn't "masked" - the machine interprets, though, the human won't (easily).

The Bashfuscator script is much more complex and dynamic, it is written in Python. This is a micro version to provide you Byte, Hex, or Dual-Hex strings for you to play with. It is entirely written in Bash.

I hope you enjoy this tool, any additions you'd like to see, feel free to submit (as well as corrections to my syntax - I know it's not the best however it works)

    YouTube Link to Bash Obfuscation by Andrew LeFevre: https://youtu.be/zef422NDmpo


#***************************************************
#
#   2. Platforms & Dependencies
#
#***************************************************


Yojimbo can be run on any Linux system with Bash installed and on Termux (which is an excellent proot system for Android users to enjoy Linux when a computer is not around). Fun fact, this script was written in a couple of hours on my phone.

I am using mostly Bash built-ins, with the exception of "sed" and "hexdump".



#***************************************************
#
#   3. Features and ...features
#
#***************************************************


You can currently transform your strings to either Byte, Hex, or Dual-Hex. This is available to you through the arguments you provide before your string.

The syntax is as follows:

    $ yojimbo -[par] <your unquoted string>

Where your available parameters are the following:

    [-B] ~> Byte
            This is the concatenation of the values from "hexdump -b" with the following format: $'\nnn\nnn\nnn'

    [-H] ~> Hex
            This is the concatenation of the values from "hexdump -C" with the following format: $'\xHH\xHH\xHH'

    [-D] ~> Dual-Hex
            This is the concatenation of the values from "hexdump -C" with the following format: $'\uHHHH\uHHHH\uHHHH'

    [-h] ~> Usage / Help
            This prints the usage or help screen. Any invalid option should print this screen as well.



#***************************************************
#
#   4. Known issues and workarounds
#
#***************************************************


    Possibly due to the way I'm getting user input to later on format it after the "getopts" sequence, you should NOT quote your input strings.
    This will result on the output taking in the first word followed by the entire string with the parameter you chose, ergo:

        $ yojimbo -H "cat /etc/shadow"

    Will unfortunately output the equivalent to the string:

        cat -H cat /etc/shadow

    The CORRECT way to input a string is unquoted, just as:

        $ yojimbo -H cat /etc/shadow

    Which will output the equivalent to your actual string:

        cat /etc/shadow



    Also, you will notice that the first word is separated from the rest of the string. This appears to be mandatory when running commands through their Unicode equivalent. To explain this better, when you input 'cat /etc/shadow', the unicode comes out separating 'cat' and '/etc/shadow' such as:

        $ yojimbo -H cat /etc/shadow

      >>>  Your string representation for:
      >>>  cat /etc/shadow
      >>>  Can be executed as:
      >>>  $'\x63\x61\x74' $'\x2f\x65\x74\x63\x2f\x73\x68\x61\x64\x6f\x77'

    This shows that 'cat' ($'\x63\x61\x74') is displayed first, accepted by the shell as a valid command, and we can follow the rest of the string however we want. We can continue with Unicode, drop in nonsense, empty parameter substitutions and combine many techniques all for the sake of making our code harder to read.



#***************************************************
#
#   5. Thank you
#
#***************************************************


    Thank you to Andrew LeFevre and the Bashfuscator development team, for showing me how to properly generate inconspicuous code and payloads in a way I've never imagined possible. I was thinking about sourcing some sketchy hardcoded variables and functions on a separate file but this method is far superior. Please take the time to check him out and the Bashfuscator GitHub repository at:

    Bashfuscator GitHub: https://github.com/Bashfuscator/Bashfuscator
    Andrew LeFevre's Bash Obfuscation lecture: https://youtu.be/zef422NDmpo


~ Zalgo
