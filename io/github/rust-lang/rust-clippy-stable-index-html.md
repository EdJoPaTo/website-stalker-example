absolute\_paths

restriction allow

 Applicability: Unspecified

Added in: 1.73.0

absurd\_extreme\_comparisons

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

alloc\_instead\_of\_core

restriction allow

 Applicability: MachineApplicable

Added in: 1.64.0

allow\_attributes

restriction allow

 Applicability: MachineApplicable

Added in: 1.70.0

allow\_attributes\_without\_reason

restriction allow

 Applicability: Unspecified

Added in: 1.61.0

almost\_complete\_range

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.68.0

almost\_swapped

correctness deny

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

approx\_constant

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

arbitrary\_source\_item\_ordering

restriction allow

 Applicability: Unspecified

Added in: 1.84.0

arc\_with\_non\_send\_sync

suspicious warn

 Applicability: Unspecified

Added in: 1.72.0

arithmetic\_side\_effects

restriction allow

 Applicability: Unspecified

Added in: 1.64.0

as\_conversions

restriction allow

 Applicability: Unspecified

Added in: 1.41.0

as\_pointer\_underscore

restriction allow

 Applicability: MachineApplicable

Added in: 1.85.0

as\_ptr\_cast\_mut

nursery allow

 Applicability: MaybeIncorrect

Added in: 1.66.0

as\_underscore

restriction allow

 Applicability: MachineApplicable

Added in: 1.63.0

assertions\_on\_constants

style warn

 Applicability: Unspecified

Added in: 1.34.0

assertions\_on\_result\_states

restriction allow

 Applicability: MachineApplicable

Added in: 1.64.0

assign\_op\_pattern

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

assign\_ops

deprecated none

 Applicability: Unspecified

Deprecated in: 1.30.0

assigning\_clones

pedantic allow

 Applicability: Unspecified

Added in: 1.78.0

async\_yields\_async

correctness deny

 Applicability: MaybeIncorrect

Added in: 1.48.0

await\_holding\_invalid\_type

suspicious warn

 Applicability: Unspecified

Added in: 1.62.0

await\_holding\_lock

suspicious warn

 Applicability: Unspecified

Added in: 1.45.0

await\_holding\_refcell\_ref

suspicious warn

 Applicability: Unspecified

Added in: 1.49.0

bad\_bit\_mask

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

big\_endian\_bytes

restriction allow

 Applicability: Unspecified

Added in: 1.72.0

bind\_instead\_of\_map

complexity warn

 Applicability: MachineApplicable

Added in: 1.45.0

blanket\_clippy\_restriction\_lints

suspicious warn

 Applicability: Unspecified

Added in: 1.47.0

blocks\_in\_conditions

style warn

 Applicability: MachineApplicable

Added in: 1.45.0

bool\_assert\_comparison

style warn

 Applicability: MachineApplicable

Added in: 1.53.0

bool\_comparison

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

bool\_to\_int\_with\_if

pedantic allow

 Applicability: MachineApplicable

Added in: 1.65.0

borrow\_as\_ptr

pedantic allow

 Applicability: MachineApplicable

Added in: 1.60.0

borrow\_deref\_ref

complexity warn

 Applicability: MachineApplicable

Added in: 1.63.0

borrow\_interior\_mutable\_const

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

borrowed\_box

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

box\_collection

perf warn

 Applicability: Unspecified

Added in: 1.57.0

box\_default

style warn

 Applicability: MachineApplicable

Added in: 1.66.0

boxed\_local

perf warn

 Applicability: Unspecified

Added in: pre 1.29.0

branches\_sharing\_code

nursery allow

 Applicability: Unspecified

Added in: 1.53.0

builtin\_type\_shadow

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

byte\_char\_slices

style warn

 Applicability: MachineApplicable

Added in: 1.81.0

bytes\_count\_to\_len

complexity warn

 Applicability: MachineApplicable

Added in: 1.62.0

bytes\_nth

style warn

 Applicability: MachineApplicable

Added in: 1.52.0

cargo\_common\_metadata

cargo allow

 Applicability: Unspecified

Added in: 1.32.0

case\_sensitive\_file\_extension\_comparisons

pedantic allow

 Applicability: MaybeIncorrect

Added in: 1.51.0

cast\_abs\_to\_unsigned

suspicious warn

 Applicability: MachineApplicable

Added in: 1.62.0

cast\_enum\_constructor

suspicious warn

 Applicability: Unspecified

Added in: 1.61.0

cast\_enum\_truncation

suspicious warn

 Applicability: Unspecified

Added in: 1.61.0

cast\_lossless

pedantic allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

cast\_nan\_to\_int

suspicious warn

 Applicability: Unspecified

Added in: 1.66.0

cast\_possible\_truncation

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

cast\_possible\_wrap

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

cast\_precision\_loss

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

cast\_ptr\_alignment

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

cast\_sign\_loss

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

cast\_slice\_different\_sizes

correctness deny

 Applicability: HasPlaceholders

Added in: 1.61.0

cast\_slice\_from\_raw\_parts

suspicious warn

 Applicability: MachineApplicable

Added in: 1.65.0

cfg\_not\_test

restriction allow

 Applicability: Unspecified

Added in: 1.81.0

char\_indices\_as\_byte\_indices

correctness deny

 Applicability: MaybeIncorrect

Added in: 1.83.0

char\_lit\_as\_u8

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

chars\_last\_cmp

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

chars\_next\_cmp

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

checked\_conversions

pedantic allow

 Applicability: MachineApplicable

Added in: 1.37.0

clear\_with\_drain

nursery allow

 Applicability: MachineApplicable

Added in: 1.70.0

clone\_on\_copy

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

clone\_on\_ref\_ptr

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

cloned\_instead\_of\_copied

pedantic allow

 Applicability: MachineApplicable

Added in: 1.53.0

cmp\_null

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

cmp\_owned

perf warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

cognitive\_complexity

nursery allow

 Applicability: Unspecified

Added in: 1.35.0

collapsible\_else\_if

style warn

 Applicability: MachineApplicable

Added in: 1.51.0

collapsible\_if

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

collapsible\_match

style warn

 Applicability: Unspecified

Added in: 1.50.0

collapsible\_str\_replace

perf warn

 Applicability: MachineApplicable

Added in: 1.65.0

collection\_is\_never\_read

nursery allow

 Applicability: Unspecified

Added in: 1.70.0

comparison\_chain

pedantic allow

 Applicability: HasPlaceholders

Added in: 1.40.0

comparison\_to\_empty

style warn

 Applicability: MachineApplicable

Added in: 1.49.0

const\_is\_empty

suspicious warn

 Applicability: Unspecified

Added in: 1.79.0

copy\_iterator

pedantic allow

 Applicability: Unspecified

Added in: 1.30.0

crate\_in\_macro\_def

suspicious warn

 Applicability: MachineApplicable

Added in: 1.62.0

create\_dir

restriction allow

 Applicability: MaybeIncorrect

Added in: 1.48.0

crosspointer\_transmute

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

dbg\_macro

restriction allow

 Applicability: MachineApplicable

Added in: 1.34.0

debug\_assert\_with\_mut\_call

nursery allow

 Applicability: Unspecified

Added in: 1.40.0

decimal\_literal\_representation

restriction allow

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

declare\_interior\_mutable\_const

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

default\_constructed\_unit\_structs

complexity warn

 Applicability: MachineApplicable

Added in: 1.71.0

default\_instead\_of\_iter\_empty

style warn

 Applicability: MachineApplicable

Added in: 1.64.0

default\_numeric\_fallback

restriction allow

 Applicability: MaybeIncorrect

Added in: 1.52.0

default\_trait\_access

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

default\_union\_representation

restriction allow

 Applicability: Unspecified

Added in: 1.60.0

deprecated\_cfg\_attr

complexity warn

 Applicability: MachineApplicable

Added in: 1.32.0

deprecated\_clippy\_cfg\_attr

suspicious warn

 Applicability: MachineApplicable

Added in: 1.78.0

deprecated\_semver

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

deref\_addrof

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

deref\_by\_slicing

restriction allow

 Applicability: MachineApplicable

Added in: 1.61.0

derivable\_impls

complexity warn

 Applicability: MachineApplicable

Added in: 1.57.0

derive\_ord\_xor\_partial\_ord

correctness deny

 Applicability: Unspecified

Added in: 1.47.0

derive\_partial\_eq\_without\_eq

nursery allow

 Applicability: MachineApplicable

Added in: 1.63.0

derived\_hash\_with\_manual\_eq

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

disallowed\_macros

style warn

 Applicability: Unspecified

Added in: 1.66.0

disallowed\_methods

style warn

 Applicability: MachineApplicable

Added in: 1.49.0

disallowed\_names

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

disallowed\_script\_idents

restriction allow

 Applicability: Unspecified

Added in: 1.55.0

disallowed\_types

style warn

 Applicability: MachineApplicable

Added in: 1.55.0

diverging\_sub\_expression

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

doc\_comment\_double\_space\_linebreaks

pedantic allow

 Applicability: MachineApplicable

Added in: 1.87.0

doc\_include\_without\_cfg

restriction allow

 Applicability: MachineApplicable

Added in: 1.85.0

doc\_lazy\_continuation

style warn

 Applicability: MachineApplicable

Added in: 1.80.0

doc\_link\_code

nursery allow

 Applicability: MaybeIncorrect

Added in: 1.86.0

doc\_link\_with\_quotes

pedantic allow

 Applicability: Unspecified

Added in: 1.63.0

doc\_markdown

pedantic allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

doc\_nested\_refdefs

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.85.0

doc\_overindented\_list\_items

style warn

 Applicability: MaybeIncorrect

Added in: 1.86.0

double\_comparisons

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

double\_ended\_iterator\_last

perf warn

 Applicability: MachineApplicable

Added in: 1.86.0

double\_must\_use

style warn

 Applicability: Unspecified

Added in: 1.40.0

double\_parens

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

drain\_collect

perf warn

 Applicability: MachineApplicable

Added in: 1.72.0

drop\_non\_drop

suspicious warn

 Applicability: Unspecified

Added in: 1.62.0

duplicate\_mod

suspicious warn

 Applicability: Unspecified

Added in: 1.63.0

duplicate\_underscore\_argument

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

duplicated\_attributes

suspicious warn

 Applicability: Unspecified

Added in: 1.79.0

duration\_subsec

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

eager\_transmute

correctness deny

 Applicability: MaybeIncorrect

Added in: 1.77.0

elidable\_lifetime\_names

pedantic allow

 Applicability: MachineApplicable

Added in: 1.84.0

else\_if\_without\_else

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

empty\_docs

suspicious warn

 Applicability: Unspecified

Added in: 1.78.0

empty\_drop

restriction allow

 Applicability: MaybeIncorrect

Added in: 1.62.0

empty\_enum

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

empty\_enum\_variants\_with\_brackets

restriction allow

 Applicability: MaybeIncorrect

Added in: 1.77.0

empty\_line\_after\_doc\_comments

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.70.0

empty\_line\_after\_outer\_attr

suspicious warn

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

empty\_loop

suspicious warn

 Applicability: Unspecified

Added in: pre 1.29.0

empty\_structs\_with\_brackets

restriction allow

 Applicability: Unspecified

Added in: 1.62.0

enum\_clike\_unportable\_variant

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

enum\_glob\_use

pedantic allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

enum\_variant\_names

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

eq\_op

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

equatable\_if\_let

nursery allow

 Applicability: MachineApplicable

Added in: 1.57.0

erasing\_op

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

err\_expect

style warn

 Applicability: MachineApplicable

Added in: 1.62.0

error\_impl\_error

restriction allow

 Applicability: Unspecified

Added in: 1.73.0

excessive\_nesting

complexity warn

 Applicability: Unspecified

Added in: 1.72.0

excessive\_precision

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

exhaustive\_enums

restriction allow

 Applicability: MaybeIncorrect

Added in: 1.51.0

exhaustive\_structs

restriction allow

 Applicability: MaybeIncorrect

Added in: 1.51.0

exit

restriction allow

 Applicability: Unspecified

Added in: 1.41.0

expect\_fun\_call

perf warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

expect\_used

restriction allow

 Applicability: Unspecified

Added in: 1.45.0

expl\_impl\_clone\_on\_copy

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

explicit\_auto\_deref

complexity warn

 Applicability: MachineApplicable

Added in: 1.64.0

explicit\_counter\_loop

complexity warn

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

explicit\_deref\_methods

pedantic allow

 Applicability: MachineApplicable

Added in: 1.44.0

explicit\_into\_iter\_loop

pedantic allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

explicit\_iter\_loop

pedantic allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

explicit\_write

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

extend\_from\_slice

deprecated none

 Applicability: Unspecified

Deprecated in: pre 1.29.0

extend\_with\_drain

perf warn

 Applicability: MachineApplicable

Added in: 1.55.0

extra\_unused\_lifetimes

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

extra\_unused\_type\_parameters

complexity warn

 Applicability: MachineApplicable

Added in: 1.69.0

fallible\_impl\_from

nursery allow

 Applicability: Unspecified

Added in: pre 1.29.0

field\_reassign\_with\_default

style warn

 Applicability: Unspecified

Added in: 1.49.0

field\_scoped\_visibility\_modifiers

restriction allow

 Applicability: Unspecified

Added in: 1.81.0

filetype\_is\_file

restriction allow

 Applicability: Unspecified

Added in: 1.42.0

filter\_map\_bool\_then

style warn

 Applicability: MachineApplicable

Added in: 1.73.0

filter\_map\_identity

complexity warn

 Applicability: MachineApplicable

Added in: 1.52.0

filter\_map\_next

pedantic allow

 Applicability: MachineApplicable

Added in: 1.36.0

filter\_next

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

flat\_map\_identity

complexity warn

 Applicability: MachineApplicable

Added in: 1.39.0

flat\_map\_option

pedantic allow

 Applicability: MachineApplicable

Added in: 1.53.0

float\_arithmetic

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

float\_cmp

pedantic allow

 Applicability: HasPlaceholders

Added in: pre 1.29.0

float\_cmp\_const

restriction allow

 Applicability: HasPlaceholders

Added in: pre 1.29.0

float\_equality\_without\_abs

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.48.0

fn\_params\_excessive\_bools

pedantic allow

 Applicability: Unspecified

Added in: 1.43.0

fn\_to\_numeric\_cast

style warn

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

fn\_to\_numeric\_cast\_any

restriction allow

 Applicability: MaybeIncorrect

Added in: 1.58.0

fn\_to\_numeric\_cast\_with\_truncation

style warn

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

for\_kv\_map

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

forget\_non\_drop

suspicious warn

 Applicability: Unspecified

Added in: 1.62.0

format\_collect

pedantic allow

 Applicability: Unspecified

Added in: 1.73.0

format\_in\_format\_args

perf warn

 Applicability: Unspecified

Added in: 1.58.0

format\_push\_string

pedantic allow

 Applicability: Unspecified

Added in: 1.62.0

four\_forward\_slashes

suspicious warn

 Applicability: MachineApplicable

Added in: 1.73.0

from\_iter\_instead\_of\_collect

pedantic allow

 Applicability: MaybeIncorrect

Added in: 1.49.0

from\_over\_into

style warn

 Applicability: MachineApplicable

Added in: 1.51.0

from\_raw\_with\_void\_ptr

suspicious warn

 Applicability: Unspecified

Added in: 1.67.0

from\_str\_radix\_10

style warn

 Applicability: MaybeIncorrect

Added in: 1.52.0

future\_not\_send

nursery allow

 Applicability: Unspecified

Added in: 1.44.0

get\_first

style warn

 Applicability: MachineApplicable

Added in: 1.63.0

get\_last\_with\_len

complexity warn

 Applicability: MachineApplicable

Added in: 1.37.0

get\_unwrap

restriction allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

host\_endian\_bytes

restriction allow

 Applicability: Unspecified

Added in: 1.72.0

identity\_op

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

if\_let\_mutex

correctness deny

 Applicability: Unspecified

Added in: 1.45.0

if\_not\_else

pedantic allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

if\_same\_then\_else

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

if\_then\_some\_else\_none

restriction allow

 Applicability: MachineApplicable

Added in: 1.53.0

ifs\_same\_cond

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

ignore\_without\_reason

pedantic allow

 Applicability: Unspecified

Added in: 1.85.0

ignored\_unit\_patterns

pedantic allow

 Applicability: MachineApplicable

Added in: 1.73.0

impl\_hash\_borrow\_with\_str\_and\_bytes

correctness deny

 Applicability: Unspecified

Added in: 1.76.0

impl\_trait\_in\_params

restriction allow

 Applicability: HasPlaceholders

Added in: 1.69.0

implicit\_clone

pedantic allow

 Applicability: MachineApplicable

Added in: 1.52.0

implicit\_hasher

pedantic allow

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

implicit\_return

restriction allow

 Applicability: MachineApplicable

Added in: 1.33.0

implicit\_saturating\_add

style warn

 Applicability: MachineApplicable

Added in: 1.66.0

implicit\_saturating\_sub

style warn

 Applicability: MachineApplicable

Added in: 1.44.0

implied\_bounds\_in\_impls

complexity warn

 Applicability: MachineApplicable

Added in: 1.74.0

impossible\_comparisons

correctness deny

 Applicability: Unspecified

Added in: 1.73.0

imprecise\_flops

nursery allow

 Applicability: MachineApplicable

Added in: 1.43.0

incompatible\_msrv

suspicious warn

 Applicability: Unspecified

Added in: 1.78.0

inconsistent\_digit\_grouping

style warn

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

inconsistent\_struct\_constructor

pedantic allow

 Applicability: MachineApplicable

Added in: 1.52.0

index\_refutable\_slice

pedantic allow

 Applicability: MaybeIncorrect

Added in: 1.59.0

indexing\_slicing

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

ineffective\_bit\_mask

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

ineffective\_open\_options

suspicious warn

 Applicability: MachineApplicable

Added in: 1.76.0

inefficient\_to\_string

pedantic allow

 Applicability: MachineApplicable

Added in: 1.40.0

infallible\_destructuring\_match

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

infinite\_iter

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

infinite\_loop

restriction allow

 Applicability: MaybeIncorrect

Added in: 1.76.0

inherent\_to\_string

style warn

 Applicability: Unspecified

Added in: 1.38.0

inherent\_to\_string\_shadow\_display

correctness deny

 Applicability: Unspecified

Added in: 1.38.0

init\_numbered\_fields

style warn

 Applicability: MachineApplicable

Added in: 1.59.0

inline\_always

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

inline\_asm\_x86\_att\_syntax

restriction allow

 Applicability: Unspecified

Added in: 1.49.0

inline\_asm\_x86\_intel\_syntax

restriction allow

 Applicability: Unspecified

Added in: 1.49.0

inline\_fn\_without\_body

correctness deny

 Applicability: MachineApplicable

Added in: pre 1.29.0

inspect\_for\_each

complexity warn

 Applicability: Unspecified

Added in: 1.51.0

int\_plus\_one

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

integer\_division

restriction allow

 Applicability: Unspecified

Added in: 1.37.0

integer\_division\_remainder\_used

restriction allow

 Applicability: Unspecified

Added in: 1.79.0

into\_iter\_on\_ref

style warn

 Applicability: MachineApplicable

Added in: 1.32.0

into\_iter\_without\_iter

pedantic allow

 Applicability: Unspecified

Added in: 1.75.0

invalid\_regex

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

invalid\_upcast\_comparisons

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

inverted\_saturating\_sub

correctness deny

 Applicability: MaybeIncorrect

Added in: 1.44.0

invisible\_characters

correctness deny

 Applicability: MachineApplicable

Added in: 1.49.0

io\_other\_error

style warn

 Applicability: MachineApplicable

Added in: 1.87.0

is\_digit\_ascii\_radix

style warn

 Applicability: MachineApplicable

Added in: 1.62.0

items\_after\_statements

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

items\_after\_test\_module

style warn

 Applicability: MachineApplicable

Added in: 1.71.0

iter\_cloned\_collect

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

iter\_count

complexity warn

 Applicability: MachineApplicable

Added in: 1.52.0

iter\_filter\_is\_ok

pedantic allow

 Applicability: HasPlaceholders

Added in: 1.77.0

iter\_filter\_is\_some

pedantic allow

 Applicability: HasPlaceholders

Added in: 1.77.0

iter\_kv\_map

complexity warn

 Applicability: MachineApplicable

Added in: 1.66.0

iter\_next\_loop

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

iter\_next\_slice

style warn

 Applicability: MachineApplicable

Added in: 1.46.0

iter\_not\_returning\_iterator

pedantic allow

 Applicability: Unspecified

Added in: 1.57.0

iter\_nth

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

iter\_nth\_zero

style warn

 Applicability: MachineApplicable

Added in: 1.42.0

iter\_on\_empty\_collections

nursery allow

 Applicability: MaybeIncorrect

Added in: 1.65.0

iter\_on\_single\_items

nursery allow

 Applicability: MaybeIncorrect

Added in: 1.65.0

iter\_out\_of\_bounds

suspicious warn

 Applicability: Unspecified

Added in: 1.74.0

iter\_over\_hash\_type

restriction allow

 Applicability: Unspecified

Added in: 1.76.0

iter\_overeager\_cloned

perf warn

 Applicability: MachineApplicable

Added in: 1.60.0

iter\_skip\_next

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

iter\_skip\_zero

correctness deny

 Applicability: MaybeIncorrect

Added in: 1.73.0

iter\_with\_drain

nursery allow

 Applicability: MaybeIncorrect

Added in: 1.61.0

iter\_without\_into\_iter

pedantic allow

 Applicability: Unspecified

Added in: 1.75.0

iterator\_step\_by\_zero

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

join\_absolute\_paths

suspicious warn

 Applicability: Unspecified

Added in: 1.76.0

just\_underscores\_and\_digits

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

large\_const\_arrays

perf warn

 Applicability: MachineApplicable

Added in: 1.44.0

large\_digit\_groups

pedantic allow

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

large\_enum\_variant

perf warn

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

large\_futures

pedantic allow

 Applicability: Unspecified

Added in: 1.70.0

large\_include\_file

restriction allow

 Applicability: Unspecified

Added in: 1.62.0

large\_stack\_arrays

pedantic allow

 Applicability: Unspecified

Added in: 1.41.0

large\_stack\_frames

nursery allow

 Applicability: Unspecified

Added in: 1.72.0

large\_types\_passed\_by\_value

pedantic allow

 Applicability: MaybeIncorrect

Added in: 1.49.0

legacy\_numeric\_constants

style warn

 Applicability: MaybeIncorrect

Added in: 1.79.0

len\_without\_is\_empty

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

len\_zero

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

let\_and\_return

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

let\_underscore\_future

suspicious warn

 Applicability: Unspecified

Added in: 1.67.0

let\_underscore\_lock

correctness deny

 Applicability: Unspecified

Added in: 1.43.0

let\_underscore\_must\_use

restriction allow

 Applicability: Unspecified

Added in: 1.42.0

let\_underscore\_untyped

restriction allow

 Applicability: Unspecified

Added in: 1.69.0

let\_unit\_value

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

let\_with\_type\_underscore

complexity warn

 Applicability: Unspecified

Added in: 1.70.0

lines\_filter\_map\_ok

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.70.0

linkedlist

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

lint\_groups\_priority

correctness deny

 Applicability: Unspecified

Added in: 1.78.0

literal\_string\_with\_formatting\_args

nursery allow

 Applicability: Unspecified

Added in: 1.85.0

little\_endian\_bytes

restriction allow

 Applicability: Unspecified

Added in: 1.72.0

lossy\_float\_literal

restriction allow

 Applicability: MachineApplicable

Added in: 1.43.0

macro\_metavars\_in\_unsafe

suspicious warn

 Applicability: Unspecified

Added in: 1.80.0

macro\_use\_imports

pedantic allow

 Applicability: MaybeIncorrect

Added in: 1.44.0

main\_recursion

style warn

 Applicability: Unspecified

Added in: 1.38.0

manual\_abs\_diff

complexity warn

 Applicability: MachineApplicable

Added in: 1.86.0

manual\_assert

pedantic allow

 Applicability: MachineApplicable

Added in: 1.57.0

manual\_async\_fn

style warn

 Applicability: MachineApplicable

Added in: 1.45.0

manual\_bits

style warn

 Applicability: MachineApplicable

Added in: 1.60.0

manual\_c\_str\_literals

complexity warn

 Applicability: MachineApplicable

Added in: 1.78.0

manual\_clamp

complexity warn

 Applicability: MaybeIncorrect

Added in: 1.66.0

manual\_contains

perf warn

 Applicability: MachineApplicable

Added in: 1.86.0

manual\_dangling\_ptr

style warn

 Applicability: MachineApplicable

Added in: 1.87.0

manual\_div\_ceil

complexity warn

 Applicability: MachineApplicable

Added in: 1.83.0

manual\_filter

complexity warn

 Applicability: MachineApplicable

Added in: 1.66.0

manual\_filter\_map

complexity warn

 Applicability: MachineApplicable

Added in: 1.51.0

manual\_find

complexity warn

 Applicability: MachineApplicable

Added in: 1.64.0

manual\_find\_map

complexity warn

 Applicability: MachineApplicable

Added in: 1.51.0

manual\_flatten

complexity warn

 Applicability: MaybeIncorrect

Added in: 1.52.0

manual\_hash\_one

complexity warn

 Applicability: MachineApplicable

Added in: 1.75.0

manual\_ignore\_case\_cmp

perf warn

 Applicability: MachineApplicable

Added in: 1.84.0

manual\_inspect

complexity warn

 Applicability: MachineApplicable

Added in: 1.81.0

manual\_instant\_elapsed

pedantic allow

 Applicability: MachineApplicable

Added in: 1.65.0

manual\_is\_ascii\_check

style warn

 Applicability: MachineApplicable

Added in: 1.67.0

manual\_is\_finite

style warn

 Applicability: MaybeIncorrect

Added in: 1.73.0

manual\_is\_infinite

style warn

 Applicability: MachineApplicable

Added in: 1.73.0

manual\_is\_power\_of\_two

pedantic allow

 Applicability: MachineApplicable

Added in: 1.83.0

manual\_is\_variant\_and

pedantic allow

 Applicability: MachineApplicable

Added in: 1.77.0

manual\_let\_else

pedantic allow

 Applicability: HasPlaceholders

Added in: 1.67.0

manual\_main\_separator\_str

complexity warn

 Applicability: MachineApplicable

Added in: 1.70.0

manual\_map

style warn

 Applicability: MachineApplicable

Added in: 1.52.0

manual\_memcpy

perf warn

 Applicability: Unspecified

Added in: pre 1.29.0

manual\_midpoint

pedantic allow

 Applicability: MachineApplicable

Added in: 1.87.0

manual\_next\_back

style warn

 Applicability: MachineApplicable

Added in: 1.71.0

manual\_non\_exhaustive

style warn

 Applicability: MaybeIncorrect

Added in: 1.45.0

manual\_ok\_err

complexity warn

 Applicability: MachineApplicable

Added in: 1.86.0

manual\_ok\_or

style warn

 Applicability: MachineApplicable

Added in: 1.49.0

manual\_option\_as\_slice

complexity warn

 Applicability: MachineApplicable

Added in: 1.86.0

manual\_pattern\_char\_comparison

style warn

 Applicability: MachineApplicable

Added in: 1.81.0

manual\_range\_contains

style warn

 Applicability: MachineApplicable

Added in: 1.49.0

manual\_range\_patterns

complexity warn

 Applicability: MachineApplicable

Added in: 1.72.0

manual\_rem\_euclid

complexity warn

 Applicability: MachineApplicable

Added in: 1.64.0

manual\_repeat\_n

style warn

 Applicability: MachineApplicable

Added in: 1.86.0

manual\_retain

perf warn

 Applicability: MachineApplicable

Added in: 1.64.0

manual\_rotate

style warn

 Applicability: MachineApplicable

Added in: 1.81.0

manual\_saturating\_arithmetic

style warn

 Applicability: MachineApplicable

Added in: 1.39.0

manual\_slice\_fill

style warn

 Applicability: MaybeIncorrect

Added in: 1.86.0

manual\_slice\_size\_calculation

complexity warn

 Applicability: MachineApplicable

Added in: 1.70.0

manual\_split\_once

complexity warn

 Applicability: MachineApplicable

Added in: 1.57.0

manual\_str\_repeat

perf warn

 Applicability: MachineApplicable

Added in: 1.54.0

manual\_string\_new

pedantic allow

 Applicability: MachineApplicable

Added in: 1.65.0

manual\_strip

complexity warn

 Applicability: MachineApplicable

Added in: 1.48.0

manual\_swap

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

manual\_try\_fold

perf warn

 Applicability: HasPlaceholders

Added in: 1.72.0

manual\_unwrap\_or

complexity warn

 Applicability: MachineApplicable

Added in: 1.49.0

manual\_unwrap\_or\_default

suspicious warn

 Applicability: MachineApplicable

Added in: 1.79.0

manual\_while\_let\_some

style warn

 Applicability: MachineApplicable

Added in: 1.71.0

many\_single\_char\_names

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

map\_all\_any\_identity

complexity warn

 Applicability: MachineApplicable

Added in: 1.84.0

map\_clone

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

map\_collect\_result\_unit

style warn

 Applicability: MachineApplicable

Added in: 1.49.0

map\_entry

perf warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

map\_err\_ignore

restriction allow

 Applicability: Unspecified

Added in: 1.48.0

map\_flatten

complexity warn

 Applicability: MachineApplicable

Added in: 1.31.0

map\_identity

complexity warn

 Applicability: MachineApplicable

Added in: 1.47.0

map\_unwrap\_or

pedantic allow

 Applicability: MachineApplicable

Added in: 1.45.0

map\_with\_unused\_argument\_over\_ranges

restriction allow

 Applicability: MaybeIncorrect

Added in: 1.84.0

match\_as\_ref

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

match\_bool

pedantic allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

match\_like\_matches\_macro

style warn

 Applicability: MaybeIncorrect

Added in: 1.47.0

match\_on\_vec\_items

deprecated none

 Applicability: Unspecified

Deprecated in: 1.86.0

match\_overlapping\_arm

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

match\_ref\_pats

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

match\_result\_ok

style warn

 Applicability: MachineApplicable

Added in: 1.57.0

match\_same\_arms

pedantic allow

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

match\_single\_binding

complexity warn

 Applicability: MachineApplicable

Added in: 1.43.0

match\_str\_case\_mismatch

correctness deny

 Applicability: MachineApplicable

Added in: 1.58.0

match\_wild\_err\_arm

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

match\_wildcard\_for\_single\_variants

pedantic allow

 Applicability: MaybeIncorrect

Added in: 1.45.0

maybe\_infinite\_iter

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

mem\_forget

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

mem\_replace\_option\_with\_none

style warn

 Applicability: MachineApplicable

Added in: 1.31.0

mem\_replace\_option\_with\_some

style warn

 Applicability: MachineApplicable

Added in: 1.86.0

mem\_replace\_with\_default

style warn

 Applicability: MachineApplicable

Added in: 1.42.0

mem\_replace\_with\_uninit

correctness deny

 Applicability: MachineApplicable

Added in: 1.39.0

min\_ident\_chars

restriction allow

 Applicability: Unspecified

Added in: 1.72.0

min\_max

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

misaligned\_transmute

deprecated none

 Applicability: Unspecified

Deprecated in: pre 1.29.0

mismatching\_type\_param\_order

pedantic allow

 Applicability: Unspecified

Added in: 1.63.0

misnamed\_getters

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.67.0

misrefactored\_assign\_op

suspicious warn

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

missing\_assert\_message

restriction allow

 Applicability: Unspecified

Added in: 1.70.0

missing\_asserts\_for\_indexing

restriction allow

 Applicability: MachineApplicable

Added in: 1.74.0

missing\_const\_for\_fn

nursery allow

 Applicability: MachineApplicable

Added in: 1.34.0

missing\_const\_for\_thread\_local

perf warn

 Applicability: MachineApplicable

Added in: 1.77.0

missing\_docs\_in\_private\_items

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

missing\_enforced\_import\_renames

style warn

 Applicability: MachineApplicable

Added in: 1.55.0

missing\_errors\_doc

pedantic allow

 Applicability: Unspecified

Added in: 1.41.0

missing\_fields\_in\_debug

pedantic allow

 Applicability: Unspecified

Added in: 1.70.0

missing\_inline\_in\_public\_items

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

missing\_panics\_doc

pedantic allow

 Applicability: Unspecified

Added in: 1.51.0

missing\_safety\_doc

style warn

 Applicability: Unspecified

Added in: 1.39.0

missing\_spin\_loop

perf warn

 Applicability: MachineApplicable

Added in: 1.61.0

missing\_trait\_methods

restriction allow

 Applicability: Unspecified

Added in: 1.66.0

missing\_transmute\_annotations

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.79.0

mistyped\_literal\_suffixes

correctness deny

 Applicability: MaybeIncorrect

Added in: 1.30.0

mixed\_attributes\_style

style warn

 Applicability: Unspecified

Added in: 1.78.0

mixed\_case\_hex\_literals

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

mixed\_read\_write\_in\_expression

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

mod\_module\_files

restriction allow

 Applicability: Unspecified

Added in: 1.57.0

module\_inception

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

module\_name\_repetitions

restriction allow

 Applicability: Unspecified

Added in: 1.33.0

modulo\_arithmetic

restriction allow

 Applicability: Unspecified

Added in: 1.42.0

modulo\_one

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

multi\_assignments

suspicious warn

 Applicability: Unspecified

Added in: 1.65.0

multiple\_bound\_locations

suspicious warn

 Applicability: Unspecified

Added in: 1.78.0

multiple\_crate\_versions

cargo allow

 Applicability: Unspecified

Added in: pre 1.29.0

multiple\_inherent\_impl

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

multiple\_unsafe\_ops\_per\_block

restriction allow

 Applicability: Unspecified

Added in: 1.69.0

must\_use\_candidate

pedantic allow

 Applicability: MachineApplicable

Added in: 1.40.0

must\_use\_unit

style warn

 Applicability: MachineApplicable

Added in: 1.40.0

mut\_from\_ref

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

mut\_mut

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

mut\_mutex\_lock

style warn

 Applicability: MaybeIncorrect

Added in: 1.49.0

mut\_range\_bound

suspicious warn

 Applicability: Unspecified

Added in: pre 1.29.0

mutable\_key\_type

suspicious warn

 Applicability: Unspecified

Added in: 1.42.0

mutex\_atomic

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

mutex\_integer

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

naive\_bytecount

pedantic allow

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

needless\_arbitrary\_self\_type

complexity warn

 Applicability: MachineApplicable

Added in: 1.47.0

needless\_as\_bytes

complexity warn

 Applicability: MachineApplicable

Added in: 1.84.0

needless\_bitwise\_bool

pedantic allow

 Applicability: MachineApplicable

Added in: 1.54.0

needless\_bool

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

needless\_bool\_assign

complexity warn

 Applicability: MachineApplicable

Added in: 1.71.0

needless\_borrow

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

needless\_borrowed\_reference

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

needless\_borrows\_for\_generic\_args

style warn

 Applicability: MachineApplicable

Added in: 1.74.0

needless\_character\_iteration

suspicious warn

 Applicability: MachineApplicable

Added in: 1.81.0

needless\_collect

nursery allow

 Applicability: MachineApplicable

Added in: 1.30.0

needless\_continue

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

needless\_doctest\_main

style warn

 Applicability: Unspecified

Added in: 1.40.0

needless\_else

style warn

 Applicability: MachineApplicable

Added in: 1.72.0

needless\_for\_each

pedantic allow

 Applicability: MachineApplicable

Added in: 1.53.0

needless\_if

complexity warn

 Applicability: MachineApplicable

Added in: 1.72.0

needless\_late\_init

style warn

 Applicability: MachineApplicable

Added in: 1.59.0

needless\_lifetimes

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

needless\_match

complexity warn

 Applicability: MachineApplicable

Added in: 1.61.0

needless\_maybe\_sized

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.81.0

needless\_option\_as\_deref

complexity warn

 Applicability: MachineApplicable

Added in: 1.57.0

needless\_option\_take

complexity warn

 Applicability: MachineApplicable

Added in: 1.62.0

needless\_parens\_on\_range\_literals

style warn

 Applicability: MachineApplicable

Added in: 1.63.0

needless\_pass\_by\_ref\_mut

nursery allow

 Applicability: Unspecified

Added in: 1.73.0

needless\_pass\_by\_value

pedantic allow

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

needless\_pub\_self

style warn

 Applicability: MachineApplicable

Added in: 1.72.0

needless\_question\_mark

complexity warn

 Applicability: MachineApplicable

Added in: 1.51.0

needless\_range\_loop

style warn

 Applicability: HasPlaceholders

Added in: pre 1.29.0

needless\_raw\_string\_hashes

pedantic allow

 Applicability: MachineApplicable

Added in: 1.72.0

needless\_raw\_strings

restriction allow

 Applicability: MachineApplicable

Added in: 1.72.0

needless\_return

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

needless\_return\_with\_question\_mark

style warn

 Applicability: MachineApplicable

Added in: 1.73.0

needless\_splitn

complexity warn

 Applicability: MachineApplicable

Added in: 1.59.0

needless\_update

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

neg\_cmp\_op\_on\_partial\_ord

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

neg\_multiply

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

negative\_feature\_names

cargo allow

 Applicability: Unspecified

Added in: 1.57.0

never\_loop

correctness deny

 Applicability: MachineApplicable

Added in: pre 1.29.0

new\_ret\_no\_self

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

new\_without\_default

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

no\_effect

complexity warn

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

no\_effect\_replace

suspicious warn

 Applicability: Unspecified

Added in: 1.63.0

no\_effect\_underscore\_binding

pedantic allow

 Applicability: Unspecified

Added in: 1.58.0

no\_mangle\_with\_rust\_abi

pedantic allow

 Applicability: MaybeIncorrect

Added in: 1.69.0

non\_ascii\_literal

restriction allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

non\_canonical\_clone\_impl

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.72.0

non\_canonical\_partial\_ord\_impl

suspicious warn

 Applicability: Unspecified

Added in: 1.73.0

non\_minimal\_cfg

style warn

 Applicability: MaybeIncorrect

Added in: 1.71.0

non\_octal\_unix\_permissions

correctness deny

 Applicability: MachineApplicable

Added in: 1.53.0

non\_send\_fields\_in\_send\_ty

nursery allow

 Applicability: Unspecified

Added in: 1.57.0

non\_std\_lazy\_statics

pedantic allow

 Applicability: MachineApplicable

Added in: 1.86.0

non\_zero\_suggestions

restriction allow

 Applicability: MachineApplicable

Added in: 1.83.0

nonminimal\_bool

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

nonsensical\_open\_options

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

nonstandard\_macro\_braces

nursery allow

 Applicability: MachineApplicable

Added in: 1.55.0

not\_unsafe\_ptr\_arg\_deref

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

obfuscated\_if\_else

style warn

 Applicability: MachineApplicable

Added in: 1.64.0

octal\_escapes

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.59.0

ok\_expect

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

only\_used\_in\_recursion

complexity warn

 Applicability: MaybeIncorrect

Added in: 1.61.0

op\_ref

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

option\_as\_ref\_cloned

pedantic allow

 Applicability: MachineApplicable

Added in: 1.77.0

option\_as\_ref\_deref

complexity warn

 Applicability: MachineApplicable

Added in: 1.42.0

option\_env\_unwrap

correctness deny

 Applicability: Unspecified

Added in: 1.43.0

option\_filter\_map

complexity warn

 Applicability: MachineApplicable

Added in: 1.53.0

option\_if\_let\_else

nursery allow

 Applicability: MaybeIncorrect

Added in: 1.47.0

option\_map\_or\_err\_ok

deprecated none

 Applicability: Unspecified

Deprecated in: 1.86.0

option\_map\_or\_none

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

option\_map\_unit\_fn

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

option\_option

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

or\_fun\_call

nursery allow

 Applicability: HasPlaceholders

Added in: pre 1.29.0

or\_then\_unwrap

complexity warn

 Applicability: MachineApplicable

Added in: 1.61.0

out\_of\_bounds\_indexing

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

overly\_complex\_bool\_expr

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

owned\_cow

style warn

 Applicability: Unspecified

Added in: 1.85.0

panic

restriction allow

 Applicability: Unspecified

Added in: 1.40.0

panic\_in\_result\_fn

restriction allow

 Applicability: Unspecified

Added in: 1.48.0

panicking\_overflow\_checks

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

panicking\_unwrap

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

partial\_pub\_fields

restriction allow

 Applicability: Unspecified

Added in: 1.66.0

partialeq\_ne\_impl

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

partialeq\_to\_none

style warn

 Applicability: MachineApplicable

Added in: 1.65.0

path\_buf\_push\_overwrite

nursery allow

 Applicability: MaybeIncorrect

Added in: 1.36.0

path\_ends\_with\_ext

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.74.0

pathbuf\_init\_then\_push

restriction allow

 Applicability: HasPlaceholders

Added in: 1.82.0

pattern\_type\_mismatch

restriction allow

 Applicability: Unspecified

Added in: 1.47.0

permissions\_set\_readonly\_false

suspicious warn

 Applicability: Unspecified

Added in: 1.68.0

pointers\_in\_nomem\_asm\_block

suspicious warn

 Applicability: Unspecified

Added in: 1.81.0

possible\_missing\_comma

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

precedence

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

precedence\_bits

restriction allow

 Applicability: MachineApplicable

Added in: 1.86.0

print\_in\_format\_impl

suspicious warn

 Applicability: HasPlaceholders

Added in: 1.61.0

print\_literal

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

print\_stderr

restriction allow

 Applicability: Unspecified

Added in: 1.50.0

print\_stdout

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

print\_with\_newline

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

println\_empty\_string

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

ptr\_arg

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

ptr\_as\_ptr

pedantic allow

 Applicability: MachineApplicable

Added in: 1.51.0

ptr\_cast\_constness

pedantic allow

 Applicability: MachineApplicable

Added in: 1.72.0

ptr\_eq

style warn

 Applicability: MachineApplicable

Added in: 1.49.0

ptr\_offset\_with\_cast

complexity warn

 Applicability: MachineApplicable

Added in: 1.30.0

pub\_enum\_variant\_names

deprecated none

 Applicability: Unspecified

Deprecated in: 1.54.0

pub\_underscore\_fields

pedantic allow

 Applicability: Unspecified

Added in: 1.77.0

pub\_use

restriction allow

 Applicability: Unspecified

Added in: 1.62.0

pub\_with\_shorthand

restriction allow

 Applicability: MachineApplicable

Added in: 1.72.0

pub\_without\_shorthand

restriction allow

 Applicability: MachineApplicable

Added in: 1.72.0

question\_mark

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

question\_mark\_used

restriction allow

 Applicability: Unspecified

Added in: 1.69.0

range\_minus\_one

pedantic allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

range\_plus\_one

pedantic allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

range\_step\_by\_zero

deprecated none

 Applicability: Unspecified

Deprecated in: pre 1.29.0

range\_zip\_with\_len

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

rc\_buffer

restriction allow

 Applicability: Unspecified

Added in: 1.48.0

rc\_clone\_in\_vec\_init

suspicious warn

 Applicability: HasPlaceholders

Added in: 1.63.0

rc\_mutex

restriction allow

 Applicability: Unspecified

Added in: 1.55.0

read\_line\_without\_trim

correctness deny

 Applicability: MachineApplicable

Added in: 1.73.0

read\_zero\_byte\_vec

nursery allow

 Applicability: MaybeIncorrect

Added in: 1.63.0

readonly\_write\_lock

perf warn

 Applicability: MaybeIncorrect

Added in: 1.73.0

recursive\_format\_impl

correctness deny

 Applicability: Unspecified

Added in: 1.48.0

redundant\_allocation

perf warn

 Applicability: MaybeIncorrect

Added in: 1.44.0

redundant\_as\_str

complexity warn

 Applicability: MachineApplicable

Added in: 1.74.0

redundant\_async\_block

complexity warn

 Applicability: MachineApplicable

Added in: 1.70.0

redundant\_at\_rest\_pattern

complexity warn

 Applicability: MachineApplicable

Added in: 1.72.0

redundant\_clone

nursery allow

 Applicability: MachineApplicable

Added in: 1.32.0

redundant\_closure

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

redundant\_closure\_call

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

redundant\_closure\_for\_method\_calls

pedantic allow

 Applicability: MachineApplicable

Added in: 1.35.0

redundant\_comparisons

correctness deny

 Applicability: Unspecified

Added in: 1.73.0

redundant\_else

pedantic allow

 Applicability: MachineApplicable

Added in: 1.50.0

redundant\_feature\_names

cargo allow

 Applicability: Unspecified

Added in: 1.57.0

redundant\_field\_names

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

redundant\_guards

complexity warn

 Applicability: MaybeIncorrect

Added in: 1.73.0

redundant\_locals

suspicious warn

 Applicability: Unspecified

Added in: 1.73.0

redundant\_pattern

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

redundant\_pattern\_matching

style warn

 Applicability: MachineApplicable

Added in: 1.31.0

redundant\_pub\_crate

nursery allow

 Applicability: MachineApplicable

Added in: 1.44.0

redundant\_slicing

complexity warn

 Applicability: MachineApplicable

Added in: 1.51.0

redundant\_static\_lifetimes

style warn

 Applicability: MachineApplicable

Added in: 1.37.0

redundant\_test\_prefix

restriction allow

 Applicability: MaybeIncorrect

Added in: 1.88.0

redundant\_type\_annotations

restriction allow

 Applicability: Unspecified

Added in: 1.72.0

ref\_as\_ptr

pedantic allow

 Applicability: MachineApplicable

Added in: 1.78.0

ref\_binding\_to\_reference

pedantic allow

 Applicability: MachineApplicable

Added in: 1.54.0

ref\_option

pedantic allow

 Applicability: Unspecified

Added in: 1.83.0

ref\_option\_ref

pedantic allow

 Applicability: MaybeIncorrect

Added in: 1.49.0

ref\_patterns

restriction allow

 Applicability: Unspecified

Added in: 1.71.0

regex\_creation\_in\_loops

perf warn

 Applicability: Unspecified

Added in: 1.84.0

regex\_macro

deprecated none

 Applicability: Unspecified

Deprecated in: 1.47.0

renamed\_function\_params

restriction allow

 Applicability: Unspecified

Added in: 1.80.0

repeat\_once

complexity warn

 Applicability: MachineApplicable

Added in: 1.47.0

repeat\_vec\_with\_capacity

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.76.0

replace\_consts

deprecated none

 Applicability: Unspecified

Deprecated in: 1.44.0

repr\_packed\_without\_abi

suspicious warn

 Applicability: Unspecified

Added in: 1.85.0

reserve\_after\_initialization

complexity warn

 Applicability: HasPlaceholders

Added in: 1.74.0

rest\_pat\_in\_fully\_bound\_structs

restriction allow

 Applicability: Unspecified

Added in: 1.43.0

result\_filter\_map

complexity warn

 Applicability: MachineApplicable

Added in: 1.77.0

result\_large\_err

perf warn

 Applicability: Unspecified

Added in: 1.65.0

result\_map\_or\_into\_option

style warn

 Applicability: MachineApplicable

Added in: 1.44.0

result\_map\_unit\_fn

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

result\_unit\_err

style warn

 Applicability: Unspecified

Added in: 1.49.0

return\_and\_then

restriction allow

 Applicability: MachineApplicable

Added in: 1.86.0

return\_self\_not\_must\_use

pedantic allow

 Applicability: Unspecified

Added in: 1.59.0

reversed\_empty\_ranges

correctness deny

 Applicability: MaybeIncorrect

Added in: 1.45.0

same\_functions\_in\_if\_condition

pedantic allow

 Applicability: Unspecified

Added in: 1.41.0

same\_item\_push

style warn

 Applicability: Unspecified

Added in: 1.47.0

same\_name\_method

restriction allow

 Applicability: Unspecified

Added in: 1.57.0

search\_is\_some

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

seek\_from\_current

complexity warn

 Applicability: MachineApplicable

Added in: 1.67.0

seek\_to\_start\_instead\_of\_rewind

complexity warn

 Applicability: MachineApplicable

Added in: 1.67.0

self\_assignment

correctness deny

 Applicability: Unspecified

Added in: 1.48.0

self\_named\_constructors

style warn

 Applicability: Unspecified

Added in: 1.55.0

self\_named\_module\_files

restriction allow

 Applicability: Unspecified

Added in: 1.57.0

semicolon\_if\_nothing\_returned

pedantic allow

 Applicability: MachineApplicable

Added in: 1.52.0

semicolon\_inside\_block

restriction allow

 Applicability: MachineApplicable

Added in: 1.68.0

semicolon\_outside\_block

restriction allow

 Applicability: MachineApplicable

Added in: 1.68.0

separated\_literal\_suffix

restriction allow

 Applicability: MachineApplicable

Added in: 1.58.0

serde\_api\_misuse

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

set\_contains\_or\_insert

nursery allow

 Applicability: Unspecified

Added in: 1.81.0

shadow\_reuse

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

shadow\_same

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

shadow\_unrelated

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

short\_circuit\_statement

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

should\_assert\_eq

deprecated none

 Applicability: Unspecified

Deprecated in: pre 1.29.0

should\_implement\_trait

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

should\_panic\_without\_expect

pedantic allow

 Applicability: HasPlaceholders

Added in: 1.74.0

significant\_drop\_in\_scrutinee

nursery allow

 Applicability: MaybeIncorrect

Added in: 1.60.0

significant\_drop\_tightening

nursery allow

 Applicability: MaybeIncorrect

Added in: 1.69.0

similar\_names

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

single\_call\_fn

restriction allow

 Applicability: Unspecified

Added in: 1.72.0

single\_char\_add\_str

style warn

 Applicability: MachineApplicable

Added in: 1.49.0

single\_char\_lifetime\_names

restriction allow

 Applicability: Unspecified

Added in: 1.60.0

single\_char\_pattern

pedantic allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

single\_component\_path\_imports

style warn

 Applicability: MachineApplicable

Added in: 1.43.0

single\_element\_loop

complexity warn

 Applicability: MachineApplicable

Added in: 1.49.0

single\_match

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

single\_match\_else

pedantic allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

single\_option\_map

nursery allow

 Applicability: Unspecified

Added in: 1.86.0

single\_range\_in\_vec\_init

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.72.0

size\_of\_in\_element\_count

correctness deny

 Applicability: Unspecified

Added in: 1.50.0

size\_of\_ref

suspicious warn

 Applicability: Unspecified

Added in: 1.68.0

skip\_while\_next

complexity warn

 Applicability: Unspecified

Added in: 1.42.0

sliced\_string\_as\_bytes

perf warn

 Applicability: MaybeIncorrect

Added in: 1.86.0

slow\_vector\_initialization

perf warn

 Applicability: Unspecified

Added in: 1.32.0

stable\_sort\_primitive

pedantic allow

 Applicability: MachineApplicable

Added in: 1.47.0

std\_instead\_of\_alloc

restriction allow

 Applicability: MachineApplicable

Added in: 1.64.0

std\_instead\_of\_core

restriction allow

 Applicability: MachineApplicable

Added in: 1.64.0

str\_split\_at\_newline

pedantic allow

 Applicability: MaybeIncorrect

Added in: 1.77.0

str\_to\_string

restriction allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

string\_add

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

string\_add\_assign

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

string\_extend\_chars

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

string\_from\_utf8\_as\_bytes

complexity warn

 Applicability: MachineApplicable

Added in: 1.50.0

string\_lit\_as\_bytes

nursery allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

string\_lit\_chars\_any

restriction allow

 Applicability: MachineApplicable

Added in: 1.73.0

string\_slice

restriction allow

 Applicability: Unspecified

Added in: 1.58.0

string\_to\_string

restriction allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

strlen\_on\_c\_strings

complexity warn

 Applicability: MachineApplicable

Added in: 1.55.0

struct\_excessive\_bools

pedantic allow

 Applicability: Unspecified

Added in: 1.43.0

struct\_field\_names

pedantic allow

 Applicability: Unspecified

Added in: 1.75.0

suboptimal\_flops

nursery allow

 Applicability: MachineApplicable

Added in: 1.43.0

suspicious\_arithmetic\_impl

suspicious warn

 Applicability: Unspecified

Added in: pre 1.29.0

suspicious\_assignment\_formatting

suspicious warn

 Applicability: Unspecified

Added in: pre 1.29.0

suspicious\_command\_arg\_space

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.69.0

suspicious\_doc\_comments

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.70.0

suspicious\_else\_formatting

suspicious warn

 Applicability: Unspecified

Added in: pre 1.29.0

suspicious\_map

suspicious warn

 Applicability: Unspecified

Added in: 1.39.0

suspicious\_op\_assign\_impl

suspicious warn

 Applicability: Unspecified

Added in: pre 1.29.0

suspicious\_open\_options

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.77.0

suspicious\_operation\_groupings

nursery allow

 Applicability: MachineApplicable

Added in: 1.50.0

suspicious\_splitn

correctness deny

 Applicability: Unspecified

Added in: 1.54.0

suspicious\_to\_owned

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.65.0

suspicious\_unary\_op\_formatting

suspicious warn

 Applicability: Unspecified

Added in: 1.40.0

suspicious\_xor\_used\_as\_pow

restriction allow

 Applicability: MaybeIncorrect

Added in: 1.67.0

swap\_ptr\_to\_ref

suspicious warn

 Applicability: MachineApplicable

Added in: 1.63.0

swap\_with\_temporary

complexity warn

 Applicability: MachineApplicable

Added in: 1.88.0

tabs\_in\_doc\_comments

style warn

 Applicability: MaybeIncorrect

Added in: 1.41.0

temporary\_assignment

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

test\_attr\_in\_doctest

suspicious warn

 Applicability: Unspecified

Added in: 1.76.0

tests\_outside\_test\_module

restriction allow

 Applicability: Unspecified

Added in: 1.70.0

to\_digit\_is\_some

style warn

 Applicability: MachineApplicable

Added in: 1.41.0

to\_string\_in\_format\_args

perf warn

 Applicability: MachineApplicable

Added in: 1.58.0

to\_string\_trait\_impl

style warn

 Applicability: Unspecified

Added in: 1.78.0

todo

restriction allow

 Applicability: Unspecified

Added in: 1.40.0

too\_long\_first\_doc\_paragraph

nursery allow

 Applicability: MachineApplicable

Added in: 1.82.0

too\_many\_arguments

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

too\_many\_lines

pedantic allow

 Applicability: Unspecified

Added in: 1.34.0

toplevel\_ref\_arg

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

trailing\_empty\_array

nursery allow

 Applicability: Unspecified

Added in: 1.58.0

trait\_duplication\_in\_bounds

nursery allow

 Applicability: MachineApplicable

Added in: 1.47.0

transmute\_bytes\_to\_str

complexity warn

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

transmute\_float\_to\_int

complexity warn

 Applicability: Unspecified

Added in: 1.41.0

transmute\_int\_to\_bool

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

transmute\_int\_to\_char

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

transmute\_int\_to\_float

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

transmute\_int\_to\_non\_zero

complexity warn

 Applicability: Unspecified

Added in: 1.69.0

transmute\_null\_to\_fn

correctness deny

 Applicability: Unspecified

Added in: 1.68.0

transmute\_num\_to\_bytes

complexity warn

 Applicability: Unspecified

Added in: 1.58.0

transmute\_ptr\_to\_ptr

pedantic allow

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

transmute\_ptr\_to\_ref

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

transmute\_undefined\_repr

nursery allow

 Applicability: Unspecified

Added in: 1.60.0

transmutes\_expressible\_as\_ptr\_casts

complexity warn

 Applicability: MachineApplicable

Added in: 1.47.0

transmuting\_null

correctness deny

 Applicability: Unspecified

Added in: 1.35.0

trim\_split\_whitespace

style warn

 Applicability: MachineApplicable

Added in: 1.62.0

trivial\_regex

nursery allow

 Applicability: Unspecified

Added in: pre 1.29.0

trivially\_copy\_pass\_by\_ref

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

try\_err

restriction allow

 Applicability: MachineApplicable

Added in: 1.38.0

tuple\_array\_conversions

nursery allow

 Applicability: Unspecified

Added in: 1.72.0

type\_complexity

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

type\_id\_on\_box

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.73.0

type\_repetition\_in\_bounds

nursery allow

 Applicability: Unspecified

Added in: 1.38.0

unbuffered\_bytes

perf warn

 Applicability: Unspecified

Added in: 1.86.0

unchecked\_duration\_subtraction

pedantic allow

 Applicability: MachineApplicable

Added in: 1.67.0

unconditional\_recursion

suspicious warn

 Applicability: Unspecified

Added in: 1.77.0

undocumented\_unsafe\_blocks

restriction allow

 Applicability: Unspecified

Added in: 1.58.0

unicode\_not\_nfc

pedantic allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

unimplemented

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

uninhabited\_references

nursery allow

 Applicability: Unspecified

Added in: 1.76.0

uninit\_assumed\_init

correctness deny

 Applicability: Unspecified

Added in: 1.39.0

uninit\_vec

correctness deny

 Applicability: Unspecified

Added in: 1.58.0

uninlined\_format\_args

style warn

 Applicability: MachineApplicable

Added in: 1.66.0

unit\_arg

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

unit\_cmp

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

unit\_hash

correctness deny

 Applicability: MaybeIncorrect

Added in: 1.58.0

unit\_return\_expecting\_ord

correctness deny

 Applicability: Unspecified

Added in: 1.47.0

unnecessary\_box\_returns

pedantic allow

 Applicability: Unspecified

Added in: 1.70.0

unnecessary\_cast

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

unnecessary\_clippy\_cfg

suspicious warn

 Applicability: MachineApplicable

Added in: 1.78.0

unnecessary\_debug\_formatting

pedantic allow

 Applicability: Unspecified

Added in: 1.87.0

unnecessary\_fallible\_conversions

style warn

 Applicability: MachineApplicable

Added in: 1.75.0

unnecessary\_filter\_map

complexity warn

 Applicability: Unspecified

Added in: 1.31.0

unnecessary\_find\_map

complexity warn

 Applicability: Unspecified

Added in: 1.61.0

unnecessary\_first\_then\_check

complexity warn

 Applicability: MachineApplicable

Added in: 1.83.0

unnecessary\_fold

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

unnecessary\_get\_then\_check

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.78.0

unnecessary\_join

pedantic allow

 Applicability: MachineApplicable

Added in: 1.61.0

unnecessary\_lazy\_evaluations

style warn

 Applicability: MachineApplicable

Added in: 1.48.0

unnecessary\_literal\_bound

pedantic allow

 Applicability: MachineApplicable

Added in: 1.84.0

unnecessary\_literal\_unwrap

complexity warn

 Applicability: MachineApplicable

Added in: 1.72.0

unnecessary\_map\_on\_constructor

complexity warn

 Applicability: MachineApplicable

Added in: 1.74.0

unnecessary\_map\_or

style warn

 Applicability: MachineApplicable

Added in: 1.84.0

unnecessary\_min\_or\_max

complexity warn

 Applicability: MachineApplicable

Added in: 1.81.0

unnecessary\_mut\_passed

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

unnecessary\_operation

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

unnecessary\_owned\_empty\_strings

style warn

 Applicability: MachineApplicable

Added in: 1.62.0

unnecessary\_result\_map\_or\_else

suspicious warn

 Applicability: MachineApplicable

Added in: 1.78.0

unnecessary\_safety\_comment

restriction allow

 Applicability: Unspecified

Added in: 1.67.0

unnecessary\_safety\_doc

restriction allow

 Applicability: Unspecified

Added in: 1.67.0

unnecessary\_self\_imports

restriction allow

 Applicability: MaybeIncorrect

Added in: 1.53.0

unnecessary\_semicolon

pedantic allow

 Applicability: MachineApplicable

Added in: 1.86.0

unnecessary\_sort\_by

complexity warn

 Applicability: MachineApplicable

Added in: 1.46.0

unnecessary\_struct\_initialization

nursery allow

 Applicability: MachineApplicable

Added in: 1.70.0

unnecessary\_to\_owned

perf warn

 Applicability: MachineApplicable

Added in: 1.59.0

unnecessary\_unwrap

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

unnecessary\_wraps

pedantic allow

 Applicability: MaybeIncorrect

Added in: 1.50.0

unneeded\_field\_pattern

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

unneeded\_struct\_pattern

style warn

 Applicability: MachineApplicable

Added in: 1.86.0

unneeded\_wildcard\_pattern

complexity warn

 Applicability: MachineApplicable

Added in: 1.40.0

unnested\_or\_patterns

pedantic allow

 Applicability: MachineApplicable

Added in: 1.46.0

unreachable

restriction allow

 Applicability: Unspecified

Added in: 1.40.0

unreadable\_literal

pedantic allow

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

unsafe\_derive\_deserialize

pedantic allow

 Applicability: Unspecified

Added in: 1.45.0

unsafe\_removed\_from\_name

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

unsafe\_vector\_initialization

deprecated none

 Applicability: Unspecified

Deprecated in: pre 1.29.0

unseparated\_literal\_suffix

restriction allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

unsound\_collection\_transmute

correctness deny

 Applicability: Unspecified

Added in: 1.40.0

unstable\_as\_mut\_slice

deprecated none

 Applicability: Unspecified

Deprecated in: pre 1.29.0

unstable\_as\_slice

deprecated none

 Applicability: Unspecified

Deprecated in: pre 1.29.0

unused\_async

pedantic allow

 Applicability: Unspecified

Added in: 1.54.0

unused\_collect

deprecated none

 Applicability: Unspecified

Deprecated in: 1.39.0

unused\_enumerate\_index

style warn

 Applicability: MachineApplicable

Added in: 1.75.0

unused\_format\_specs

complexity warn

 Applicability: MaybeIncorrect

Added in: 1.66.0

unused\_io\_amount

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

unused\_peekable

nursery allow

 Applicability: Unspecified

Added in: 1.65.0

unused\_result\_ok

restriction allow

 Applicability: MaybeIncorrect

Added in: 1.82.0

unused\_rounding

nursery allow

 Applicability: MachineApplicable

Added in: 1.63.0

unused\_self

pedantic allow

 Applicability: Unspecified

Added in: 1.40.0

unused\_trait\_names

restriction allow

 Applicability: MachineApplicable

Added in: 1.83.0

unused\_unit

style warn

 Applicability: MachineApplicable

Added in: 1.31.0

unusual\_byte\_groupings

style warn

 Applicability: MaybeIncorrect

Added in: 1.49.0

unwrap\_in\_result

restriction allow

 Applicability: Unspecified

Added in: 1.48.0

unwrap\_or\_default

style warn

 Applicability: MachineApplicable

Added in: 1.56.0

unwrap\_used

restriction allow

 Applicability: Unspecified

Added in: 1.45.0

upper\_case\_acronyms

style warn

 Applicability: MaybeIncorrect

Added in: 1.51.0

use\_debug

restriction allow

 Applicability: Unspecified

Added in: pre 1.29.0

use\_self

nursery allow

 Applicability: MachineApplicable

Added in: pre 1.29.0

used\_underscore\_binding

pedantic allow

 Applicability: Unspecified

Added in: pre 1.29.0

used\_underscore\_items

pedantic allow

 Applicability: Unspecified

Added in: 1.83.0

useless\_asref

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

useless\_attribute

correctness deny

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

useless\_conversion

complexity warn

 Applicability: MachineApplicable

Added in: 1.45.0

useless\_format

complexity warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

useless\_let\_if\_seq

nursery allow

 Applicability: HasPlaceholders

Added in: pre 1.29.0

useless\_nonzero\_new\_unchecked

complexity warn

 Applicability: MachineApplicable

Added in: 1.86.0

useless\_transmute

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

useless\_vec

perf warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

vec\_box

complexity warn

 Applicability: Unspecified

Added in: 1.33.0

vec\_init\_then\_push

perf warn

 Applicability: HasPlaceholders

Added in: 1.51.0

vec\_resize\_to\_zero

correctness deny

 Applicability: MaybeIncorrect

Added in: 1.46.0

verbose\_bit\_mask

pedantic allow

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

verbose\_file\_reads

restriction allow

 Applicability: Unspecified

Added in: 1.44.0

waker\_clone\_wake

perf warn

 Applicability: MachineApplicable

Added in: 1.75.0

while\_float

nursery allow

 Applicability: Unspecified

Added in: 1.80.0

while\_immutable\_condition

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

while\_let\_loop

complexity warn

 Applicability: HasPlaceholders

Added in: pre 1.29.0

while\_let\_on\_iterator

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

wildcard\_dependencies

cargo allow

 Applicability: Unspecified

Added in: 1.32.0

wildcard\_enum\_match\_arm

restriction allow

 Applicability: MaybeIncorrect

Added in: 1.34.0

wildcard\_imports

pedantic allow

 Applicability: MachineApplicable

Added in: 1.43.0

wildcard\_in\_or\_patterns

complexity warn

 Applicability: Unspecified

Added in: 1.42.0

write\_literal

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

write\_with\_newline

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

writeln\_empty\_string

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

wrong\_pub\_self\_convention

deprecated none

 Applicability: Unspecified

Deprecated in: 1.54.0

wrong\_self\_convention

style warn

 Applicability: Unspecified

Added in: pre 1.29.0

wrong\_transmute

correctness deny

 Applicability: Unspecified

Added in: pre 1.29.0

zero\_divided\_by\_zero

complexity warn

 Applicability: Unspecified

Added in: pre 1.29.0

zero\_prefixed\_literal

complexity warn

 Applicability: MaybeIncorrect

Added in: pre 1.29.0

zero\_ptr

style warn

 Applicability: MachineApplicable

Added in: pre 1.29.0

zero\_repeat\_side\_effects

suspicious warn

 Applicability: Unspecified

Added in: 1.79.0

zero\_sized\_map\_values

pedantic allow

 Applicability: Unspecified

Added in: 1.50.0

zombie\_processes

suspicious warn

 Applicability: MaybeIncorrect

Added in: 1.83.0

zst\_offset

correctness deny

 Applicability: Unspecified

Added in: 1.41.0
