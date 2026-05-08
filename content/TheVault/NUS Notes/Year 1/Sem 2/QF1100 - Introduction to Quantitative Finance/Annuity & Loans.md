---
title: Annuity & Loans
Date Created: 2024-02-27
Last Updated: 2025-09-27
tags:
  - QF1100
  - Math
  - Finance
---
# Annuity
---
An <span style='color:#0fb9b1'>annuity</span> is a contract that <span style='color:#f7b731'>pays</span> the holder (the annuitant) money periodically, according to a predetermined <span style='color:#f7b731'>schedule or formula</span> (finite time).

A <span style='color:#0fb9b1'>perpetuity</span> is <span style='color:#f7b731'>an annuity</span> which pays a fixed sum periodically <span style='color:#f7b731'>forever</span>.

It is more of a contract where a person <span style='color:#f7b731'>pays a steady stream</span> of cash as an investment.

**Perpetual Annuity Formula**
$$
PV = \sum^{\infty}_{k = 1} \frac{A}{(1 + r)^{k}} = \frac{A}{1 + r}\sum^{\infty}_{k = 0} \frac{1}{(1 + r)^{k}} = \frac{A}{1+r} \times \frac{1}{1 - \frac{1}{1+r}} = \frac{A}{r}
$$
**Where**
- $A$ is the **amount paid continuously** for 1 period
- $r$ is the interest rate

Now $n$ <span style='color:#f7b731'>goes to infinity</span>, this is because a perpetuity, there is no end or the person is unsure of when to end. If it a annuity, then it is the regular [[Interest Rates, PV & FV#Present Value|preset value]] formula up till $n$.

The <span style='color:#fa8231'>problem</span> <span style='color:#f7b731'>can be both FV and PV</span>, it depends on the scenario and aim.

**Note that**
$$
\sum^{\infty}_{k = 0} x^{k} = \frac{1}{1-x}
$$
# Loans
---
It is the process of borrowing money from the bank and then <span style='color:#f7b731'>pay a installment every month</span> with interest until the debt is fully paid.

For <span style='color:#0fb9b1'>loans</span>, it is assumed that the <span style='color:#f7b731'>first payment is at the end of the first year</span> $t = 1$, <b><mark style='background:#f7b731'>unless specified</mark></b>.

Depending on the <span style='color:#f7b731'>cash flow, the PV will be different</span> :
- $(0,c,c,c,c,\dots)$, here the **PV will be the principle**
- $(P,-c,-c,-c,-c,\dots)$ here the **PV will be 0**
>This is because, the summation of all the installments should be equal to principle, thus $0 = P - \sum^{n}_{k}{-c \times (1 +  r)^k}$

Now regarding the <span style='color:#fa8231'>last payment</span> usually, the final payment will be less than the installment :
- If the borrower wants to <span style='color:#f7b731'>pay together with the last installment</span>, then the take the $\lfloor n \rfloor$ 
- If the borrower wants to <span style='color:#f7b731'>pay in the subsequent year</span>, then it will be $\lfloor n \rfloor + 1$
