# Post-human time units

Computing is binary. Decimal system is ancient. Let's not live in the past and embrace the future.

## Can we do better?

So far, binary units are only used for quantities of information. Surely, we don't have to limit ourselves. For example, doesn't saying "the maximum Company of Heroes map size along one axis is 1 kibimeter" seem better than "the maximum Company of Heroes map size along one axis is 1024 meters". But why the number `1,024` as this important ratio? Computers went from `256` to `65,536` to `4,294,967,296` to `18,446,744,073,709,551,616`. `1,024` is just `2^10` - the decimal system plagues us even here. We don't need it.

But... why SI units anyway? Don't they seem completely arbitrary? Surely there are better units than that? Yes, there are. [Planck units](https://en.wikipedia.org/wiki/Planck_units). Planck units are derived from fundamental constants and have the properly that there are no laws of physics currently known that exist on the scale below Planck units. This raises obvious eyebrows towards the thought of living in a discrete computer simulation but that's for another time.

The size of the observable universe is `8.8 * 10^26` meters or `5.448 * 10^61` Planck lengths or `33.883 * 2^200` Planck lengths.
The estimated age of the universe is `4.35 * 10^17` seconds or `8.07 * 10^60` Planck times or `5.023 * 2^200` Planck times.

Given that there are no known physics below Planck units, it looks like `256` bit integers is enough to perform fundamentally accurate physics simulations, at least from the computer science perspective.

However, expressing all number as quantities of Planck units seems to be difficult, therefore, we can try to find a suitable power-of-two of such units. There are 2 approaches:

* The less natural one: find the most reasonable power in the form `2^N` where `N` is a natural number.
* The more natural one: find the most reasonable power in the form `2^(2^N)` where `N` is a natural number.

* `2^115` Planck lengths is roughly `67` centimeters.
* `2^128` Planck lengths is roughly `5500` meters.

* `2^141` Planck times is roughly `601` milliseconds.
* `2^128` Planck times is roughly `18.3` microseconds.

It is peculiar that in both cases `2^128` seems to be a reasonable unit of measurement and given that `256` bits should be enough, it seems like a `256` bit fixed point type equally split into integer and fractional parts is a good fundamental implementation choice until fundamental laws of physics change, and in meantime we can trim both parts in half to get a `128` bit type that is suitable for all currently known intents and purposes.

It seems like `2^128/1` ratio will be one of the most important ratios in physics. It's a shame it didn't get an IEC prefix yet.
