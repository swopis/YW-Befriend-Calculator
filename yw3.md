Access: https://swopis.github.io/YW-Befriend-Calculator/yw3/

> [!CAUTION]
> This section is not finished. It may contain errors or miss information.

## How does Befriending work?
Make sure to first read the [Common Starting Point](README.md#common-starting-point).  
The resulting number will be referenced as `difficulty`

### Base Probability
The base probability can be calculated using the following formula:  

$$ 1 : 2^{difficulty + 1} $$

For example if the difficulty is `2` the base probability is $1:2^{3}$ or $1:8$ or 12.5%.

### Player-Influenced Bonuses
After calculating the base chance, the bonuses the player can influence are _added_:
* food bonus
* Yo-Kai blaster bonus
* superstar soul/popularity skill
* unpopularity skill
* wisp bonus
* shrine bonus (1%)
* aura bonus

> [!NOTE]
> Each bonus can only be added once. Nothing stacks.

#### Food
| Difficulty | Food Tier 1 | Food Tier 2 | Food Tier 3 | Food Tier 4 |
|------------|-------------|-------------|-------------|-------------|
| 2          | 10%         | 15%         | 20%         | 25%         | 
| 3          | 5%          | 8%          | 11%         | 14%         |
| 4          | 4%          | 6%          | 8%          | 10%         |
| 5          | 4%          | 5%          | 6%          | 7%          |
| 6          | 3%          | 4%          | 5%          | 6%          |
| 7          | 2%          | 3%          | 4%          | 5%          |
| 8          | 1%          | 2%          | 3%          | 4%          |
| 9          | 1%          | 1%          | 2%          | 3%          |

If the given food was the Yo-Kai's favorite food the value gets multiplied by 1.5. If it was the Yo-Kai's hated food it gets multiplied by 0.4.
For example, if you gave a tier 4 favorite food at difficulty 1 the bonus will be 37.5% instead of 25%.

The forbidden fruit guarantees this Yo-Kai to get selected.

#### Yo-Kai Blaster
If the Yo-Kai blaster was set to befriend mode, a bonus depending on how "full" the Yo-Kai was shot and a factor. This factor depends on the `difficulty`.

| Difficulty | Factor       |
|------------|--------------|
| 2          | 0.35         |
| 3          | 0.20         |
| 4          | 0.15         |
| 5          | 0.10         |
| 6          | 0.07         |
| 7          | 0.05         |
| 8          | 0.04         |
| 9          | 0.03         |

For example, a difficulty 9 Yo-Kai with max blaster level will get a $100 * 0.03 = 3\\%$ bonus.

#### Skills / Souls
| Difficulty | popularity / superstar soul | unpopularity |
|------------|-----------------------------|--------------|
| 2          | 10%                         | -10%         |
| 3          | 5%                          | -4.5%        |
| 4          | 4%                          | -2%          |
| 5          | 4%                          | -1%          |
| 6          | 3%                          | -0.5%        |
| 7          | 2%                          | -0.25%       |
| 8          | 1%                          | -0.1%        |
| 9          | 1%                          | -0.05%       |

#### Wisps
| Difficulty | Blue Wisp | Golden Wisp |
|------------|-----------|-------------|
| 2          | 15%       | 37.5%       |
| 3          | 8%        | 21%         |
| 4          | 6%        | 15%         |
| 5          | 5%        | 10.5%       |
| 6          | 4%        | 9%          |
| 7          | 3%        | 7.5%        |
| 8          | 2%        | 6%          |
| 9          | 1%        | 4.5%        |

#### What is the shrine bonus?
Sometimes after you have put your 1$ into the shrine in Mt. Wildwood, you get the message: "I have a feeling that I've got a lot more friends now.".
After this message every Yo-Kai has a 1% higher chance of approaching you after a battle for one day.

#### Auras
There are 3 different aura tiers.
| Aura            | Aura Tier |
|-----------------|-----------|
| Whistle         | 1         |
| Birdsong        | 1         |
| Porous          | 2         |
| Extreme Porous  | 2         |
| Good Fortune    | 1         |
| Enma            | 3         |
| Enma EX         | 3         |
| Deva Enma       | 2         |

Then the bonus depends on aura tier and difficulty.
| Difficulty | Aura Tier 1 | Aura Tier 2 | Aura Tier 3 |
|------------|-------------|-------------|-------------|
| 2          | 15%         | 20%         | 25%         |
| 3          | 8%          | 11%         | 14%         |
| 4          | 6%          | 8%          | 10%         |
| 5          | 5%          | 6%          | 8%          |
| 6          | 4%          | 5%          | 6%          |
| 7          | 3%          | 4%          | 5%          |
| 8          | 2%          | 3%          | 4%          |
| 9          | 1%          | 2%          | 3%          |

If the aura Enma or Enma EX is active and the enemy Yo-Kai has the tribe Enma, the Yo-Kai will always get selected.

## Modding opportunities
The befriend bonuses are all stored in the chara param file:
```
CHARA_FRIEND_RATE_INFO (
    BaseChance|False
    Tier1Bonus|False
    Tier2Bonus|False
    Tier3Bonus|False
    Tier4Bonus|False
    Popularity|False
    Unpopularity|False
    BlueWisp|False
    GoldenWisp|False
    BlasterFactor|False
    ShrineBonus|False
    Unk1|False
    Unk2|False
    AuraTier1|False
    AuraTier2|False
    AuraTier3|False
)
```
