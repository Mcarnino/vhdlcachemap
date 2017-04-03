library ieee;

use ieee.std_logic_1164.all;

use ieee.std_logic_arith.all;

use ieee.std_logic_unsigned.all; 

use work.definitions.all;




entity direct_cache is

	port (

			clk : in std_logic;

			rst : in std_logic;

			addr : in std_logic_vector((cache_tag_width + cache_line_width + cache_word_width)-1 downto 0);

			hit : out std_logic;




			cache_we : out std_logic;

			cache_data_from : out std_logic_vector(cache_data_width-1 downto 0);

			cache_line : out std_logic_vector(cache_line_width-1 downto 0);

			cache_tag : out std_logic_vector(cache_tag_width-1 downto 0);

			cache_data_to : out std_logic_vector(cache_data_width-1 downto 0);




			main_mem_addr : out std_logic_vector(main_mem_adr_width-1 downto 0);

			main_mem_data_from : out std_logic_vector(main_mem_data_width-1 downto 0);

			

			state : out integer

		);

end direct_cache;




architecture structural of direct_cache is

	component direct_cache_ctrl is

		port (

				clk, rst : in std_logic;

				addr : in std_logic_vector((cache_tag_width + cache_line_width + cache_word_width)-1 downto 0);

				hit : out std_logic;




				cache_data_from : in std_logic_vector(cache_data_width-1 downto 0);

				cache_we : out std_logic;

				cache_line : out std_logic_vector(cache_line_width-1 downto 0);

				cache_tag : out std_logic_vector(cache_tag_width-1 downto 0);

				cache_data_to : out std_logic_vector(cache_data_width-1 downto 0);




				main_mem_data_from : in std_logic_vector(main_mem_data_width-1 downto 0);

				main_mem_addr : out std_logic_vector(main_mem_adr_width-1 downto 0);

				

				state : out integer

			);

	end component;

	

	component main_mem is

		port (

				clk, rst : in std_logic;

				addr : in std_logic_vector(main_mem_adr_width-1 downto 0);

				data_out : out std_logic_vector(main_mem_data_width-1 downto 0)

			);

	end component;

	

	component cache is

		port (

				clk, rst : in std_logic;

				we : in std_logic;

				line : in std_logic_vector(cache_line_width-1 downto 0);

				data_in : in std_logic_vector(cache_data_width-1 downto 0);

				data_out : out std_logic_vector(cache_data_width-1 downto 0)

			);

	end component;




	--******************************************

	--*	TODO: Add any signal here

	--******************************************

	  signal sig_clk : std_logic;

	  signal sig_rst : std_logic;

	  signal sig_addr : std_logic_vector ((cache_tag_width + cache_line_width + cache_word_width)-1 downto 0);

	  signal sig_cache_data_from : std_logic_vector(cache_data_width-1 downto 0);

	  signal sig_main_mem_data_from : std_logic_vector(main_mem_data_width-1 downto 0);

	  signal sig_noword_addr : std_logic_vector(main_mem_adr_width-1 downto 0);

	  signal sig_main_data_out : std_logic_vector(main_mem_data_width-1 downto 0);

	  signal sig_we : std_logic;

	  signal sig_line : std_logic_vector(cache_line_width-1 downto 0);

	  signal sig_cache_data_in : std_logic_vector(cache_data_width-1 downto 0);

begin

	--******************************************

	--*	TODO: Complete the structural model

	--******************************************

	cache_ctrl_struct : direct_cache_ctrl port map (sig_clk, sig_rst, sig_addr, h, sig_cache_data_from, sig_we,

sig_line, sig_cache_data_in, sig_main_mem_data_from, sig_noword_addr, s);

	cache_struct : direct_cache port map (sig_clk, sig_rst, sig_we, sig_line, sig_cache_data_in,

sig_cache_data_from);

	
	main_mem_struct : main_mem port map (sig_clk, sig_rst, sig_noword_addr,
sig_main_mem_from);												 

end structural;
