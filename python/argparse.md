# Argparse Module

``` python

import argparse

parser = argparse.ArgumentParser(description="what the projects do")
parser.add_argument( 'a', # short notation, could be lowercase or uppercase
                '--argument', # long notation 
                metavar='', # this help to clean the -help command
                required=True, # if it is required or not
                type=int, 
                help='help1')
args = parser.parse_args()

 _ = args.argument # Gets the argument "argument" value

```

``` bash
python file.py -a 75 # gives you the information
```

## Mutually excluse argument

``` python
group = parser.add_mutually_exclusive_group()
group.add_argument('q', '--quiet', action='store_true', help='print quiet')
group.add_argument('v', '--verbose', action='store_true', help='print verbose')

args = parser.parse_args()

if args.quiet:
    print(...) # print very less info
elif args.verbose;
    print(...) # print more information
else:
    print(...) # print more or less information

```

``` bash
python file.py -a 75 -v # gives you the information
```

**Observation** See the difference, with parser every input comes with its value `-h 5 -a string` etc. With group it comes just the argument without its value.


Other example of usages to put optional the argument:

``` python
# Required positional argument
parser.add_argument('pos_arg', type=int,
                    help='A required integer positional argument')

# Optional positional argument
parser.add_argument('opt_pos_arg', type=int, nargs='?',
                    help='An optional integer positional argument')

# Optional argument
parser.add_argument('--opt_arg', type=int,
                    help='An optional integer argument')

# Switch
parser.add_argument('--switch', action='store_true',
                    help='A boolean switch')
```

resulting:
``` bash
$ ./app 1 2 --opt_arg 3 --switch

Argument values:
1
2
3
True
```

# Reference
[This video](https://www.youtube.com/watch?v=cdblJqEUDNo)
[StackOverflow](https://stackoverflow.com/questions/20063/whats-the-best-way-to-parse-command-line-arguments)