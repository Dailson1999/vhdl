library ieee;
use ieee.std_logic_1164.all;
use ieee.numeric_std.all;

entity proj_vhdl is
  port (
    A, B: in std_logic_vector(7 downto 0);
    Sub: in std_logic;
    Result: out std_logic_vector(7 downto 0);
    Borrow: out std_logic
  );
end entity proj_vhdl;

architecture Behavioral of proj_vhdl is
  signal internal_result: signed(7 downto 0);
  signal internal_borrow: std_logic;
begin
  process (A, B, Sub)
  begin
   if Sub = '1' then
		internal_result <= signed(A) - signed(B);
	if internal_result < 0 then
		internal_borrow <= '1';
	else
		internal_borrow <= '0';
	end if;
else
  internal_result <= signed(A) + signed(B);
  internal_borrow <= '0';
end if;

    
    Result <= std_logic_vector(internal_result);
    Borrow <= internal_borrow;
  end process;
end architecture Behavioral;
