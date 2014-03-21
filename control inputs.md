# Fetch/Inc/Exec 
## Fetch
* feed PC into RAM unit to get instruction
* store output of RAM in instruction regs

## Inc
* feed PC into AU
* set carry in of AU
* feed output back into PC

* PC enable
* Input A mux 0
* Output mux 0
* Output dmux 0

## Exec
* pass signal into array of DMUXs to provide a one hot encoding that can be used
  to signal the OR gates in the control path
* pass the FN reg value into the control inputs of the DMUXs



# Instructions
## LDAM
Load MEM[oreg] into A reg.

* Select OREG as input A
* Pass through AU into RAM 
* Select RAM as output
* Store in AREG

* AREG enable
* Input A mux 1
* AU: 0001

## LDBM
Load MEM[oreg] into B reg.

* Select OREG as input A
* Pass through AU into RAM
* Select RAM as output
* Store in BREG

* BREG enable
* Input A mux 1
* AU: 0001
* Output dmx 1

## STAM
Store A reg to MEM[oreg].

* Select  as input A
* Pass through AU into RAM
* Enable RAM write

* RAM enable
* Input A mux 1
* AU: 0001

## LDAC
Load OREG into AREG

* Select OREG as input A
* Pass through AU into output DMX and feed into A
* Enable AREG

* AREG enable
* Output MUX 0
* Input A mux 1
* AU: 0001

## LDBC
Load OREG into BREG

* Select OREG as input A
* Pass through AU into output DMX and feed into B
* Enable BREG

* Out DMX 1
* BREG enable
* Input A MUX 1
* AU: 0001
* Out MUX 0

## LDAP
Load address in PC: AREG <- PC + OREG

* AREG enable
* Out MUX 0
* Input B MUX 0
* Input A MUX 0

## LDAI
Load memory in AREG: AREG <- MEM[OREG + PC]

* AREG enable
* OUT MUX 0
* INPUT B MUX 0
* INPUT A MUX 0

## LDBI
Load memory in BREG: BREG <- MEM[OREG + PC]

* BREG enable
* OUT DMX 1 
* INPUT B MUX 0
* INPUT A MUX 0

## STAI
Store AREG to mem: MEM[BREG + OREG] <- AREG

* MEM enable
* INPUT A MUX 1

## BR
Branch unconditionally: PC <- PC + OREG

* OUT DMX 0
* PC Enable
* INPUT A MUX 0 
* INPUT B MUX 0
* OUTPUT MUX 0 

## BRZ
If AREG = 0:
  PC <- PC + OREG

IF AREG = 0 then enable the following control signals
(therefore pass one hot signal into MUX controlled by comp of AREG)

* PC enable
* OUTPUT DMX 0
* INPUT A MUX 0
* INPUT B MUX 0
* OUTPUT MUX 0

## BRN

If AREG < 0:
  PC <- PC + OREG

We can reuse the path from the last instruction if we change the function of the
AU comp units

## BRB

PC <- BREG

* PC enable
* INPUT A MUX 0
* INPUT A MUX 1
* OUTPUT MUX 0
* OUTPUT DMX 0

## ADD
AREG <- AREG + BREG

* AREG Enable
* OUTPUT MUX 0

