# Quicksort Pivots

in the lectures I only briefly mentioned strategies for determining a good pivot
for quicksort. The implementation on the slides simply picks the leftmost
element in the part of the array that we consider as a pivot. I also mentioned a
few other ways of picking a good pivot, e.g. randomly.

Median-of-three is also a good way of picking a pivot -- inspect the first,
middle, and last elements of the part of the array under consideration and
choose the median value. Using the probabilities for picking a pivot in a
particular part of the array (in the same way as we did on slide 34), argue
whether this method is more or less (or equally) likely to pick a good pivot
compared to simply choosing the first element. Assume that all permutations are
equally likely, i.e. the input array is ordered randomly.

Your answer must derive probabilities for choosing a good pivot and
quantitatively reason with them.

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

# Discerning the Probabilities

Referencing slide \#34 from the sorting material, the model denotes that there are three different sections of any given input array that a pivot could be selected from. There are the two ends of the array which are categorized to be **bad** pivots because they belong towards the beginning or end of the array rather than the middle. The model makes it pretty clear that $\frac{1}{4}$ of the time, a randomly selected pivot will be picked from either of the **bad** pivot sections. Moreover, there are that leaves $\frac{2}{4} = \frac{1}{2}$ selections to randomly come from a **good** pivot section.

Acknowledging that, we can pretty easily break any arbitrary array into four different *quartiles* where two quartiles represent **bad** pivots and the other two represent **good** pivots. Next, we can apply some introductory combinatorics to contrive that considering *three* different elements from *four* different quartiles gives us $4^{3} = 64$ distinct combinations representing the different ways we can select a pivot. In other words, we can consider the probability of **any** given pivot selection to be out of $64$ possible outcomes by breaking the problem into **four** equal quartiles. Each quartile can be designated by where a random pivot would end up in relation to the "center" of the array. $Q_{1}$ is the first *(left-most)* quartile where any pivots selected are too small to be considered good selections. $Q_{2}$ and $Q_{3}$ are the two middle quartiles where any pivots selected are considered good selections. $Q_{4}$ is the last *(right-most)* quartile where any pivots selected are too large to be considered good selections.

Now that we have a sufficient probability distribution to consider, we need to consider the method of selecting a pivot in context to that distribution. By the definition of a median, we know that the pivot will always end up between the two quartiles in which the other two elements land in. That is, we know a *good* pivot will **always** result under two distinct conditions. The first scenario being when one of the three random selections would fall into $Q_{1}$ and a different selection of the random three selections falls into $Q_{4}$. The third random selection would naturally **have** to exist within either $Q_{2}$ or $Q_{3}$ since it would be the median of the three selections. The second scenario is whenever two of the three random selections would fall into $Q_{2}$ *or* $Q_{3}$ which necessitates the median random selection must *also* exist within either $Q_{2}$ or $Q_{3}$. 

Conversely, a *bad* pivot will **always** result when two of the three random selections would **both** fall into either $Q_{1}$ *or* $Q_{4}$. This is because the median selection would then fall into either $Q_{1}$ or $Q_{4}$ which are both considered *bad* pivot selections. Otherwise, a *bad* pivot would also result when **all three** random selections would fall into either $Q_{1}$ *or* $Q_{4}$.

Finally, we know the probability distribution and the four distinct combinations of outcomes. We know that there are two combinations of selections that will result in a good pivot, and two combinations of selections that will result in a bad pivot. To determine the exact probability values, we only need to discern exactly how many combinations fall into each of the four distinct outcomes. To do so, I will represent the arbitrary random selections by the quartile that they belong in after being sorted, and I will denote the quartiles as $Q_{1}$, $Q_{2}$, $Q_{3}$, and $Q_{4}$.

First I will consider the combinations of two of the three random selections falling into $Q_{1}$ or $Q_{4}$. 
$$\begin{gather*}
(Q_{2} Q_{1} Q_{1}), (Q_{1} Q_{2} Q_{1}), (Q_{1} Q_{1} Q_{2}), (Q_{2} Q_{4} Q_{4}), \\ (Q_{4} Q_{2} Q_{4}), (Q_{4} Q_{4} Q_{2}), (Q_{3} Q_{1} Q_{1}), (Q_{1} Q_{3} Q_{1}), \\ (Q_{1} Q_{1} Q_{3}), (Q_{3} Q_{4} Q_{4}), (Q_{4} Q_{3} Q_{4}), (Q_{4} Q_{4} Q_{3}) \\
\end{gather*}
$$

We can see that there are twelve distinct combinations where two out of the three pivot selections end up being bad choices. Thus, the probability of selecting one of those combinations is $\frac{12}{64} = \frac{3}{16}$.

Next, I will consider the combinations of all three random selections falling into $Q_{1}$ or $Q_{4}$:

$$\begin{gather*}
(Q_{1} Q_{1} Q_{1}), (Q_{1} Q_{1} Q_{4}), (Q_{1} Q_{4} Q_{1}), (Q_{4} Q_{1} Q_{1}), \\ (Q_{1} Q_{4} Q_{4}), (Q_{4} Q_{1} Q_{4}), (Q_{4} Q_{4} Q_{1}), (Q_{4} Q_{4} Q_{4}) \\ 
\end{gather*}
$$

There are eight distinct combinations where all three pivot selections end up being bad choices. Thus, the probability of selecting one of those combinations is $\frac{8}{64} = \frac{2}{16} = \frac{1}{8}$.

Although I *could* depict all the unique combinations for the good pivot selections, I don't necessarily have to because I now have all the probability values for selecting a **bad** pivot: $\frac{3}{16} + \frac{2}{16} = \frac{5}{16} = 0.3125 * 100\% = 31.25\%$. If this method will result in us selecting a *bad* pivot five out of sixteen times ($\frac{5}{16}$), we can infer that the probability of selecting a **good** pivot will be: $1 - \frac{5}{16} = \frac{11}{16} = 0.6875 * 100\% = 68.75\%$.

## Final Answer

Since the probability of selecting a *good* pivot via the median-of-three method is $\frac{11}{16} = 68.75\%$, we know that it is more likely to select a *good* pivot using this method than it is to select a *good* pivot using the leftmost element of the array. The probability of selecting a *good* pivot using the leftmost element of the array is $\frac{1}{2} = 50\%$. Therefore, the median-of-three method is more likely to select a *good* pivot than the leftmost element method.