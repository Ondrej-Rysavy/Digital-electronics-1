# Digital-electronics-1

## Part One: Link to the repository

Link: https://github.com/Simon-Roubal/Digital-electronics-1

## Part Two: function f(c,b,a) table

| **c** | **b** |**a** | **f(c,b,a)** |
| :-: | :-: | :-: | :-: |
| 0 | 0 | 0 |  |
| 0 | 0 | 1 |  |
| 0 | 1 | 0 |  |
| 0 | 1 | 1 |  |
| 1 | 0 | 0 |  |
| 1 | 0 | 1 |  |
| 1 | 1 | 0 |  |
| 1 | 1 | 1 |  |

## Part Three: Verification of De Morgan's laws

Link to EDA: https://www.edaplayground.com/x/QeJB

Code:
```vhdl
architecture dataflow of gates is
begin
    f_o      <= (((not b_i) and a_i) or ((not c_i) and (not b_i)));
    fnand_o  <= (a_i nand (not b_i)) nand ((not b_i) nand (not c_i));
    fnor_o   <= (a_i nor (not c_i)) nor b_i;
end architecture dataflow;
```
Screen:

## Part Four: Verification of Distributive laws


Link to EDA: https://www.edaplayground.com/x/J7ZZ

Code:
```vhdl
architecture dataflow of gates is
begin
    f1_o  <= x_i and (not x_i);
    f2_o  <= x_i or (not x_i);
    f3_o  <= x_i or  x_i  or  x_i  or  x_i;
    f4_o  <= x_i and  x_i  and  x_i  and x_i;
    f11_o <= (x_i and  y_i) or (x_i and  z_i);
    f12_o <= x_i and (y_i or z_i);
    f21_o <= ((x_i or y_i) and (x_i or z_i));
    f22_o <= x_i or (y_i and  z_i);
end architecture dataflow;
```
Screen:
