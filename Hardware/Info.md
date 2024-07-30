# Universal computer architecture

## Goal

Design a computer architecture that is capable of simulating our Universe at the Planck scale - performing fundamentally accurate simulations.

## Design decisions

### 512-bit registers and address space

It takes 276 bits to enumerate every atom in the observable Universe so 512-bits should be enough given current known laws of physics. So we start with 512-bit and expand it if we discover something new later.

### No dedicated floating point unit

Floating point numbers were invented as a compromise to allow for greater values at the cost of precision. Sure, they can be helpful in basic inaccurate simulations but absolutely don't work for proper accurate simulations.
