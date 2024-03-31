---
title: 'Superposition'
date: 2024-03-31
permalink: /posts/2024/03/superposition/
tags:
  - quantum
  - superposition
---

What is superposition? And how can something be in two states at the same time?

# Introduction
One thing that can be really confusing is the notion of a qubit being in a superposition of states. After all, how can something be in two states at the same time? It's not like a coin can be both heads and tails at the same time, right?

The closest we can get to that is by spinning the coin, and while it's spinning, it's neither heads nor tails. And as soon as it lands, it's either heads or tails.
But that's different from the coin being in both states at the same time - it's just the coin spinning back and forth between heads and tails and us not knowing which state it's in until we look at it.

In this article we'll see mathematically why it's the case the superposition is different from mere uncertainty about which state a qubit is in.
But before we get there, we'll have to talk about measurement and different bases.

# Basis States
A qubit is always in a state of superposition, even if we know it's in a certain state, say, $\ket{0}$.
We just have to be a bit more specific about what kind of superposition we're talking about.
In this case, if we measure a qubit and find it's in state $\ket{0}$ we can say that in terms of the _computational basis_ it's not in superposition, but it is in a superposition in _other_ measurement bases.
To see why that is the case, take a look at the Bloch sphere below.

<center>
<a title="Smite-Meister, CC BY-SA 3.0 &lt;https://creativecommons.org/licenses/by-sa/3.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Bloch_sphere.svg"><img width="512" alt="Bloch sphere" src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6b/Bloch_sphere.svg/725px-Bloch_sphere.svg.png"></a>
</center>

What is most often referred to as a superposition, is a superposition between the states $\ket{0}$ and $\ket{1}$, which are the basis states in the computational basis.
So for example taking a qubit in the state $\ket{0}$ and applying the Hadamard gate to it, rotates the state vector around the y-axis by $\theta=\frac{\pi}{2}$, which brings it into the state $\ket{+}=\frac{\ket{0} + \ket{1}}{\sqrt{2}}$.
That is, the state of the qubit is now in equal superposition between the states $\ket{0}$ and $\ket{1}$.

But the $\ket{0}$ and $\ket{1}$ states are not the only basis states. There are infinitely many basis states, and we can always express the state of a qubit in terms of a superposition of these basis states.
There are three requirements for a set of basis states to be considered a basis.
The first is that they are **orthogonal**. They appear spatially parallel on the Bloch sphere (e.g. the "up" and "down" states $\ket{0}$ and $\ket{1}$, but they are geometrically orthogonal to each other.
Two other features of basis states are that they are **complete** in the sense that they span the entire space of possible states and that they are **normalised** (i.e. the inner product of a basis states with itself is 1, to ensure we get valid probabilities).
To see that for example the basis states $\ket{0}$ and $\ket{1}$ are complete and normalised, consider that you can reach any point on the Bloch Sphere by choosing appropriate $\theta$ and $\phi$ angles.

So what are the different bases we typically encounter in quantum computing?
- First of all there is computational basis, or z-basis with basis states
  - $\ket{0}$
  - $\ket{1}$
- Then there is the Hadamard basis, or x-basis. One way to get to these states from $\ket{0}$, as we have seen, is to rotate around the y-axis:
  - $\ket{+} = \frac{\ket{0} + \ket{1}}{\sqrt{2}}$
  - $\ket{-} = \frac{\ket{0} - \ket{1}}{\sqrt{2}}$
- And finally there is the y-basis, which you get to from, say, $\ket{0}$, by rotating around the x-axis:
  - $\ket{i} = \frac{\ket{0} + i\ket{1}}{\sqrt{2}}$
  - $\ket{-i} = \frac{\ket{0} - i\ket{1}}{\sqrt{2}}$

Of course we can also rewrite the computational basis vectors in terms of other basis states like the Hadamard basis states:
- $\ket{0} = \frac{\ket{+} + \ket{-}}{\sqrt{2}}$
- $\ket{1} = \frac{\ket{+} - \ket{-}}{\sqrt{2}}$

which is a way of saying that the computational basis states are a superposition of the Hadamard basis states as claimed above.

As you can see, any point on the Bloch Sphere can be expressed in any of these, or other, bases. And that's why a qubit is always in a state of superposition _in some basis_, even if we know it's in a certain state in the computational basis, say, $\ket{0}$.

States vectors in the computational basis are just kets with a 1 in the position of the state and 0s elsewhere: $\ket{0} = \begin{bmatrix} 1 \cr 0 \end{bmatrix}$ and $\ket{1} = \begin{bmatrix} 0 \cr 1 \end{bmatrix}$.
The three conditions for basis vectors mentioned above can then be expressed as follows:
- **orthogonality**: $\braket{0\|1} = \braket{1\|0} = 0$
- **normality**: $\braket{0\|0} = \braket{1\|1} = 1$
- **completeness**: $\psi = \begin{bmatrix} \psi_{1} \cr \psi_{2} \end{bmatrix} = \psi_{1}\ket{0} + \psi_{2}\ket{1}$

With the definition of an arbitratry quantum state $\psi = \begin{bmatrix} \psi_{1} \cr \psi_{2} \end{bmatrix}$ in place, we can see that the inner product of it with a basis state gives us a measure for how similar it is to that basis state.
That is, $\braket{0|\psi} = \psi_{1}\braket{0|0} + \psi_{2}\braket{0|1} = \psi_{1}$, and $\braket{1|\psi} = \psi_{1}\braket{1|0} + \psi_{2}\braket{1|1} = \psi_{2}$.

If we make the assumption that the normalization condition also holds for any arbitrary state, in other words, that any linear combination of basis states leads to a pure state - a state on the surface of the Bloch sphere, we obtain $\braket{\psi\|\psi} = \|\psi_{1}\|^{2} + \|\psi_{2}\|^{2} = 1$.

Substituting the expressions for $\psi_{1}$ and $\psi_{2}$ from above, we get 

\$\$
\braket{\psi|\psi} = |\braket{0|\psi}|^{2} + |\braket{1|\psi}|^{2} = \psi_{1}^{2} + \psi_{2}^{2} = 1
\$\$

which basically yields the Born Rule.
This expression tells us that projecting an arbitrary state vector onto a basis state not only gives us a measure of how similar the state is to the basis state.
It also gives us something called the **probability amplitudes** $\psi_{1}$ and $\psi_{2}$, which, when squared, give us the probabilities of observing either state $\ket{0}$ or $\ket{1}$ when measuring the state $\psi$ in the computational basis.

# Measurement

So far we've seen what basis states are mathematically and in terms of the Bloch Sphere.
Let's now see how to set up an experiment to measure a qubit in a certain basis.

There are 2 parts to explaining measurement in quantum mechanics: running experiments and see what actually happens and the mathematical formalism that describes what happens.
For the first part, it's instructive to learn about the [Stern-Gerlach experiments](https://en.wikipedia.org/wiki/Stern%E2%80%93Gerlach_experiment).
One could write an entire article about these experiments, but we'll focus on only a few aspects here.
<center>
<a title="Tatoute, CC BY-SA 4.0 &lt;https://creativecommons.org/licenses/by-sa/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Stern-Gerlach_experiment_svg.svg"><img width="1024" alt="Stern-Gerlach experiment svg" src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ee/Stern-Gerlach_experiment_svg.svg/1024px-Stern-Gerlach_experiment_svg.svg.png"></a>
</center>
The gist of the experiment is that we shoot a beam of silver atoms (2) through a magnetic field (3), and then we measure the deflection of the atoms on a screen (5).
What we're really measuring here is the spin of the atom.
Depending on the spin of the atom, it gets deflected either up or down when it goes through the magnetic field.
Before measurement it can point in any direction, but after measurement (after we observe it on the screen) always either points up or down.
The up and down states are the basis states of the computational basis/ z-axis.

This result is different than if we were to run it with a classical object, like a magnet, which can point in any direction just like the spin of an atom.
If we were to shoot a magnet with a random orientation through the magnetic field, it would get deflected in proportion to its orientation.
And if we were to repeat this experiment many times, we would see a continuous distribution of deflections on the screen (4).
The silver atom however, being a quantum object, always gets deflected either up or down, and never in between.

Before measurement, the state of the atom, it's spin, is in a random superposition of the up and down states.
But after measurement, the state of the atom is either up or down.
So it is in a definite state, not in a superposition anymore, in the computational basis.
This result is what is meant when one says that the act of measuring a qubit alters its state.
One can verify that the atom is really not in a superposition anymore by letting it pass through another Stern-Gerlach apparatus after it got deflected up:
If the second apparatus is oriented in the same direction as the first one (i.e. we measure in the computational basis again), and we take an atom that got deflected **up** by the first apparatus, it will get deflected **up** again by the second apparatus.

<center>
<a title="MJasK, CC BY-SA 4.0 &lt;https://creativecommons.org/licenses/by-sa/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Stern-Gerlach_Analyzer_Sequential_Series_E1.png"><img width="1024" alt="Stern-Gerlach Analyzer Sequential Series E1" src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/64/Stern-Gerlach_Analyzer_Sequential_Series_E1.png/1024px-Stern-Gerlach_Analyzer_Sequential_Series_E1.png"></a>
</center>
<br>

But it's not just that the apparatus filtered out the atoms that were in the down state.
There is another variant of this experiment which adds a second apparatus that is rotated by 90 degrees, effectively measuring the spin of the atom in the x-basis now.
Behind that second apparatus is a third one which again measures the spin in the z-basis.

The interesting result here is that when we measure the spin of the atom (which we measured to be the in the **up** state according to the first apparatus) in the x-bases, it seems to "reset" the state of the atom along the z-axis.
We know this, because when we measure the spin of the atom in the z-basis for the second time (after having measured in the x-basis), we no longer have a 100% chance of finding the atom in the **up** state.
Instead we again find that the atom is in an equal superposition of the up and down states.
<center>
<a title="MJasK, CC BY-SA 4.0 &lt;https://creativecommons.org/licenses/by-sa/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Stern-Gerlach_Analyzer_Sequential_Series_E3.png"><img width="1024" alt="Stern-Gerlach Analyzer Sequential Series E3" src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/cb/Stern-Gerlach_Analyzer_Sequential_Series_E3.png/1024px-Stern-Gerlach_Analyzer_Sequential_Series_E3.png"></a>
</center>
<br>


One finding of the SG experiments is that we can never know both the spin of an atom in the x-basis and the z-basis (or any other basis) at the same time.
This is also referred to as the different bases being **incompatible** with each other.

Having seen what happens in the Stern-Gerlach experiments, let's now see what happens mathematically when we measure a qubit.
By convention, we measure a qubit in the computational basis, at which point we observe the qubit to be in either the $\ket{0}$ or $\ket{1}$ state.
That is, we can't actually measure the state of a qubit (in terms of it $\theta$ and $\phi$ rotations) with a single measurement.
While a qubit is a probabilistic object, the act of measuring it will always yield a definite result.
In that sense, measuring the qubit collapses the state of a qubit into one of the basis states.

Recall that we can express an arbitrary qubit state as $\psi = \psi_{1}\ket{0} + \psi_{2}\ket{1}$, and that the amplitutes $\psi_{1}$ and $\psi_{2}$ can be obtained by taking the inner product of the state with the basis states: $\psi_{1} = \braket{0\|\psi}$ and $\psi_{2} = \braket{1\|\psi}$.
This allows us to rewrite the state of the qubit in terms of the outer products of the basis states:
\begin{equation}
\ket{\psi} = \braket{0\|\psi}\ket{0} + \braket{1\|\psi}\ket{1} \\\ 
  =(\ket{0}\bra{0} + \ket{1}\bra{1})\ket{\psi}
\end{equation}

where $\ket{0}\bra{0} + \ket{1}\bra{1}$ is just the identity matrix.
Crucially though we can think of $\ket{0}\bra{0}$ and $\ket{1}\bra{1}$ as the operators that get applied to the state of the qubit when they leave the top and bottom holes of the Stern-Gerlach apparatus, respectively.
So when we measure the state of the qubit, we're actually applying the operators $\ket{0}\bra{0}$ and $\ket{1}\bra{1}$ to the state of the qubit.

For example, when we measure the $\ket{0}$ state, we apply the operator $\ket{0}\bra{0}$ to $\ket{\psi}$ which collapses the state of the qubit into the $\ket{0}$ state: 
\begin{equation}
\begin{bmatrix} 1 & 0 \cr 0 & 0 \end{bmatrix} \begin{bmatrix} \psi_{1} \cr \psi_{2} \end{bmatrix} = \begin{bmatrix} \psi_{1} \cr 0 \end{bmatrix} = \psi_{1} \ket{0}.
\end{equation}

In other words, after measurement, we state of the qubit is no longer $\psi$, but $\psi_{1}\ket{0}$, which is another way of saying that the act of measurement alters the state of a qubit.

# How is this different from classical probability?
With all of the basics in place, we can now get to the question from the beginning: how is superposition different from mere uncertainty about which state a qubit is in?

Let's start with a quantum state
\begin{equation}
\Psi = \frac{1}{\sqrt{2}} ( \ket{0} + \ket{1} )
\end{equation}

This state is in a superposition of the $\ket{0}$ and $\ket{1}$ states, meaning it's not the case that the state is either $\ket{0}$ or $\ket{1}$ with equal probability.
Instead, there is a 0% chance that the state is in the $\ket{0}$ or the $\ket{1}$ state, and a 100% chance that the state is in the superposition of the two states, $\psi$.

To see why, consider measuring the state not in the computational basis but another, incompatible, basis like the Hadamard basis.
We can express the state $\Psi$ in terms of the Hadamard basis states because as we've seen above:

\begin{equation}
\ket{0} = \frac{1}{\sqrt{2}}(\ket{+} + \ket{-}) \\\ 
  \ket{1} = \frac{1}{\sqrt{2}}(\ket{+} - \ket{-})
\end{equation}

So by substituting we find that the state $\Psi$ actually corresponds to the $\ket{+}$ state in the Hadamard basis: $\ket{\Psi} = \ket{+}$.

We can then run 2 experiments with our $\Psi$ state, one in the computational basis and one in the Hadamard basis.
- In the computational basis, we measure the state to be either $\ket{0}$ or $\ket{1}$ with equal probability.
- And in the Hadamard basis, we **always** find the state to be $\ket{+}$.

Now consider the alternative scenario where $\Psi$ is not in a superposition, but in a classical probabilistic mixture of the $\ket{0}$ and $\ket{1}$ states.
This means that the state of the qubit is either $\ket{0}$ or $\ket{1}$ with equal probability, instead of both at the same time.
If we state is $\ket{0}$, then the state of the qubit in the Hadamard basis would be either $\ket{+}$ or $\ket{-}$ with equal probability.
And likewise, if the state is $\ket{1}$, then the state of the qubit in the Hadamard basis would also be either $\ket{+}$ or $\ket{-}$ with equal probability.

In other words, if we run the same 2 experiments as above:
- In the computational basis, we measure the state to be either $\ket{0}$ or $\ket{1}$ with equal probability, as before.
- But in the Hadamard basis, we measure the state to be either $\ket{+}$ or $\ket{-}$ with **equal probability**.

So that is the key difference between superposition and classical probability.
In superposition, quantum amplitudes are not independent of each other.
They can interfere and effectively cancel each other out.
This can be verified experimentally by preparing the same state multiple times and measuring it 2 incompatible bases, as described above.

# Conclusion
That's a wrap for this article.
We've covered a lot of ground, touching upon measurement bases, the Stern-Gerlach experiments and measurement in quantum mechanics.
Finally we saw how superposition is different from mere uncertainty about which state a qubit is in.