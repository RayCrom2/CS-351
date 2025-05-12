|Thread<br>Count|Wall Clock<br>Time|User Time|System Time|Speedup|
|:--:|--:|--:|--:|:--:|
|1|14.28|13.78| 0.39|1.00|
|2| 7.71|14.37| 0.51| 1.85|
|3| 5.30|14.46| 0.52| 2.69|
|4| 4.54|15.93| 0.75| 3.15|
|5| 3.90|16.16| 0.82| 3.66|
|6| 3.33|16.47| 0.88| 4.29|
|7| 3.06|16.54| 1.05| 4.67|
|8| 2.79|17.07| 1.21| 5.12|
|16| 1.84|19.24| 1.90| 7.76|
|24| 1.62|20.91| 2.52| 8.81|
|32| 1.62|20.06| 3.28| 8.81|
|40| 1.60|19.55| 6.10| 8.93|
|48| 1.73|19.30|10.39| 8.25|
|56| 1.88|17.45|27.08| 7.60|
|64| 1.96|17.76|46.63| 7.29|
|72| 1.87|17.59|50.39| 7.64|
|80| 1.91|17.85|26.96| 7.48|

![image](https://github.com/user-attachments/assets/28b0a897-51f6-4821-b460-44e26b6ce7c2)

Question: Notice that there is a maximum speed-up factor, but not necessarily using the most threads. Make a guess (i.e., write a short paragraph) as to why you think more threads aren't necessary better. Here's a hint: think about a group of people waiting to go through a turnstile (like at BART or Disney World). Are more people able to go through it just because there are more people?
 -I think that as the amount of threads increase that there comes a point that we no longer gain anything from using more threads. This is because making more threads becomes more of a problem when they have to share resources like memory, cache, or I/O. Too many threads can also lead to overhead from context switching and sync delays. In short, creating and executing more threads eventually outweighs the performance gains and can even slow a program down (bottleneck).

Question: Do you think it's possible to get "perfect scaling" — meaning that the $(1-p)$ terms is zero?
 -I do not think it is possible to get perfect scaling. For this to be true, the entire program would have to be able to be parallelizable and in most, if not all cases, there is some set-up that can not be parallelized. 

**Computing for $$16$$ $$cores$$:**

$$ serial = \frac{0.010163129 + 0.000000716}{1.774976347} = 0.0569 $$
$$ speedup = \frac{1}{1 - 0.9431 + \frac{0.9431}{16}} = 1.892326616 $$

One final Question: in reviewing the graph of speed-ups to number of threads, note that we get pretty linear (when you plot the dots, they're pretty close to being a line) speed-up. What's the slope of that line? (Pick two values, like for one and seven threads, and do the rise-over-run thing you learned in Algebra). Does that linear trend continue as we add more threads? What do you think causes the curve to "flatten out" when we use large thread counts?
 -The slope for my line from 1-7 is .602. The trend does not continue as we add more threads, the slope actually decreases in magnitude. I think that large thread counts flatten this slope because the overhead involved in managing so many threads outweighs the benefits of parralelization.
