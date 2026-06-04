# Yokai Watch Befriend Rate Calculators
Access: https://swopis.github.io/YW-Befriend-Calculator/

> [!NOTE]
> This guide only covers befriends that happen after a battle with "Yo-Kai is approaching you."

## Calculating the Difficulty
In Yo-Kai Watch 1, 2 and 3 each Yo-Kai gets assigned a 4-byte-descriptor that determines it's befriend rates.  
These descriptors can be found [here](friend_rates.md).  

### Yo-Kai Watch 1
In Yo-Kai Watch 1, the difficulty is now determined by shifting the descriptor value to the right by 28 minus the amount of times you already befriended that specific Yo-Kai times 4 and only taking the last 4 bit.
```python
difficulty = descriptor << (28 - already_befriended * 4) & 0xF
```
This means in hex you can read the n-th. value from the left, where n is the amount of that specific Yo-Kai already befriended.  
The befriend rate then depends heavily on that number. Generally speaking, the higher the number, the smaller the befriend rate.  
You cannot befriend the same Yo-Kai more than 6 times even though the descriptor sometimes has more values.
In the following sections this number will be referenced as `difficulty`.

### Yo-Kai Watch 2 and 3
In Yo-Kai Watch 2 and 3, the difficulty is now determined by shifting the descriptor value to the right by the amount of times you already befriended that specific Yo-Kai times 4 and only taking the last 4 bit.
```python
difficulty = descriptor << (already_befriended * 4) & 0xF
```
This means in hex you can read the n-th. value from the right, where n is the amount of that specific Yo-Kai already befriended.  
The befriend rate then depends heavily on that number. Generally speaking, the higher the number, the smaller the befriend rate.  
In the following sections this number will be referenced as `difficulty`.

## Multiple Selections
In both Yo-Kai Watch 2 and Yo-Kai Watch 3, there is an rng roll for every enemy Yo-Kai. If multiple are selected, the one that befriends is determined as follows:  
For all selected Yo-Kai, the difficulty for having zero of them befriended is calculated. Then the Yo-Kai with the highest value gets selected.  
If there are still multiple Yo-Kai selected, the befriending Yo-Kai will be determined randomly with equal probability.


## Games
* [Yo-Kai Watch 1](yw1.md)
* [Yo-Kai Watch 2](yw2.md)
* [Yo-Kai Watch 3](yw3.md)

## Bit-Flags
* `0x0CC4EC4E`: always 0% befriend probability
* `0xABCB4EE6`: always 100% befriend probability
