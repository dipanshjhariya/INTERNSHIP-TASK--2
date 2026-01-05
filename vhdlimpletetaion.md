library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;

entity ram is
    generic (
        ADDR_WIDTH : integer := 4;  -- 16 locations
        DATA_WIDTH : integer := 8   -- 8-bit data
    );
    port (
        clk   : in  std_logic;
        we    : in  std_logic;
        addr  : in  unsigned(ADDR_WIDTH-1 downto 0);
        din   : in  std_logic_vector(DATA_WIDTH-1 downto 0);
        dout  : out std_logic_vector(DATA_WIDTH-1 downto 0)
    );
end entity;

architecture Behavioral of ram is
    type ram_type is array (0 to (2**ADDR_WIDTH)-1) of std_logic_vector(DATA_WIDTH-1 downto 0);
    signal mem : ram_type := (others => (others => '0'));
begin
    process(clk)
    begin
        if rising_edge(clk) then
            if we = '1' then
                mem(to_integer(addr)) <= din;
            end if;
            dout <= mem(to_integer(addr));
        end if;
    end process;
end Behavioral;