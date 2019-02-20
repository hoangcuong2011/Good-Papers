Non-Convex Optimization in Machine Learning - a few things to learn.

1. saddle point: derivative is zero for every possible direction, but the point is useless

2. how many saddle points: a lot (exponential to the dimension)

3. Do we get converge to saddle point?
Perhaps no. We get stuck there because gradient is very small (==0), but the model does not get converge to there. There is a paper from Berkeley about this, but still a bit not readable for non-math people.

4. how to escape saddle point?

first. approach: using second-order derivivate method. but too expensive.

second. approach: adding noise.

5. Is it solved?

hell-know

second-order derivivate: too slow.

adding noise: theoretically - works in polynomial time. bad news: polynomial time with ... number of dimension ...

6. so why Neural network can be trained, given a hell of saddle points are out there?

We don't know yet.
