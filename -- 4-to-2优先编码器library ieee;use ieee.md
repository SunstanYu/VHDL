```vhdl

-- 4-to-2优先编码器
library ieee;
use ieee.std_logic_1164.all;

entity priority_encoder_4to2 is
    port (
        in0: in std_logic;
        in1: in std_logic;
        in2: in std_logic;
        in3: in std_logic;
        out0: out std_logic_vector(1 downto 0)
    );
end priority_encoder_4to2;

architecture behavioral of priority_encoder_4to2 is
begin
    out0 <= "00" when (in3 = '1') else
            "01" when (in2 = '1') else
            "10" when (in1 = '1') else
            "11" when (in0 = '1') else
            "ZZ";
end behavioral;

-- 16-to-4优先编码器
library ieee;
use ieee.std_logic_1164.all;

entity priority_encoder_16to4 is
    port (
        in0: in std_logic;
        in1: in std_logic;
        in2: in std_logic;
        in3: in std_logic;
        in4: in std_logic;
        in5: in std_logic;
        in6: in std_logic;
        in7: in std_logic;
        in8: in std_logic;
        in9: in std_logic;
        in10: in std_logic;
        in11: in std_logic;
        in12: in std_logic;
        in13: in std_logic;
        in14: in std_logic;
        in15: in std_logic;
        out0: out std_logic_vector(3 downto 0)
    );
end priority_encoder_16to4;

architecture behavioral of priority_encoder_16to4 is
    signal out0_0: std_logic_vector(1 downto 0);
    signal out0_1: std_logic_vector(1 downto 0);
    signal out0_2: std_logic_vector(1 downto 0);

begin
    -- 第一级4-to-2编码器
    priority_encoder_4to2_0: entity work.priority_encoder_4to2
    port map (
        in0 => in0,
        in1 => in1,
        in2 => in2,
        in3 => in3,
        out0 => out0_0
    );
    
    priority_encoder_4to2_1: entity work.priority_encoder_4to2
    port map (
        in0 => in4,
        in1 => in5,
        in2 => in6,
        in3 => in7,
        out0 => out0_1
    );
    
    priority_encoder_4to2_2: entity work.priority_encoder_4to2
    port map (
        in0 => in8,
        in1 => in9,
        in2 => in10,
        in3 => in11,
        out0 => out0_2
    );
    
    priority_encoder_4to2_3: entity work.priority_encoder_4to2
    port map (
        in0 => in12,
        in1 => in13,
        in2 => in14,
        in3 => in15,
        out0 => out0
    );
    
    -- 第二级4-to-2编码器
    priority_encoder_4to2_4: entity work.priority_encoder_4to2
    port map(
        
    )
```



```vhdl
library ieee;
use ieee.std_logic_1164.all;

entity priority_encoder_16_to_4 is
    port (
        in_vec : in std_logic_vector(15 downto 0);
        out_vec : out std_logic_vector(3 downto 0);
        r:out std_logic
    );
end entity priority_encoder_16_to_4;

architecture Behavioral of priority_encoder_16_to_4 is
    signal temp_out_vec_0 : std_logic_vector(1 downto 0);
    signal temp_out_vec_1 : std_logic_vector(1 downto 0);
    signal temp_out_vec_2 : std_logic_vector(1 downto 0);
    signal temp_out_vec_3 : std_logic_vector(1 downto 0);
begin
    priority_encoder_4_to_2_0: entity work.priority_encoder_4_to_2
        port map (
            in_vec => in_vec(3 downto 0),
            out_vec => temp_out_vec_0
        );

    priority_encoder_4_to_2_1: entity work.priority_encoder_4_to_2
        port map (
            in_vec => in_vec(7 downto 4),
            out_vec => temp_out_vec_1
        );

    priority_encoder_4_to_2_2: entity work.priority_encoder_4_to_2
        port map (
            in_vec => in_vec(11 downto 8),
            out_vec => temp_out_vec_2
        );

    priority_encoder_4_to_2_3: entity work.priority_encoder_4_to_2
        port map (
            in_vec => in_vec(11 downto 8),
            out_vec => temp_out_vec_3
        );
    
```



```vhdl
entity priority_encoder is
    port (
        input_vector: in std_logic_vector(15 downto 0);
        output_code: out std_logic_vector(3 downto 0);
        activity_flag: out std_logic
    );
end priority_encoder;

architecture Behavioral of priority_encoder is
begin
    process(input_vector)
    begin
        output_code <= "0000";
        activity_flag <= '0';

        if input_vector(15) = '1' then
            output_code <= "1111";
            activity_flag <= '1';
        elsif input_vector(14) = '1' then
            output_code <= "1110";
            activity_flag <= '1';
        elsif input_vector(13) = '1' then
            output_code <= "1101";
            activity_flag <= '1';
        elsif input_vector(12) = '1' then
            output_code <= "1100";
            activity_flag <= '1';
        elsif input_vector(11) = '1' then
            output_code <= "1011";
            activity_flag <= '1';
        elsif input_vector(10) = '1' then
            output_code <= "1010";
            activity_flag <= '1';
        elsif input_vector(9) = '1' then
            output_code <= "1001";
            activity_flag <= '1';
        elsif input_vector(8) = '1' then
            output_code <= "1000";
            activity_flag <= '1';
        elsif input_vector(7) = '1' then
            output_code <= "0111";
            activity_flag <= '1';
        elsif input_vector(6) = '1' then
            output_code <= "0110";
            activity_flag <= '1';
        elsif input_vector(5) = '1' then
            output_code <= "0101";
            activity_flag <= '1';
        elsif input_vector(4) = '1' then
            output_code <= "0100";
            activity_flag <= '1';
        elsif input_vector(3) = '1' then
            output_code <= "0011";
            activity_flag <= '1';
        elsif input_vector(2) = '1' then
            output_code <= "0010";
            activity_flag <= '1';
        elsif input_vector(1) = '1' then
            output_code <= "0001";
            activity_flag <= '1';
        elsif input_vector(0) = '1' then
            output_code <= "0000";
            activity_flag <= '1';
        end if;
    end process;
end Behavioral;

```

testbench

```vhdl
library ieee;
use ieee.std_logic_1164.all;

entity tb_priority_encoder is
end entity tb_priority_encoder;

architecture behavioral of tb_priority_encoder is
    signal in_vec: std_logic_vector(15 downto 0);
    signal out_code: std_logic_vector(3 downto 0);
    signal out_activity: std_logic;
    
    component priority_encoder is
        port (
            in_vec: in std_logic_vector(15 downto 0);
            out_code: out std_logic_vector(3 downto 0);
            out_activity: out std_logic
        );
    end component priority_encoder;
begin
    dut: priority_encoder
        port map (
            in_vec => in_vec,
            out_code => out_code,
            out_activity => out_activity
        );

    stimulus: process
    begin
        in_vec <= "0000000000000000"; -- input 0
        wait for 10 ns;
        assert (out_code = "0000" and out_activity = '0')
            report "Test failed for input 0" severity error;
        
        in_vec <= "0000000000000001"; -- input 1
        wait for 10 ns;
        assert (out_code = "0001" and out_activity = '1')
            report "Test failed for input 1" severity error;
        
        in_vec <= "0000000000000010"; -- input 2
        wait for 10 ns;
        assert (out_code = "0010" and out_activity = '1')
            report "Test failed for input 2" severity error;
        
        in_vec <= "0000000000000011"; -- input 3
        wait for 10 ns;
        assert (out_code = "0001" and out_activity = '1')
            report "Test failed for input 3" severity error;
        
        in_vec <= "0000000000000100"; -- input 4
        wait for 10 ns;
        assert (out_code = "0011" and out_activity = '1')
            report "Test failed for input 4" severity error;
        
        in_vec <= "0000000000010000"; -- input 8
        wait for 10 ns;
        assert (out_code = "0101" and out_activity = '1')
            report "Test failed for input 8" severity error;
        
        in_vec <= "0000000001000000"; -- input 10
        wait for 10 ns;
        assert (out_code = "0111" and out_activity = '1')
            report "Test failed for input 10" severity error;
        
        in_vec <= "1111111111111111"; -- all inputs active
        wait for 10 ns;
        assert (out_code = "0001" and out_activity = '1')
            report "Test failed for all inputs active" severity error;
        
        wait;
    end process stimulus;
end architecture behavioral;

```



```
entity priority_encoder_tb is
end priority_encoder_tb;

architecture Behavioral of priority_encoder_tb is
    component priority_encoder is
        port (
            input_vector: in std_logic_vector(15 downto 0);
            output_code: out std_logic_vector(3 downto 0);
            activity_flag: out std_logic
        );
    end component;

    signal input_vector: std_logic_vector(15 downto 0);
    signal output_code: std_logic_vector(3 downto 0);
    signal activity_flag: std_logic;

begin
    DUT: priority_encoder port map(
        input_vector => input_vector,
        output_code => output_code,
        activity_flag => activity_flag
    );

    -- Test case 1: All inputs are '0'
    test_case_1: process
    begin
        input_vector <= "0000000000000000";
        wait for 10 ns;
        assert output_code = "0000" and activity_flag = '0'
        report "Test case 1 failed" severity error;
        wait;
    end process;

    -- Test case 2: Only one input is '1' (lowest priority)
    test_case_2: process
    begin
        input_vector <= "0000000000000001";
        wait for 10 ns;
        assert output_code = "0001" and activity_flag = '1'
        report "Test case 2 failed" severity error;
        
        input_vector <= "0000000000000010";
        wait for 10 ns;
        assert output_code = "0010" and activity_flag = '1'
        report "Test case 2 failed" severity error;
        
        input_vector <= "0000000000000100";
        wait for 10 ns;
        assert output_code = "0100" and activity_flag = '1'
        report "Test case 2 failed" severity error;
        
        input_vector <= "0000000000001000";
        wait for 10 ns;
        assert output_code = "1000" and activity_flag = '1'
        report "Test case 2 failed" severity error;
        
        input_vector <= "0000000000010000";
        wait for 10 ns;
        assert output_code = "0000" and activity_flag = '1'
        report "Test case 2 failed" severity error;
        wait;
    end process;
```

4-2:

```vhdl
entity priority_encoder_4to2 is
    port (
        input_vector: in std_logic_vector(3 downto 0);
        output_code: out std_logic_vector(1 downto 0);
        activity_flag: out std_logic
    );
end priority_encoder_4to2;

architecture Behavioral of priority_encoder_4to2 is
begin
    process(input_vector)
    begin
        output_code <= "00";
        activity_flag <= '0';
        
        if input_vector(3) = '1' then
            output_code <= "11";
            activity_flag <= '1';
        elsif input_vector(2) = '1' then
            output_code <= "10";
            activity_flag <= '1';
        elsif input_vector(1) = '1' then
            output_code <= "01";
            activity_flag <= '1';
        elsif input_vector(0) = '1' then
            output_code <= "00";
            activity_flag <= '1';
        end if;
    end process;
end Behavioral;

```

16-4

```vhdl
entity priority_encoder is
    port (
        input_vector: in std_logic_vector(15 downto 0);
        output_code: out std_logic_vector(3 downto 0);
        activity_flag: out std_logic
    );
end entity priority_encoder;

architecture Behavioral of priority_encoder is
    component priority_encoder_4to2 is
        port (
            input_vector: in std_logic_vector(3 downto 0);
            output_code: out std_logic_vector(1 downto 0);
            activity_flag: out std_logic
        );
    end component;

    signal input_vector_1: std_logic_vector(3 downto 0);
    signal input_vector_2: std_logic_vector(3 downto 0);
    signal input_vector_3: std_logic_vector(3 downto 0);
    signal input_vector_4: std_logic_vector(3 downto 0);
    signal output_code_1: std_logic_vector(1 downto 0);
    signal output_code_2: std_logic_vector(1 downto 0);
    signal output_code_3: std_logic_vector(1 downto 0);
    signal output_code_4: std_logic_vector(1 downto 0);
    signal activity_flag_1: std_logic;
    signal activity_flag_2: std_logic;
    signal activity_flag_3: std_logic;
    signal activity_flag_4: std_logic;

begin
   
  
    -- Split input_vector into four 4-bit vectors
    input_vector_1 <= input_vector(3 downto 0);
    input_vector_2 <= input_vector(7 downto 4);
    input_vector_3 <= input_vector(11 downto 8);
    input_vector_4 <= input_vector(15 downto 12);

    -- Connect the 4-to-2 priority encoder instances
    priority_encoder_1: priority_encoder_4to2 port map(
        input_vector => input_vector_1,
        output_code => output_code_1,
        activity_flag => activity_flag_1
    );
    priority_encoder_2: priority_encoder_4to2 port map(
        input_vector => input_vector_2,
        output_code => output_code_2,
        activity_flag => activity_flag_2
    );
    priority_encoder_3: priority_encoder_4to2 port map(
        input_vector => input_vector_3,
        output_code => output_code_3,
        activity_flag => activity_flag_3
    );
    priority_encoder_4: priority_encoder_4to2 port map(
        input_vector => input_vector_4,
        output_code => output_code_4,
        activity_flag => activity_flag_4
    );

    -- Determine the highest priority input
    with output_code_1 select
        output_code <= "00" & output_code_2 when "01",
                       "01" & output_code_2 when "10",
                       "10" & output_code_3 when "11",
                       "11" & output_code_4 when others;
    
    if activity_flag_4 = '1' then
            output_code <= "11" & output_code_4;
            activity_flag <= '1';
        elsif activity_flag_3 = '1' then
            output_code <= "10" & output_code_3;
            activity_flag <= '1';
        elsif activity_flag_2 = '1' then
            output_code <= "01" & output_code_2;
            activity_flag <= '1';
        elsif activity_flag_1 = '1' then
            output_code <= "00" & output_code_1;
            activity_flag <= '1';
        else  output_code <= "0000";
        end if;

    -- Determine the activity flag
    activity_flag <= activity_flag_1 or activity_flag_2 or
                     activity_flag_3 or activity_flag_4;

end architecture Behavioral;

```

