# Apuntes de FoxDot
Traducción parcial de la documentación de [FoxDot](http://foxdot.org/): Live Coding con [Python](https://www.python.org/) & [SuperCollider](https://supercollider.github.io/), realizado por [Qirky](https://github.com/Qirky).

(en proceso)

## SynthDefs
`print(SynthDefs)`

sawbass karp gong varsaw bell scratch pulse audioin blip pads rave donk saw orient creep growl marimba razz dub arpy ambi viola piano quin crunch noise star bass dab dirt twang swell pluck glass soprano charm spark bug squish sitar zap snick play2 play1 prophet ripple fuzz lazer klank nylon soft scatter loop

## Escalas
`print(Scale.names())`

chromatic dorian dorian2 egyptian freq harmonicMajor harmonicMinor indian justMajor justMinor locrian locrianMajor lydian lydianMinor major majorPentatonic melodicMinor minor minorPentatonic mixolydian phrygian prometheus ryan zhi

## Efectos/ Atributos
`print(Player.get_attributes())`

degree oct freq dur delay buf blur amplify scale bpm sample env sus fmod pan rate amp midinote channel vib vibdepth slide sus slidedelay slidefrom bend benddelay coarse pshift hpr hpf lpf lpr swell bpr bpnoise bpf crush bits amp dist chop decay echo spin cut mix room formant shape

Effects are added to Player objects as keywords instructions like `dur` or `amp` but are a little more tricky. Each effect has a "title" keyword, which requires a nonzero value to add the effect to a Player. Effects also have other attribute keywords which can be any value and may have a default value which is set when a Player is created.

- *High Pass Filter* - Title keyword: `hpf`, Attribute keyword(s): `hpr` Only frequences above the value of `hpf` are kept in the final signal. Use `hpr` to set the resonance (usually a value between 0 and 1)

- *Low Pass Filter* - Title keyword: `lpf`, Attribute keyword(s): `lpr` Only frequences below the value of `lpf` are kept in final signal. Use `lpr` to set the resonance (usually a value between 0 and 1)

 - *Bitcrush* - Title keyword: `bits`, Attribute keyword(s): `crush` The bit depth, in number of bits, that the signal is reduced to; this is a value between 1 and 24 where other values are ignored. Use crush to set the amount of reduction to the bitrate (defaults to 8)

- *Reverb* - Title keyword: `room`, Attribute keyword(s): `mix` The room argument specifies the size of the room and mix is the dry/wet mix of reverb; this should be a value between 0 and 1 (defalts to 0.25)

 - *Chop* - Title keyword: `chop`, Attribute keyword(s): `sus` 'Chops'` the signal into chunks using a low frequency pulse wave over the sustain of a note.

 - *Slide To* - Title keyword: `slide`, Attribute keyword(s): `Slides'` the frequency value of a signal to freq * (slide+1) over the duration of a note (defaults to 0)

 - *Slide From* - Title keyword: `slidefrom`, Attribute keyword(s): `Slides'` the frequency value of a signal from freq * (slidefrom) over the duration of a note (defaults to 1)

- *Comb delay* (echo) - Title keyword: `echo`, Attribute keyword(s): `decay` Sets the decay time for any echo effect in beats, works best on Sample Player (defaults to 0)

- *Panning* - Title keyword: `pan`, Attribute keyword(s): `Panning`, where -1 is far left, 1 is far right (defaults to 0)

- *Vibrato* - Title keyword: `vib`, Attribute keyword(s): `Vibrato` (defaults to 0)

Undocumented: Spin, Shape, Formant, BandPassFilter, Echo

## Funciones

### P10(n)
Devuelve un patrón de **longitud n** de una serie generada aleatoriamente de 1 y 0.

ej. `P10(3)` -> `P[0, 0, 1]

### PAlt(pat1, pat2, *patN)
Devuelve un patrón generado alternando los valores de las secuencias dadas.

ej. `PAlt((1,2,3),(0,1,3))` -> `P[P(1, 2, 3), P(0, 1, 3)]`

### PDelay(*args)
None

### PDur(n, k, start=0, dur=0.25)
Devuelve las duraciones basadas en los ritmos euclidianos (ver `PEuclid`) donde **dur** es la longitud de cada paso (*step*).

ej.  `PDur(3, 8)` -> `P[0.75, 0.75, 0.5]`

### PEuclid(n, k)
Returns the Euclidean rhythm which spreads 'n' pulses over 'k' steps as evenly as possible.
Devuelve el ritmo euclidiano que extiende 'n' pulsos sobre 'k' pasos lo más uniformemente posible. 

ej. `PEuclid(3, 8)` -> `P[1, 0, 0, 1, 0, 0, 1, 0]`

### PPairs(seq, func=<lambda>)
Laces a sequence with a second sequence obtained by performing a function on the original. By default this is lambda n: 8 - n.

### PQuicken(dur=0.5, stepsize=3, steps=6)
None

### PRange(start, stop=None, step=None)
Devuelve un patrón equivalente a `Pattern(range(start, stop, step))`

ej. `PRange(0,4)` -> `P[0, 1, 2, 3]`

### PRhythm(durations)
[1,(3,8)] -> [(1,2.75,3.5),2] work in progress

### PShuf(seq)
PShuf(seq) -> Returns a shuffled version of seq

### PSine(n=16)
Returns values of one cycle of sine wave split into 'n' parts
Devuelve los valores de un ciclo de onda sinusoidal dividida en 'n' partes.

ej. `PSine(3)` -> `P[0.0, 0.8660254037844387, -0.8660254037844384]`

### PSq(a=1, b=2, c=3)
Returns a Pattern

ej. `PSq(1,5,7)` -> `P[1, 32, 243, 1024, 3125, 7776, 16807]`

### PStep(n, value, default=0)
Returns a Pattern that every n-term is 'value' otherwise 'default'

### PStretch(seq, size)
Returns 'seq' as a Pattern and looped until its length is 'size'.

ej. `PStretch([0,1,2], 5)` -> `P[0, 1, 2, 0, 1]`

### PStutter(x, n=2)
PStutter(seq, n) -> Creates a pattern such that each item in the array is repeated n times (n can be a pattern)

### PSum(n, total, **kwargs)
Returns a Pattern of length 'n' that sums to equal 'total'

ej. `PSum(3,8) -> P[3, 3, 2]`; `PSum(5,4) -> P[1, 0.75, 0.75, 0.75, 0.75]`

### PTri(start, stop=None, step=None)
Devuelve un patrón equivalente a `Pattern(range(start, stop, step))` con su forma invertida añadida.

ej. `PTri(4)` -> `P[0, 1, 2, 3, 4, 3, 2, 1]`

### PZip(pat1, pat2, *patN)
Crea un *pattern* que agrupa como una cremallera (*zips*) varios *patterns*. 

ej. `PZip([0,1,2], [3,4])` -> `P[(0, 3), (1, 4), (2, 3), (0, 4), (1, 3), (2, 4)]`

### PZip2(pat1, pat2, rule=<lambda>)
Como PZip pero sólo con dos *patterns*. Agrupa los valores si cumplen la condición (*rule*).

## Classes
`PGroupDiv(self, *args, **kwargs)`

Stutter every other request

Methods

### __getitem__(self, key)
Overrides the Pattern.getitem to allow indexing by TimeVar and PlayerKey instances.

### __invert__(self)
Using the ~ symbol as a prefix to a Pattern will reverse it.

`a = P[:4] print(a, ~a) P[0, 1, 2, 3], P[3, 2, 1, 0]`

### __iter__(self)
Returns a generator object for this Pattern

### __len__(self)
Returns the *expanded" length of the pattern. e.g. the following are identical.

>>> print( len(P[0,1,2,[3,4]]) )
8
>>> print( len(P[0,1,2,3,0,1,2,4]) )
8

### __or__(self, other)
Use the '|' symbol to 'pipe' Patterns into on another

### __ror__(self, other)
Use the '|' symbol to 'pipe' Patterns into on another

### __setslice__(self, i, j, item)
Only works in Python 2

### accum((((('self',),),),), (((('n', None), None), None), None)=None)
Returns a Pattern that is equivalent to list of sums of that Pattern up to that index.

### all(self, func=<lambda>)
Returns true if all of the patterns contents satisfies func(x) - default is nonzero

### amen(self, size=2)
Merges and laces the first and last two items such that a drum pattern "x-o-" would become "(x[xo])-o([-o]-)"

### asGroup(self)
Returns the Pattern as a PGroup

### choose(self)
Returns one randomly selected item

### contains_nest(self)
Returns true if the pattern contains a nest

### copy(self)
Returns a copy of the Pattern such that alterations to the Pattern.data do not affect the original.

### count(self, item)
Returns the number of occurrences of item in the Pattern

### deep_shuffle(self, n=1)
Returns a new Pattern with shuffled contents and shuffles any nested patterns. To shuffle the contents of nested patterns with the rest 

of the Pattern's contents, use true_shuffle.

### every(self, n, method, *args, **kwargs)
Returns the pattern looped n-1 times then appended with the version returned when method is called on it.

### flatten(self)
Returns a nested PGroup as un-nested e.g.

>>> `P(0,(3,5)).flatten()` -> `P(0, 3, 5)`

### get_behaviour(self)
Returns a function that modulates a player event dictionary

### getitem(self, key)
Is called by getitem

### group(self)
Returns the Pattern as a PGroup

### invert(self)
Inverts the values with the Pattern.

### items(self)
Returns a generator object equivalent to using enumerate()

### layer(self, method, *args, **kwargs)
Zips a pattern with a modified version of itself. Method argument can be a function that takes this pattern as its first argument, or 

the name of a Pattern method as a string.

### limit((((('self',),),),), (((('func',),),),), (((('value',),),),))
Returns a new Pattern generated by adding elements from this Pattern to a new list and repeatedly calling func() on this list until 

func(l) is greater than value e.g.

`print( P[0, 1, 2, 3].limit(sum, 10) )` -> `P[0, 1, 2, 3, 0, 1, 2]`

### loop((((('self',),),),), (((('n',),),),))
Repeats this pattern n times

### make(self)
This method automatically laces and groups the data

### merge(self, value)
Merge values into one PGroup

### mirror(self)
Reverses the pattern. Differs to Pattern.reverse() in that all nested patters are also reversed.

### normalise(self)
Returns the pattern with all values between 0 and 1

### palindrome((((('self',),),),), (((('a', 0), 0), 0), 0)=0, (((('b', None), None), None), None)=None)
Returns the original pattern with mirrored version of itself appended. 
- removes values from the middle of the pattern, if positive.
- removes values from the end of the pattern, should be negative.

ej.
`P[:4].palindrome()` -> `P[0, 1, 2, 3, 3, 2, 1, 0]` 
`P[:4].palindrome(1)` -> `P[0, 1, 2, 3, 2, 1, 0]`
`P[:4].palindrome(-1)` -> `P[0, 1, 2, 3, 3, 2, 1]`
`P[:4].palindrome(1,-1)` -> `P[0, 1, 2, 3, 2, 1]`

### pipe(self, pattern)
Concatonates this patterns stream with another

### pivot((((('self',),),),), (((('i',),),),))
Mirrors and rotates the Pattern such that the item at index 'i' is in the same place

### replace(self, sub, repl)
Replaces any occurrences of "sub" with "repl"

### reverse(self)
Reverses the contents of the Pattern. Nested patterns are not reversed. To reverse the contents of nester patterns use Pattern.mirror()

### sample((((('self',),),),), (((('n',),),),))
Returns an n-length pattern from a sample

### shuffle(self, n=1)
Returns a new Pattern with shuffled contents. Note: nested patterns stay together. To shuffle the contents of nested patterns, use 

deep_shuffle or true_shuffle.

### shufflets(self, n)
Returns a Pattern of 'n' number of PGroups made from shuffled versions of the original Pattern

### sort(self)
Used in place of sorted(pattern) to force type

### splice(self, seq, *seqs)
Takes at least list / Pattern and creates a new Pattern by adding a value from each pattern in turn to the new pattern. e.g.

`P[0,1,2,3].splice([4,5,6,7],[8,9])` -> `P[0,4,8,1,5,9,2,6,8,3,7,9]`

### stretch((((('self',),),),), (((('size',),),),))
Stretches (repeats) the contents until len(Pattern) == size

### string(self)
Returns a PlayString in string format from the Patterns values

### stutter(self, n=2)
Returns a new Pattern with each item repeated by n. Use a list of numbers for stutter different items by different amount. e.g.

`P[0, 1, 2, 3].stutter([1,3])` -> `P[0, 1, 1, 1, 2, 3, 3, 3]`

### true_copy(self, new_data=None)
Returns a copy of the Pattern such that items within the Pattern hold the same state as the original.

### true_shuffle(self, n=1)
Returns a new Pattern with completely shuffle contents such that nested Patterns are shuffled within the larger Pattern

### unduplicate(self)
Removes any consecutive duplicate numbers from a Pattern

### zip(self, other)
Returns a Pattern of PGroups, where each PGroup contains the i-th element from each of the argument sequences. The length of the pattern is the lowest common multiple of the lengths of the two joining patterns.
