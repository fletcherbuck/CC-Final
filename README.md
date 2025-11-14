---
title: "Calculating Molar Masses"
embed-resources: true
---
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import os
import sympy
from sympy import sympify

massnumbers = {"C": 12.011,"O": 15.999,"H": 1.008,"N": 14.007,"F": 18.998,"He": 4.003,"Li": 6.941,"Be": 9.012,"B": 10.811,"Ne": 20.180,"Na": 22.990,"Mg": 24.305,"Al": 26.982,"P": 30.974,"S": 32.065,"Cl": 35.453,"Ar": 39.948}

def find_elements(compound):
    elements = []
    i = 0

    while i < len(compound):

        if i + 1 < len(compound) and compound[i+1].islower():
            element = compound[i:i+2]
            i += 2
        else:
            element = compound[i]
            i += 1

        num_str = ""
        while i < len(compound) and compound[i].isdigit():
            num_str += compound[i]
            i += 1

        count = int(num_str) if num_str else 1

        elements.append((element, count))

    return elements
def molar_mass(formula):
    elements = find_elements(formula)
    total_mass = 0
    for element, count in elements:
        total_mass += massnumbers[element] * count
        individual_masses.append([element,count,massnumbers[element],massnumbers[element]*count])
    return total_mass

individual_masses = []

Caffeine = "C8H10N4O2"
total = molar_mass(Caffeine)
print(f"Total molecular mass: {total:.3f}\n")

u= sympy.symbols("u")
n= sympy.symbols("n")
expr = u*n
sympy.latex(f)
latex_expr = sympy.latex(expr)
latex_expr
#caffine calculation in sympy

df = pd.DataFrame(individual_masses, columns=["Element", "Count", "Atomic Mass", "Total Mass"])
df
print(df.to_markdown(index=False))

plt.figure(figsize=(6,6))
plt.pie(df["Total Mass"], labels=df["Element"], autopct="%1.1f%%")
plt.title("Element Mass Contribution in Caffeine")
plt.show()

```
