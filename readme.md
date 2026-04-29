### Half Adder
ha.vhdl
```
library ieee;
use ieee.std_logic_1164.all;
entity ha is
		port
		(
			a: in std_ulogic;
			b: in std_ulogic;
			o: out std_ulogic;
			c: out std_ulogic
		);
end ha;

architecture behave of ha is
begin
	o <= a xor b;
	c <= a and b;
end behave;
```
va_tb.vhdl
```
library ieee; 
use ieee.std_logic_1164.all;

entity ha_tb is
end ha_tb;

architecture test of ha_tb is
	component ha
		port
		(
			a: in std_ulogic;
			b: in std_ulogic;
			o: out std_ulogic;
			c: out std_ulogic
		);
	end component;
	
	signal a, b, o, c : std_ulogic;
begin
	half_adder: ha port map (a => a, b => b, o => o, c => c);
	
	process begin
	
		a <= 'X';
		b <= 'X';
		wait for 1 ns;
		
		a <= '0';
		b <= '0';
		wait for 1 ns;
		
		a <= '0';
		b <= '1';
		wait for 1 ns;
		
		a <= '1';
		b <= '0';
		wait for 1 ns;
		
		a <= '1';
		b <= '1';
		wait for 1 ns;
		
		assert false report "Reached end of test";
		wait;
	
	end process;
	
end test;
```
![Image](https://github.com/user-attachments/assets/5d5ef5a1-5e65-4185-af51-344c2710800d)

### D Flip-Flop
dff.vhdl
```
library ieee;
use ieee.std_logic_1164.all;

entity DFF is
port( din: in std_logic;
clk: in std_logic;
rst: in std_logic;
dout: out std_logic);
end DFF;

architecture behavioral of DFF is
begin
process(rst,clk,din)
begin
if (rst='1') then
dout<='0';
elsif(rising_edge(clk)) then
dout<= din;
end if;
end process;

end behavioral;
```
dff_tb.vhdl
```
LIBRARY ieee;
USE ieee.std_logic_1164.ALL;

ENTITY DFF_tb IS
END DFF_tb;

ARCHITECTURE behavior OF DFF_tb IS 

    COMPONENT DFF
    PORT(
         din : IN  std_logic;
         clk : IN  std_logic;
         rst : IN  std_logic;
         dout : OUT  std_logic
        ); 
    END COMPONENT;
    
   signal din : std_logic := '0';
   signal clk : std_logic := '0';
   signal rst : std_logic := '1';
   signal dout : std_logic;

   constant clk_period : time := 10 ns;

BEGIN

 uut: DFF PORT MAP (
          din => din,
          clk => clk,
          rst => rst,
          dout => dout
        );

  clk_process :process
  begin
  clk <= '0';
  wait for clk_period/2;
  clk <= '1';
  wait for clk_period/2;
  if NOW > 200 ns then
  wait;
  end if;
  end process;

  stim_proc: process
  begin  

  rst <= '1';
  wait for 50 ns; 

  rst <= '0';
  din <= '0';
  wait for 50 ns;
  
  rst <= '0';
  din <= '1';  
  wait for 50 ns;

  rst <= '1';
  wait;

  end process;

END;
```
![Image](https://github.com/user-attachments/assets/3beb9288-07aa-4202-aa9d-6d3cff183765)
## Data Analysis

I have provided below some snapshots of my experimentation with some data analysis capabilities that python can deliver, through use of histograms, charts including time series, and a scatter plot with a linear trednline.

## Edit plt_final.py and plt_cv2.py to read CSV file with customized plot titles

plt_final.py
> data = read_csv('rpidata.csv')

plt_cv2.py
> X = read_csv('rpidata.csv', usecols=[1])
> Y = read_csv('rpidata.csv', usecols=[2])

## Python plt_final
![Image](https://github.com/user-attachments/assets/9e7a1875-3bfd-4c72-a2a8-8081b19c7575)

![Image](https://github.com/user-attachments/assets/194d4eaf-8a44-4601-babf-e7a74b3ce674)

![Image](https://github.com/user-attachments/assets/b4a1878f-f8bd-4e12-ac7d-06ffeb026493)

![Image](https://github.com/user-attachments/assets/bd64bff1-4d94-4913-b9ce-48dcaa430e13)

![Image](https://github.com/user-attachments/assets/97045d2b-3b89-47ea-a226-848803e4769a)

![Image](https://github.com/user-attachments/assets/8fdaaad5-2c08-476f-9e8b-fd7ba1cde1f7)
## Python plt_cv2
![Image](https://github.com/user-attachments/assets/0bab968c-64b6-4f22-92af-e76e337b3f67)
