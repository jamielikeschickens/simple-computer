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

### Execute
* INMUX  = 0
* AUCNT  = 
* OUTMUX = 1

