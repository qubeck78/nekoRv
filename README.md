# nekoRv
Single stage RISC-V32 IM core written in VHDL.

```
entity nekoRv is
generic
(
    genInitialPC:       std_logic_vector( 31 downto 0 ) := x"00000000";
    genInitialSP:       std_logic_vector( 31 downto 0 ) := x"00005a80";
);

port( 
    
    clk:                in  std_logic;
    reset:              in  std_logic;
    
    a:                  out std_logic_vector( 31 downto 0 );
    din:                in  std_logic_vector( 31 downto 0 );
    dout:               out std_logic_vector( 31 downto 0 );
    
    be:                 out std_logic;
    ready:              in  std_logic;
    wr:                 out std_logic;
    dataMask:           out std_logic_vector( 3 downto 0 );
    
    instrFetchCycle:    out std_logic
    
);
end nekoRv;
```

## Generics
**genInitialPC** - address loaded to PC during reset.

**genInitialSP** - address loaded to Stack Pointer during reset.

## Ports
**clk** - CPU clock.

**reset** - CPU reset, high level active.

**a** - address out ( bits a1 and a0 are not used and set to 0 ).

**din** - data in.

**dout** - data out.

**be** - bus enable, active high during bus cycle ( instruction fetch, data load, data store ).

**ready** - ready input, indicates that bus peripheral put data on bus ( during read cycle ), or wrote data ( during write cycle ). High state ends bus cycle.

**wr** - write enable, active high.

**dataMask** - byte data mask, used commonly during wire cycles. Each bit enables one of 4 octets in 32-bit word. 

  bit 0 - enables d7 - d0
  
  bit 1 - enables d15 - d8
  
  bit 2 - enables d23 - d16
  
  bit 3 - enables d31 - d24

  
  Valid values are: "1111", "1100", "0011", "1000", "0100", "0010", "0001".

**instrFetchCycle** - set to '1' during instruction fetch cycle or '0' when data load/store bus cycle.

  

