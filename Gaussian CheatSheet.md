- Gaussian CheatSheet

Gaussian distribution has a lot of beautiful formula that we might encounter them in various cases. Here I show some of them.

1. *Gaussian Indentities* (For reference see this http://www.gatsby.ucl.ac.uk/~snelson/thesis.pdf - page 124)
Let us assume we have a Gaussian distribution on a vector y:
    Y samples from N(mean U*f, covariance A)
    
where f is a random variable, and

    f is samples from N(0, covarance B)
Then

    p(Y) = \integral df p(y|f)p(f) = N(0, A + U B U^T )

Let see how useful this is. Consider a very simple example:

    f is samples from N(0, covarance B)
And

    Y samples from N(f, covariance A)
    
Then

    P(Y) = \integral df p(y|f)p(f) = N(0, A+ I B I^T) = N(0, A+ B)
    

Let us turn to a somewhat more involved example (For reference see this http://www.gatsby.ucl.ac.uk/~snelson/thesis.pdf - pages 38-39). Let us assume U = K_{NM}K_{MM}^-1 and B = K_{MM}. The tricky part is U B U^T, which can be computed
as:

      K_{NM}K_{MM}^-1 K_{MM} (K_{NM}K_{MM}^-1)^T
    = K_{NM}K_{MM}^-1 K_{MM} (K_{MM}^-1)^T (K_{NM})^T (use the rule (AB)^T = B^T A^T)
    = K_{NM} I K_{MM}^T)^-1 (K_{NM})^T (use the rule K_{MM}^-1 K_{MM} = I and the rule (A^-1)^T = (A^T)^-1
    = K_{NM} K_{MM}^-1 K_{MN} (K_{MM} is a symmetric matrix)

How beautiful it is!

2. *Conditioning Gaussian* (For reference see this http://cs229.stanford.edu/section/cs229-gaussian_processes.pdf)

Let us assume 

    X samples from N(U_X, SIGMA_XX)

    Y samples from N(U_Y, SIGMA_YY)
    
The conditional densities are also Gaussian

    X|Y samples N(U_X + SIGMA_XY SIGMA_YY^-1 (Y-U_Y), SIGMA_XX -SIGMA_XY SIGMA_YY^-1 SIGMA_YX)
    Y|X samples N(U_Y + SIGMA_YX SIGMA_XX^-1 (X-U_X), SIGMA_YY -SIGMA_YX SIGMA_XX^-1 SIGMA_XY)

See http://cs229.stanford.edu/section/cs229-gaussian_processes.pdf for a proof.
This is one of the most useful formula I have seen regardingto Gaussian distribution. For example, let us assume:

    X, Y samples from N(0, SIGMA_XY)

Then we have

    X samples from N(0, SIGMA_XX)
    Y samples from N(0, SIGMA_YY)
    
The conditional densities are as follows:

    Y|X samples from N(SIGMA_YX SIGMA_XX^-1 X, SIGMA_YY -SIGMA_YX SIGMA_XX^-1 SIGMA_XY)
    
In Gaussian Processes, we perform prediction per each new test case using this formula.

3. Gaussian integral
The Gaussian integral is encountered very often in practice. The formulas are as follows:

    integral_{-infinity}^{infinity}dx exp{-x^2}  = sqrt{\pi}
    integral_{-infinity}^{infinity}dx exp{-ax^2} = sqrt{\pi/a}
    integral_{-infinity}^{infinity}dx exp{-a(x+b)^2} = sqrt{\pi/a}
    
How beautiful it is!

4. Laplace’s technique: normal approximation to posterior (see reference: http://www2.stat.duke.edu/~st118/sta250/laplace.pdf and http://www.cedar.buffalo.edu/~srihari/CSE574/Chap4/Chap4-Part4.pdf)

Let us assume a model q(theta). Doing a second order Taylor expansion of q(theta) gives us:

    q(theta) \approx q(theta^) + (theta-theta^) q'(theta^) + 1/2 (theta-theta^)^2 q''(theta^)

Let us choose theta^ as follows
    
    theta^ = argmax_{theta} q(theta)
    
In this way q'(theta^) = 0 and q''(theta^) < 0. Therefore,

    q(theta) \approx q(theta^) + 1/2 (theta-theta^)^2 q''(theta^)
    
Instead of working with q(theta), it is very useful to work with ln q(theta) instead:


    ln q(theta) \approx ln q(theta^) + 1/2 (theta-theta^)^2 (ln q(theta^))''
    q(theta) \approx q(theta) exp{ (theta-theta^)^2 (ln q(theta^))''/2 }
    or q(theta) \approx q(theta^) exp{ - (theta-theta^)^2 -(ln q(theta^))''/2 }

Once q(theta) is approximated using Laplace's technique, the normalized version of q(theta)  has a beautiful form. In detail, 

    \integral dtheta q(theta) \approx integral_{-infinity}^{infinity} dtheta q(theta^) exp{ - (theta-theta^)^2 -(ln q(theta^))''/2 }

Recall that 

    integral_{-infinity}^{infinity}dx exp{-ax^2}  = sqrt{\pi/a}
    
Then 

    \integral dtheta q(theta) \approx q(theta^) \sqrt{2\pi/-(ln q(theta^))'' } } = Z

As the normalizing constant has a tractable (and beautiful) form, we can the normalized version of q(theta) as follows:
    
     q(theta)/Z \approximate N(theta|theta^, 1/-(ln q(theta^))'')
     
