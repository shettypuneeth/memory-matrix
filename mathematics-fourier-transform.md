# Fourier Transform

Fourier transform turns a function of time, usually intensity over time, to function of frequency.

- Lets us pull out the constituent frequencies that make up a given signal.
- One practical application of this we see everywhere is noise cancellation or signal filtering.
- A way to achieve that would be,
  - Consider the signal coming in at various intensities over time. The sound encoded in the form of varying voltages, from one millisecond to the next. A high pitched sound is nothing but a signal with a high frequency, so in essence what we want is to identify this frequency and flatten it out.
  - So we take the Fourier transform of the original signal to get it's frequency graph and the high pitch can be identified as a spike at some high frequency on the frequency graph.
  - Once we flatten out the spike, what we are left with is the FT of a signal which is very much similar to the FT original signal but without the high pitch sound.
  - Taking the inverse FT of this signal would give us the original signal with the high pitched filtered out.
