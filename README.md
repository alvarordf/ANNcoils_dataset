# ANNcoilsDataset
Electromagnetic FEA simulations of coupled coils for IMDs from the article **Neural Network-Based Design of Wireless Power Transfer Systems for Implantable Medical Devices** (Álvaro Rodríguez Fuentes, Miguel Jiménez Carrizosa, Regina Ramos Hortal).
## Description of the dataset
The dataset includes geometric and electrical data of coupled multilayer squared planar coils. **4635** simulations were performed using the electromagnetic FEA software *Ansys HFSS 2025 R1*. This data was used to train an Artificial Neural Network using the *Neural Net Fitting* application of *MATLAB*.
The file includes:
### Simulation inputs: geometry
The coupled coils of the simulations are defined by their geometry. Thus, the inputs of the simulations are included in columns 1 to 16. These variables are represented in the following figure:

![453157554-741e52e5-c288-45bc-a9aa-6686271e33e4](https://github.com/user-attachments/assets/c710c017-5b27-48a2-9ec6-d08d244066cd)


1. **Freq (MHz)**: operating frequency (fixed at 6.78 MHz)
2. **Dist (mm)**: distance between primary and secondary coils (fixed at 15 mm)
3. **W1 (mm)**: trace width of primary coil
4. **W2 (mm)**: trace width of secondary coil
5. **S1 (mm)**: trace separation of primary coil
6. **S2 (mm)**: trace width of secondary coil
7. **N1**: number of turns per layer of primary coil
8. **N2**: number of turns per layer of secondary coil
9. **D1 (mm)**: external length of primary coil
10. **D2 (mm)**: external length of secondary coil
11. **Nlay1**: number of layers of of primary coil
12. **Nlay2**: number of layers of secondary coil
13. **H1 (oz)**: trace thickness of primary coil (fixed at 1 oz.)
14. **H2 (oz)**: trace thickness of secondary coil (fixed at 1 oz.)
15. **X1 (mm)**: total thickness of primary coil (fixed at 1.6 mm)
16. **X2 (mm)**: total thickness of secondary coil (fixed at 1.6 mm)
The range of each variable is defined in the following table:

| Var. | Freq (MHz) | Dist (mm) | W1 (mm) | W2 (mm) | S1 (mm) | S2 (mm) | N1  | N2  | D1 (mm) | D2 (mm) | Nlay1 | Nlay2 | H1 (oz) | H2 (oz) | X1 (mm) | X2 (mm) |
| ---- | ---------- | --------- | ------- | ------- | ------- | ------- | --- | --- | ------- | ------- | ----- | ----- | ------- | ------- | ------- | ------- |
| Min  | 6.78       | 15        | 0.5     | 0.5     | 0.5     | 0.5     | 1   | 1   | 10      | 5       | 2     | 2     | 2       | 2       | 1.6     | 1.6     |
| Max  | 6.78       | 15        | 4       | 3       | 3       | 2       | 5   | 5   | 40      | 20      | 4     | 4     | 2       | 2       | 1.6     | 1.6     |
### Simulation outputs: electrical variables
The outputs of the simulations are the electrical parameters of the inductive link. The FEA software resolves the system as a two-port network, yielding the complex impedance matrix of the system:
$\mathbf{U} =\mathbf{Z}\cdot\mathbf{I}$; 

Their complex values are included in columns 17-20. From the impedance matrix (Z-matrix), the electrical variables of the inductive link are extracted (columns 20-28):

![453157722-dfa10250-0cd1-483e-9d66-bcfa9cac12d0](https://github.com/user-attachments/assets/db836db7-1804-4b2e-9573-8cabe16fe411)

20. **L1 (uH)**: Self inductance of primary coil, in uH.

$L_1=\frac{1}{2\pi f_{sw}} \Im{(Z_{11})}$

21. **L2 (uH)**: Self inductance of secondary coil, in uH.

$L_2=\frac{1}{2\pi f_{sw}} \Im{(Z_{22})}$

22. **R1 (Ohm)**: Self resistance of primary coil, in Ohms.

$R_1=\Re{(Z_{11})}$

23. **R2 (Ohm)**: Self resistance of secondary coil, in Ohms.

$R_2=\Re{(Z_{22})}$

24. **k**: Coupling factor of the inductive link.

$k=\frac{\Im{(Z_{12})}}{\sqrt{\Im{(Z_{11})}\Im{(Z_{22})}}}$

25. **Q1**: Quality factor of primary coil.

$Q_1=\frac{\Im{(Z_{11})}}{\Re{(Z_{11})}}$

26. **Q2**: Quality factor of secondary coil.

$Q_2=\frac{\Im{(Z_{22})}}{\Re{(Z_{22})}}$

27. **Ro**: optimal output load, in Ohms.

$R_o = R_2 \sqrt{1+k^2Q_1Q_2}$

28. **Eff_max**: maximum theoretical efficiency.

$\eta_{max} = \frac{k^2Q_1Q_2}{(1+\sqrt{1+k^2Q_1Q_2})^2}$
 
## Usage
This repository includes two versions of the dataset: a .csv file and a .mat file. The .mat file includes a table (ANNCoilsFEA) and three arrays:
- **In**: includes the 10 geometrical variables that represent the inputs of the ANN: (W1, W2, S1, S2, N1, N2, Dext1, Dext2, Nlay1, Nlay2).
- **Out**: includes the 5 electrical variables that represent the outputs of the ANN: (L1, L2, R1, R2, k).
- **Out_norm**: includes the 5 electrical variables that represent the outputs of the ANN. These variables are preprocessed to enhance the regression capabilities of the ANN: (log10(L1), log10(L2), log10(R1), log10(R2), 10.*k)

For simple and fast tests, the ANN can be created and trained using the *Neural Net Fitting* application of *MATLAB*, either by its graphical GUI or generating the proper training code. More information about this tool can be found in:
- [https://www.mathworks.com/help/deeplearning/ref/neuralnetfitting-app.html](https://www.mathworks.com/help/deeplearning/ref/fitnet.html)
- [https://www.mathworks.com/help/deeplearning/ref/feedforwardnet.html](https://www.mathworks.com/help/deeplearning/ref/neuralnetfitting-app.html)

## Additional information
More information about how to properly train the ANN and adjust their hyperparameters can be found in the article **Neural Network-Based Design of Wireless Power Transfer Systems for Implantable Medical Devices** (Álvaro Rodríguez Fuentes, Miguel Jiménez Carrizosa, Regina Ramos Hortal). 

## Credits
If you use this dataset, please consider the proper citation of the article:

[1] A. Rodriguez-Fuentes, M. J. Carrizosa and R. Ramos, "Neural Network-Based Design of Wireless Power Transfer Systems for Implantable Medical Devices," in IEEE Transactions on Power Electronics, vol. 41, no. 2, pp. 3011-3024, Feb. 2026, doi: 10.1109/TPEL.2025.3614366

## Author
- Name: Álvaro Rodríguez Fuentes
- Affiliation: Centro de Electrónica Industrial y Sistemas Multimodales, Universidad Politécnica de Madrid
- Email: alvaro.rofuentes@upm.es

