# 4 Bit Synchronous Up Counter

This chip is a 4 bit synchronous binary up counter.

## What it does

On every **rising edge** of the clock, the counter increments by 1:

- `0000 → 0001`
- `0001 → 0010`
- `0010 → 0011`
- ...
- `1111 → 0000`

All output bits change together because the counter is **synchronous**.

## Pins

| Pin | Name | Direction | Description |
|-----|------|-----------|-------------|
| 1 | CLK | Input | Clock input. Counter updates on the rising edge |
| 2 | RST | Input | Reset input. When high, counter resets to `0000` |
| 3 | EN | Input | Enable input. When high, counter increments on clock edge |
| 4 | Q0 | Output | Least significant bit |
| 5 | Q1 | Output | Output bit 1 |
| 6 | Q2 | Output | Output bit 2 |
| 7 | Q3 | Output | Most significant bit |

## Behavior

- If `RST = 1`, the counter resets to `0000`
- Else if `EN = 1` and `CLK` has a rising edge, the counter increments
- Else the current count is held

## Truth Summary

| RST | EN | CLK Rising Edge | Next State |
|-----|----|------------------|------------|
| 1 | X | X | `0000` |
| 0 | 0 | Yes | Hold current value |
| 0 | 1 | Yes | Count up by 1 |
| 0 | X | No | Hold current value |

## Example Test

To test the chip in Wokwi:

1. Connect a square wave clock source to `CLK`
2. Connect a pushbutton or logic input to `RST`
3. Tie `EN` high
4. Connect `Q0`, `Q1`, `Q2`, and `Q3` to LEDs

Expected result:

- The outputs count upward in binary on each clock pulse
- Pressing reset forces the output back to `0000`

## Example Count Sequence

| Clock Pulses | Q3 Q2 Q1 Q0 |
|--------------|-------------|
| 0 | 0000 |
| 1 | 0001 |
| 2 | 0010 |
| 3 | 0011 |
| 4 | 0100 |
| 5 | 0101 |
| 6 | 0110 |
| 7 | 0111 |
| 8 | 1000 |
| 9 | 1001 |

## Notes

This design is useful for:

- Frequency division
- Digital event counting
- Sequence generation
- Learning synchronous sequential logic
