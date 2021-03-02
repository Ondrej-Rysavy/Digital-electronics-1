# Part One: Link to the reposiory
https://github.com/Simon-Roubal/Digital-electronics-1/tree/main/Labs/03-vivado
# Part Two: Table with connection of 16 slide switches and 16 LEDs on Nexys A7 board
| **Part** | **Pin** | **Active** |
| :-: | :-: | :-: |
| LED0 | H17 | High |
| LED1 | K15 | High |
| LED2 | J13 | High |
| LED3 | N14 | High |
| LED4 | R18 | High |
| LED5 | V17 | High |
| LED6 | U17 | High |
| LED7 | U16 | High |
| LED8 | V16 | High |
| LED9 | T15 | High |
| LED10 | U14 | High |
| LED11 | T16 | High |
| LED12 | V15 | High |
| LED13 | V14 | High |
| LED14 | V12 | High |
| LED15 | V11 | High |
| SW0 | J15 | - |
| SW1 | L16 | - |
| SW2 | M13 | - |
| SW3 | R15 | - |
| SW4 | R17 | - |
| SW5 | T18 | - |
| SW6 | U18 | - |
| SW7 | R13 | - |
| SW8 | T8 | - |
| SW9 | U8 | - |
| SW10 | R16 | - |
| SW11 | T13 | - |
| SW12 | H6 | - |
| SW13 | U12 | - |
| SW14 | U11 | - |
| SW15 | V10 | - |

# Part Three: Two-bit wide 4-to-1 multiplexer

## Listing of VHDL architecture

```vhdl
library ieee;
use ieee.std_logic_1164.all;

entity mux_2bit_4to1 is
    port(
        a_i           : in  std_logic_vector(2 - 1 downto 0);
        b_i           : in  std_logic_vector(2 - 1 downto 0);
        c_i           : in  std_logic_vector(2 - 1 downto 0);
        d_i           : in  std_logic_vector(2 - 1 downto 0);
        
        sel_i         : in  std_logic_vector(2 - 1 downto 0);

        f_o    :out std_logic_vector(2 - 1 downto 0)
    );
end entity mux_2bit_4to1;

architecture Behavioral of mux_2bit_4to1 is
begin
    f_o     <=  a_i when (sel_i="00")else
                b_i when (sel_i="01")else
                c_i when (sel_i="10")else
                d_i;

end architecture Behavioral;
```
## Listing of VHDL stimulus process from testbench file

```vhdl
library ieee;
use ieee.std_logic_1164.all;

entity tb_mux_2bit_4to1 is

end entity tb_mux_2bit_4to1;

architecture testbench of tb_mux_2bit_4to1 is

    -- Local signals
    signal s_a       : std_logic_vector(2 - 1 downto 0);
    signal s_b       : std_logic_vector(2 - 1 downto 0);
    signal s_c       : std_logic_vector(2 - 1 downto 0);
    signal s_d       : std_logic_vector(2 - 1 downto 0);
    signal s_sel     : std_logic_vector(2 - 1 downto 0);
    signal s_f       : std_logic_vector(2 - 1 downto 0);

begin
    uut_mux_2bit_4to1 : entity work.mux_2bit_4to1
        port map(
            a_i           => s_a,
            b_i           => s_b,
            c_i           => s_c,
            d_i           => s_d,
            sel_i         => s_sel,
            
            f_o           => s_f
        );

    p_stimulus : process
    begin
        -- Report a note at the begining of stimulus process
        report "Stimulus process started" severity note;

        s_d <= "00";s_c <= "00";s_b <= "00"; s_a <= "00";
        s_sel <= "00";  wait for 100 ns;
        
        s_d <= "10";s_c <= "01";s_b <= "01"; s_a <= "00";
        s_sel <= "00";  wait for 100 ns;
        
        s_d <= "10";s_c <= "01";s_b <= "01"; s_a <= "11";
        s_sel <= "00";  wait for 100 ns;
        
        s_d <= "10";s_c <= "01";s_b <= "01"; s_a <= "00";
        s_sel <= "01";  wait for 100 ns;
        
        s_d <= "10";s_c <= "01";s_b <= "11"; s_a <= "00";
        s_sel <= "01";  wait for 100 ns;
        
        s_sel <= "10";  wait for 100 ns;
        
        s_sel <= "11";  wait for 100 ns;

        -- Report a note at the end of stimulus process
        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;

end architecture testbench;
```
## Screenshot with simulated time waveforms

![alt text](https://github.com/Simon-Roubal/Digital-electronics-1/blob/main/Labs/03-vivado/Pictures/out.png?raw=true)

# Guide to Vivado

## Založení projektu ve Vivadu

### Klineme na záložku File/Project/New…

![obrazek](https://user-images.githubusercontent.com/77580298/109648182-9b6fca80-7b5a-11eb-97c9-c0742ffc940b.png)

### Otevře se nám okno s vytvořením nového projektu, klikneme na Next

![obrazek](https://user-images.githubusercontent.com/77580298/109648220-a9bde680-7b5a-11eb-8e96-6faabe0ae2d4.png)

### Zde zvolíme jméno projektu a jeho umístění

![obrazek](https://user-images.githubusercontent.com/77580298/109648505-fc979e00-7b5a-11eb-9153-1bf0beb41947.png)

### Typ projektu zvolíme RTL

![obrazek](https://user-images.githubusercontent.com/77580298/109648554-08836000-7b5b-11eb-8296-1bcdc1a5977d.png)

### Vytvoříme VHDL souce file se stejným názvem jako projekt

![obrazek](https://user-images.githubusercontent.com/77580298/109648600-16d17c00-7b5b-11eb-893a-1658c6fbcfeb.png)
![obrazek](https://user-images.githubusercontent.com/77580298/109648608-19cc6c80-7b5b-11eb-8fa8-2596f7c3135c.png)

### Constrain soubory nevytváříme

![obrazek](https://user-images.githubusercontent.com/77580298/109648641-26e95b80-7b5b-11eb-896e-c537e906baf0.png)

### Nahoře vybereme záložku Boards

![obrazek](https://user-images.githubusercontent.com/77580298/109648665-2fda2d00-7b5b-11eb-9578-b21050c34802.png)

### Zvolíme desku Nexys A7-50

![obrazek](https://user-images.githubusercontent.com/77580298/109648706-3b2d5880-7b5b-11eb-8158-3127c7569456.png)

### A potvrdíme vytvoření objektu

![obrazek](https://user-images.githubusercontent.com/77580298/109648736-44b6c080-7b5b-11eb-9ff2-62c24bd4bd0f.png)

### Pokud chceme můžeme předdefinovat vstupy

![obrazek](https://user-images.githubusercontent.com/77580298/109648764-4da79200-7b5b-11eb-9e6b-1e1cbcc01cb0.png)

### Nyní máme vytvořený projekt a v části sources otevřeme náš zdrojový soubor

![obrazek](https://user-images.githubusercontent.com/77580298/109648820-5b5d1780-7b5b-11eb-8993-ebefe47f655f.png)

### Nyní můžeme už náš program editovat

![obrazek](https://user-images.githubusercontent.com/77580298/109648852-64e67f80-7b5b-11eb-9f52-ac85da176b71.png)

## Vytvoření Test benche

### Klikneme na záložku File/Add Sources…

![obrazek](https://user-images.githubusercontent.com/77580298/109648900-762f8c00-7b5b-11eb-91b4-47180b9d8c46.png)

### Vybereme Add or create simulation sources

![obrazek](https://user-images.githubusercontent.com/77580298/109648928-7e87c700-7b5b-11eb-88bd-fbd1c45de860.png)

### Vytvoříme VHDL source file tb_/název/ a dokončíme

![obrazek](https://user-images.githubusercontent.com/77580298/109648959-8a738900-7b5b-11eb-8ce7-4eb82daee3de.png)
![obrazek](https://user-images.githubusercontent.com/77580298/109648968-8d6e7980-7b5b-11eb-82b4-0ac920dc2ef9.png)

### Pokud chceme můžeme předdefinovat vstupy
 
![obrazek](https://user-images.githubusercontent.com/77580298/109649009-995a3b80-7b5b-11eb-9130-810650c640ac.png)

### Test bench opět nalezneme v záložce sources

![obrazek](https://user-images.githubusercontent.com/77580298/109649038-a24b0d00-7b5b-11eb-813a-361e82195f2a.png)

## Spuštění simulace

### Klineme na Flow/Run Simulation/ Run Behavioral simulation

![obrazek](https://user-images.githubusercontent.com/77580298/109649083-b42cb000-7b5b-11eb-82db-51445cb53444.png)

###  Pro dobré zobrazení simulace použijeme funkci Zoom fit

![obrazek](https://user-images.githubusercontent.com/77580298/109649122-bf7fdb80-7b5b-11eb-8139-827d12d38188.png)

## Vytvoření constrains souboru

### Klikneme na záložku File/Add Sources…

![obrazek](https://user-images.githubusercontent.com/77580298/109649162-ce668e00-7b5b-11eb-841c-b935f5efa217.png)

### Vybereme Add or create constrains

![obrazek](https://user-images.githubusercontent.com/77580298/109649184-d8888c80-7b5b-11eb-9447-2bf5cd47ce94.png)

### Vytvoříme nový XDC source file a potvrdíme

![obrazek](https://user-images.githubusercontent.com/77580298/109649222-e4744e80-7b5b-11eb-81bf-403b0abcfabe.png)
![obrazek](https://user-images.githubusercontent.com/77580298/109649243-ec33f300-7b5b-11eb-838f-179d2c6286de.png)

### Opět otevřeme přes sources

![obrazek](https://user-images.githubusercontent.com/77580298/109649271-f524c480-7b5b-11eb-91fb-3d1cc80ddc87.png)

### Vložíme data z Githubu výrobce 

![obrazek](https://user-images.githubusercontent.com/77580298/109649289-fe159600-7b5b-11eb-8257-6ffd8a60c612.png)

### Změníme požadované vstupy a výstupy 

![obrazek](https://user-images.githubusercontent.com/77580298/109649307-079efe00-7b5c-11eb-8d52-89885e269bd0.png)




