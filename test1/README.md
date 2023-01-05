# Reproducing the Documentation Demo
In this test of circom, I reproduce the demo of the Documentation. It involves writing a template which contains the input and output signals of a circuit followed by the computations on the input signal which eventually lead to the output signal.

## Stack used
1. Windows Subsystem Linux
2. Circom 2.0
3. SnarkJS

## Observations
The following observations were made while trying this demo out:
- Consider the circuit as a black-box. Input signals feed into the black box and output signals come out of it.
- Templates are to Components what Classes are to Object in OOP
- General convention when declaring signals is `signal <input/output> <identifier>` for eg, `signal input a;` will define an input signal `a` while `signal output out[N]` will define an output `out` which is an array of `N` elements
- All signals in a template are private
- To make a circuit, create a Component from a template by `component <component name> <(optional) define viewing scope of the signals> = <template name>` for eg, `component main {public [in1, in2]} = Multiplier()` would define a circuit called `main` from the `Multiplier()` template which has two public inputs `in1` and `in2`. If template `Multipler()` has other input signals within it then they will be considered as private
- templates can be nested inside templates by creating component of the template to be nested inside the template which should nest it
- let's say that `c1` is a component inside a template `t1` and `c1` contains an input signal `a`. Then `c1.a <== t1.in1` will generate a constraint and assign `in1` to `a` where `in1` is the input signal of `t1`

- `circom` is used for writing the circuit, compiling the circuit and computing a witness from a user provided `input.json` file. This would generate a binary encoded Witness file with extension `.wtns` which will be used in `snarkjs` to create the proofs.

- In our circuit, we try to factorize 33 and prove that we know two number which can be multiplied to obtain 33