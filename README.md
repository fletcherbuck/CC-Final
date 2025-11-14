# Calculating Molar Masses Programmatically: A Quarto Solution"

## Introduction

This project is designed to demonstrate the process of creating a scientific computation tool using Python and publishing it through a Quarto webpage hosted on GitHub Pages. The focus is on calculating the **molar mass** of chemical compounds programmatically. By combining chemistry, computer science, and mathematics, this project bridges multiple scientific disciplines while showcasing the potential of computational tools in education and research.

The molar mass calculator takes a chemical formula (like `H2O`, `C6H12O6`, or `Fe2(SO4)3`) and determines the total molecular weight based on known atomic masses of each element. It uses a parser that interprets chemical formulas, manages parentheses for grouped atoms, and correctly applies subscripts to multiply atom counts. This project also includes symbolic representation using SymPy, tabular data analysis with pandas, and graphical visualization through matplotlib — all integrated within a single Quarto document.

This document thoroughly explains how the code works, its scientific importance, and how such a project can be used in education. It also covers challenges faced during development, provides a full breakdown of every component, and summarizes the lessons learned.

---

## What the Project Is and Its Purpose

The goal of this project is to create a Python-based tool that automates the process of calculating molecular weights. In chemistry, calculating molar mass is one of the most fundamental operations. Traditionally, this is done manually by summing atomic weights multiplied by their respective counts in the formula. However, for complex compounds or repetitive tasks, manual calculations can be error-prone and time-consuming.

By developing a program that automatically parses a chemical formula, identifies the elements, counts their occurrences, and sums their contributions, we eliminate human error and make the process efficient. The output provides both numeric and visual insights into how different atoms contribute to the total molecular mass.

Furthermore, by embedding this project into a Quarto webpage, the results become reproducible, interactive, and shareable. Quarto allows researchers and students to integrate code, results, text, and equations into one cohesive document — much like Jupyter notebooks but with professional publishing capabilities.

---

## How It Works: Code Overview

The code for this project can be broken down into several main components:

1. **Atomic Mass Table**
2. **Formula Parsing Function**
3. **Molar Mass Calculation Function**
4. **Data Presentation (Table and Graph)**
5. **Symbolic Representation (SymPy)**
6. **Visualization (Matplotlib)**

Each of these plays a critical role in making the tool both functional and educational.

#### 1. Atomic Mass Table

At the heart of the program lies a dictionary called `atomic_masses`. This dictionary stores the molar mass (in grams per mole) for each element. For example:

```python
atomic_masses = {
    'H': 1.008, 'He': 4.0026, 'Li': 6.94, 'Be': 9.0122, 'B': 10.81, 'C': 12.011,
    'N': 14.007, 'O': 15.999, 'F': 18.998, 'Na': 22.99, 'Mg': 24.305,
    'Al': 26.982, 'Si': 28.085, 'P': 30.974, 'S': 32.06, 'Cl': 35.45, 'K': 39.098,
    'Ca': 40.078, 'Fe': 55.845, 'Cu': 63.546, 'Zn': 65.38
}
```

This lookup table allows the program to retrieve the atomic mass of each element when calculating totals. When an element is found in a formula, its value is multiplied by its count and added to the total molar mass.

#### 2. Formula Parsing

Parsing chemical formulas is one of the most challenging parts of this project. Chemical formulas follow patterns that combine uppercase and lowercase letters, numbers, and parentheses. The function `parse_formula()` converts a text string like `Fe2(SO4)3` into a structured dictionary:

```python
{'Fe': 2, 'S': 3, 'O': 12}
```

It does this by breaking the formula into tokens using a regular expression (regex). The regex pattern used is:

```python
r'([A-Z][a-z]?|\d+|\(|\))'
```

This identifies elements (like `Fe`, `S`, `O`), numbers, and parentheses. The parser uses a stack structure to manage nested groups of atoms. When it encounters a `(`, it starts a new group; when it finds a `)`, it closes that group and applies any following multiplier.

For instance, `Fe2(SO4)3` is processed as:
- Fe appears twice.
- (SO4) is repeated 3 times, giving 3 sulfur atoms and 12 oxygen atoms.

This stack-based method ensures that complex formulas with nested parentheses are handled correctly.

#### 3. Molar Mass Calculation

After parsing, the program calculates the total molar mass using:

```python
def molar_mass(formula):
    counts = parse_formula(formula)
    total = 0
    for el, cnt in counts.items():
        total += atomic_masses[el] * cnt
    return counts, total
```

This function iterates through each element and multiplies its atomic mass by the count obtained from the parser. The results are summed to produce the final molar mass. This simple loop forms the computational engine of the project.

#### 4. Data Presentation with Pandas

Once the molar mass is computed, the next step is to present the results in a readable form. Using the pandas library, we can create a DataFrame to show the breakdown of elements:

| Element | Count | Atomic Mass (g/mol) | Contribution (g/mol) |
|----------|--------|---------------------|-----------------------|
| Fe       | 2      | 55.845              | 111.69               |
| S        | 3      | 32.06               | 96.18                |
| O        | 12     | 15.999              | 191.99               |

The total molar mass is the sum of the contributions column. This table makes it clear how each element contributes to the total molecular mass.

#### 5. Symbolic Representation (SymPy)

To reinforce the mathematical aspect of chemistry, the project uses SymPy to represent formulas symbolically. For instance, glucose (`C6H12O6`) can be expressed symbolically as:

$$ 6M_C + 12M_H + 6M_O $$

This equation is generated by SymPy and rendered in LaTeX automatically. It visually connects the program’s numerical calculation with the chemical equation it represents, bridging computational and theoretical chemistry.

#### 6. Visualization with Matplotlib

Visual representation is a key educational tool. The program creates a bar graph showing how much each element contributes to the overall molar mass.

```python
plt.bar(df['element'], df['contribution_g_per_mol'])
plt.xlabel('Element')
plt.ylabel('Contribution (g/mol)')
plt.title(f'Element contributions to molar mass of {formula}')
```

This graph helps students quickly see which elements are most responsible for a compound’s mass — for example, heavier elements like iron or lead dominate compared to lighter ones like hydrogen.

---

## Educational and Scientific Applications

This project has multiple educational and scientific benefits:

#### 1. Chemistry Education
In classrooms, students struggle with chemical formulas and molar mass calculations. By automating this process, educators can demonstrate the logic behind each calculation step. Students can input their own compounds and immediately see numeric, tabular, and graphical representations to help them visualize what is going on. Not only does this help students learn, it can make students work more effeciently by saving time by having a solution to doing tedious calculations by hand. These calculations, though simple, can take extra time that is vital in a laboratory or lecture type envornment.

#### 2. Computational Thinking
This project also encourages interdisciplinary learning. It teaches programming concepts in a scientific context, allowing these concepts to be viualized in an easy to understand stem-related disipline.

#### 3. Scientific Research
Researchers and lab technicians frequently calculate molar masses while preparing chemical solutions. Automating this process ensures accuracy,consistency,and efficeintly, particularly when dealing with large datasets or repetitive calculations.

#### 4. Reproducibility
By using Quarto and GitHub Pages, results are fully reproducible. This means this exact code can be utilized by those in need of somethinmg to quickly complete these calculations.

---

## Struggles and Challenges Faced 
This project was extremely difficult for me, as it was very complicated and introcate despite the main goal being so simple. I struggled in 

---

## Tables and Graphs Explained

#### Tables
The pandas DataFrame table organizes computed results into a human-readable format. Each row corresponds to an element, and the columns detail its atomic mass, count, and contribution. This tabular structure aligns perfectly with laboratory-style data recording — precise, quantitative, and verifiable.

| Element | Count | Atomic Mass (g/mol) | Contribution (g/mol) |
|----------|--------|---------------------|-----------------------|
| Fe       | 2      | 55.845              | 111.69               |
| S        | 3      | 32.06               | 96.18                |
| O        | 12     | 15.999              | 191.99               |

The table is generated automatically for any input formula. This feature is especially useful for comparing multiple compounds or teaching students to read chemical data.

#### Graphs
The matplotlib-generated bar chart visually represents each element’s contribution. It provides an intuitive understanding of which atoms dominate the molecular weight. For compounds containing both light and heavy atoms, this contrast is immediately clear.

Such visual tools enhance conceptual learning — rather than memorizing numbers, students can *see* the impact of different elements on molecular structure and mass.

---

## Summary

This molar mass calculator project demonstrates how computational methods can enhance traditional science learning. By combining Python programming, chemical understanding, and data visualization, it creates a dynamic and educationally valuable tool.

**Key takeaways:**
- The parser translates chemical notation into computable data structures.
- Python’s ecosystem (regex, pandas, matplotlib, sympy) provides the analytical and visualization tools.
- Quarto enables integration of narrative, computation, and graphics in one polished webpage.
- Publishing on GitHub Pages ensures accessibility and reproducibility.

In education, this tool can help students understand both the science and computation behind chemical formulas. In research, it can automate molar mass calculations for complex compounds. And as a project, it illustrates how science, technology, engineering, and mathematics can converge in a single reproducible workflow.

This combination of theory, practice, and presentation represents the future of scientific learning — transparent, interactive, and interdisciplinary.
