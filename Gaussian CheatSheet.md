- Gaussian CheatSheet
Gaussian distribution has a lot of beautiful formula that we might encounter them in various cases. Here I show some of them.

1. Gaussian Indentities. (For reference see this http://www.gatsby.ucl.ac.uk/~snelson/thesis.pdf - page 124)
Let us assume we have a Gaussian distribution on a vector y:
    Y samples from N(mean U*f, covariance A)
    
where f is a random variable, and

    f is samples from N(0, covarance B)
    
Then 
        p(Y) = \integral df p(y|f)p(f) = N(0, A + U B U^T )

Let see how useful this is (For reference see this For reference see this http://www.gatsby.ucl.ac.uk/~snelson/thesis.pdf - pages 38-39). Let us assume U = K_{NM}K_{MM}^-1 and B = K_{MM}. The tricky part is U B U^T, which can be computed
as:

      K_{NM}K_{MM}^-1 K_{MM} (K_{NM}K_{MM}^-1)^T
    = K_{NM}K_{MM}^-1 K_{MM} (K_{MM}^-1)^T (K_{NM})^T (use the rule (AB)^T = B^T A^T)
    = K_{NM} I K_{MM}^T)^-1 (K_{NM})^T (use the rule K_{MM}^-1 K_{MM} = I and the rule (A^-1)^T = (A^T)^-1
    = K_{NM} K_{MM}^-1 K_{MN} (K_{MM} is a symmetric matrix)

So beautiful it is!
