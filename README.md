This README provides instructions on using the Python code for molecular descriptor calculations and regression analysis.

Introduction
The provided Python script utilizes the RDKit and Mordred libraries for molecular descriptor calculations and performs regression analysis on boiling points of organic compounds based on molecular features.

Installation
Ensure you have Python installed on your system. You can install the required libraries using pip:
pip install rdkit mordred pandas matplotlib statsmodels

Usage

1.Import the necessary libraries:
from rdkit import Chem
from mordred import Calculator, descriptors
import pandas as pd
import matplotlib.pyplot as plt
import statsmodels.api as sm

2.Initialize the Mordred calculator for descriptor calculation:
calc = Calculator(descriptors, ignore_3D=True)

3.Calculate molecular descriptors:
pentane = Chem.MolFromSmiles('CCCCC')
methyl_pentane = Chem.MolFromSmiles('CCCC(C)C')
wiener_index = WienerIndex.WienerIndex()
result1 = wiener_index(pentane)
result2 = wiener_index(methyl_pentane)

4.Perform regression analysis:
X = df[["MW", "Wiener", "Z1", "Z2"]]  # Features
X = sm.add_constant(X)
y = df[["BP_K"]]  # Target variable
model = sm.OLS(y, X).fit()
predictions = model.predict(X)
print(model.summary())

5.Visualize results:
plt.scatter(df.MW, df.BP_K)
plt.xlabel('Molecular Weight')
plt.ylabel('Boiling Point in Kelvin')
plt.show()
Dataset
The provided dataset BP.CSV contains compounds with their respective boiling points (in Celsius and Kelvin), SMILES representation, and molecular weight.

