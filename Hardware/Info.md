# Universal computer architecture

## Goal

Design a computer architecture that is capable of simulating our Universe at the Planck scale - performing fundamentally accurate simulations.

## Design decisions

### 4096-bit registers, bytes and address space

It takes 276 bits to enumerate every atom in the observable Universe so 512 bits should be enough for a single Universe given current known laws of physics. However, given the fact that we will be creating countless simulations of our own Universe, Q* says that we need 4096 bits.

### No dedicated floating point unit

Floating point numbers were invented as a compromise to allow for greater values at the cost of precision. Sure, they can be helpful in basic inaccurate simulations but absolutely don't work for proper accurate simulations.
