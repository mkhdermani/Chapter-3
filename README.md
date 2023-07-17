# Chapter-3
## Porgram 1

```julia

using JuMP, Ipopt

Kbar = 10.0
Lbar = 20.0
α = 0.3
β1 = 0.3
β2 = 0.6

#define the model
model = Model(Ipopt.Optimizer)

#define the variables
@variable(model, x1 >= 0)
@variable(model, x2 >= 0)
@variable(model, l1 >= 0)
@variable(model, l2 >= 0)
@variable(model, k1 >= 0)
@variable(model, k2 >= 0)

#define constraint of Cobb-Douglas production function
@NLconstraint(model, x1 == l1^β1 * k1^(1-β1))
@NLconstraint(model, x2 == l2^β2 * k2^(1-β2))
@constraint(model, l1 + l2 == Lbar)
@constraint(model, k1 + k2 == Kbar)

#define the objective function
@NLobjective(model, Max, (x1^α) * (x2^(1-α)))

#summary of the model
@show model

#solve the model
optimize!(model)

#status of the model
@show termination_status(model)

#GET THE OPTIMAL VALUE
@show value(x1)
@show value(x2)
@show value(l1)
@show value(l2)
@show value(k1)
@show value(k2)

#show objective value
@show objective_value(model)

```
```
model = A JuMP Model
Maximization problem with:
Variables: 6
Objective function type: Nonlinear
`AffExpr`-in-`MathOptInterface.EqualTo{Float64}`: 2 constraints
`VariableRef`-in-`MathOptInterface.GreaterThan{Float64}`: 6 constraints
Nonlinear: 2 constraints
Model mode: AUTOMATIC
CachingOptimizer state: EMPTY_OPTIMIZER
Solver name: Ipopt
Names registered in the model: k1, k2, l1, l2, x1, x2

******************************************************************************
This program contains Ipopt, a library for large-scale nonlinear optimization.
 Ipopt is released as open source code under the Eclipse Public License (EPL).
         For more information visit https://github.com/coin-or/Ipopt
******************************************************************************

This is Ipopt version 3.14.13, running with linear solver MUMPS 5.6.0.

Number of nonzeros in equality constraint Jacobian...:       10
Number of nonzeros in inequality constraint Jacobian.:        0
Number of nonzeros in Lagrangian Hessian.............:        9

Total number of variables............................:        6
                     variables with only lower bounds:        6
                variables with lower and upper bounds:        0
                     variables with only upper bounds:        0
Total number of equality constraints.................:        4
Total number of inequality constraints...............:        0
        inequality constraints with only lower bounds:        0
   inequality constraints with lower and upper bounds:        0
        inequality constraints with only upper bounds:        0

iter    objective    inf_pr   inf_du lg(mu)  ||d||  lg(rg) alpha_du alpha_pr  ls
   0  9.9999900e-03 2.00e+01 2.82e-01  -1.0 0.00e+00    -  0.00e+00 0.00e+00   0
   1  7.1979707e+00 5.67e-01 1.36e+03  -1.0 1.11e+01    -  8.99e-04 1.00e+00f  1
   2  6.8849673e+00 2.17e-03 3.89e+01  -1.0 3.89e-01   2.0 9.81e-01 1.00e+00h  1
   3  7.5221549e+00 2.38e-03 5.56e-01  -1.0 3.28e+00    -  1.00e+00 1.00e+00f  1
   4  8.6805008e+00 8.46e-01 1.60e-01  -1.7 5.80e+00    -  8.13e-01 1.00e+00f  1
   5  8.0780364e+00 8.21e-02 4.03e-02  -1.7 1.08e+00    -  1.00e+00 1.00e+00h  1
   6  8.0408925e+00 8.98e-03 3.61e-03  -2.5 4.53e-01    -  1.00e+00 1.00e+00h  1
   7  8.0350656e+00 1.11e-04 3.70e-05  -3.8 5.32e-02    -  1.00e+00 1.00e+00h  1
   8  8.0349885e+00 1.91e-09 7.98e-10  -5.7 1.81e-04    -  1.00e+00 1.00e+00h  1
   9  8.0349885e+00 1.08e-12 4.56e-13  -8.6 7.07e-06    -  1.00e+00 1.00e+00h  1

Number of Iterations....: 9

                                   (scaled)                 (unscaled)
Objective...............:  -8.0349884580269606e+00    8.0349884580269606e+00
Dual infeasibility......:   4.5565195698078065e-13    4.5565195698078065e-13
Constraint violation....:   1.0764722446765518e-12    1.0764722446765518e-12
Variable bound violation:   0.0000000000000000e+00    0.0000000000000000e+00
Complementarity.........:   2.5095845729454518e-09    2.5095845729454518e-09
Overall NLP error.......:   2.5095845729454518e-09    2.5095845729454518e-09


Number of objective function evaluations             = 10
Number of objective gradient evaluations             = 10
Number of equality constraint evaluations            = 10
Number of inequality constraint evaluations          = 0
Number of equality constraint Jacobian evaluations   = 10
Number of inequality constraint Jacobian evaluations = 0
Number of Lagrangian Hessian evaluations             = 9
Total seconds in IPOPT                               = 0.029

EXIT: Optimal Solution Found.
termination_status(model) = MathOptInterface.LOCALLY_SOLVED
value(x1) = 4.043216058934125
value(x2) = 10.784754073882947
value(l1) = 3.52941177435552
value(l2) = 16.47058822564448
value(k1) = 4.2857142880809125
value(k2) = 5.714285711919088
objective_value(model) = 8.03498845802696

8.03498845802696
```
