# Diablo 2 Melee Dex Analysis

or _"Everything you wanted to know about Chance To Hit, but were afraid of the Math."_

This guide is geared towards all players: newbies, and veterans alike. Some results will be obvious to the experienced player, and some will be new. I hope everyone enjoys finding a little insight into "Why and How does the game work?"

Note: Don't panic over the Math & formulas -- I'll try not to bog the reader down with them. If they make you anxious, feel free to skip them or just jump right to the conclusions if you want. ;-) While they are used to show where my findings come from, it is not necessary to exactly understand the formulas. I will explain what they mean (or at least try to.)

# Introduction

We all know adding Dex improves your Chance To Hit for melee characters. However, this raises some important questions:

- Is there a minimum Dex you can get away with?
- Is there such a thing as too much Dex?
- When I increase my Dex, how does my Chance To Hit % change?
- How much Dex should I have to have a good Chance To Hit %?

This document investigates how much Dex you need, and the inter-dependencies of AR, Levels (both Character and Monster), and Chance To Hit along with introducing the concept of "Virtual Dex."

# Abbreviations

* `AR` = Attack Rating (The higher the number the better the chance the attacker has to hit)
* `DR` = Defense Rating. (The higher the number, the better the chance the defender has to defend.)
* `Barb` = Short for Barbarian.
* `Base Dex` = Points in Dex if you unequipped all gear giving a bonus.
* `BO` = Barbarian's Battle Orders. Increases max Life and Mana
* `C2H%` = Chance To Hit Percent. Diablo 2, unfortunately, caps this at 5% (min) and 95% (max).
* `CLev` = Character Level.
* `Gear` = The equipment (armor, weapons, charms, etc) that your character uses.
* `Frenzier` = Barb with Frenzy
* `Mauler` = Barb with Mace (usually IK Maul and Berserk.)
* `MLev` = Monster Level.
* `Str/Dex/Vit/Eng` = Character stats: Strength / Dexterity / Vitality / Energy.
* `SLev` = Skill Level. (You can only invest up to 20 points into skills, although skills can be higher, via gear.)
* `Stats` = Any combination of your character statistics (Str, Dex, Vit, or Eng.)
* `ROI` = Return On Investment. Technically the ratio of : return / cost. Some skills have a linear ROI (every skill point invested you receive a straight +X% increase.) Others have a decreasing ROI (you get less +X% for every skill point invested.)
* `Virtual Dex` = If you unequipped your +AR items, the difference of how much real Dex you would need to match the same AR.

# Background

Although I'll be using my 2 Barbs as examples to see the various relationships between stats and their effects, the results are applicable to any character with melee attacks. (The Mauler and the Frenzier represent the extreme and normal, respectively, investment Dex strategies for melee characters.)

* Level 99 Mauler (20 BO, 20 Berserk), with stats invested ONLY into Str & Vit. Base Dex is (20), but with gear (IK gloves, belt, helm) is 50.

* Level 71 Frenzier, stats 200 Str, 200 Vit, 40 Dex (Base) but is 66 with dual Ali Baba's & gloves. AR = 1433 with Gear.

For the C2H% calculations, I use Hell Meph as my "training dummy", since he's high level, and easy to get to.

/!\ **TIP:** To check the in-game display of C2H%, open your character stats, and hover your mouse over the AR display.

Arreat Summit gives these stats for Hell Meph:

* MLev: 90
* DR: 780
* Reference: https://classic.battle.net/diablo2exp/monsters/act3-mephisto.shtml

And these 2 key formulas:

    {Equation 1.} C2H% = 100 * AR / (AR + DR) * 2 * CLev / (Clev + MLev)
    {Equation 2.} DexAR = (Dex * 4) - 8 (corrected)

Reference:

* https://classic.battle.net/diablo2exp/basics/characters.shtml

/!\ **Note:** Arreat Summit has an incorrect formula for DexAR! They list DexAR as being offset by -28, but it really should be -8.

We'll also make use of a few percent formulas from Algebra.
The percent increase from Original Value to New Value, is defined as:

    B = A + P%

Which can be written as:

    {Equation P1.} %Change = {(B/A) - 1} * 100

and re-arranging to solve for B

    {Equation P2.} B = A * {1 + (%Change / 100)}

# Questions

What prompted me to take a closer look at the ROI for Dex, was that after building a MF Frenzy Barb the same way as my Mauler (and seeing how his C2H% would still be bad at CLev 99), I wanted to answer these questions:

Q1. **Factors affecting C2H%**

* i. If I add Dex, how does my C2H% change?
* ii. If I add AR, how does my C2H% change?
* iii. If I increase my level, how does my C2H% change?
* iv. Why do 2 chars, both at CLev 99 and with low Dex, have such a drastic difference in C2H%?

Q2. **What is the optimal way to increase my C2H%?**

Q3. **How do I figure out how much Dex I ultimately need ?**

* i. If I need a certain C2H%, how much AR do I need?
* ii. Given my desired AR, how much Dex do I need to reach my desired C2H%?

Q4. **How does changing AR affects C2H% ?**

* And since I'm talking about Dex, I'll throw in this question & (answer) too:

Q5. **How much Dex should I have to maintain a good blocking rate?**

# Formulas

Onward to the math analysis and answers! (Don't worry, I've done it for you.)

If we rearrange Eq. 1, and solve for AR, writing down partial results, we get these handy formulas:

    {Equation 3.} X = (CLev + MLev) / (100 * 2 * Clev)

Notice how this is effectively a constant once we reach our maximum level.

    {Equation 4.} Y = X * C2H%
    {Equation 5.} AR = (Y * DR) / (1 - Y)

This is the same formula as Eq. 1, but this alternate form makes it easier to solve later equations.

    {Equation 6.} C2H% = AR / (AR + DR) * (1 / X)

I'm going to give some examples first so we get an intuitive feel for the various relationships between stats. Then we'll calculate the exact formulas we need to precisely answer the questions.

---

# A1. Factors Affecting C2H%

Pretty straightforward - just list all the variables used in Formulas 1 & 2. :-)

* AR,
* DR,
* CLev,
* MLev, and
* Dex

Now to answer the sub-questions:

* i) **Effect of Dex on C2H%**

Example:

* When my Mauler reached CLev 99, (2584 AR) he had a C2H% of 79%. After I gave him +100 Dex points (Dex now effectively 150), AR went up to 2813 and the C2H% moved up to 81%.

* I was shocked to see that adding the extra 100 Dex only increased my C2H% by a measly +2 !! That's another 400 life (actually ~800% life with 20 BO) I just threw away by not investing into Vit !

**Immediate Conclusion:** Dex has a bad ROI for a pure Mauler (when you already have a high AR.)

* ii) **Effect of AR on C2H%**

At first we might be tempted to double our AR to double our C2H%, but looking at the Equation 6, we see that won't work, unfortunately.

    {Equation 6.} C2H% = AR / (AR + DR) * (1 / X)

Proof:

    Original C2H% = AR / (AR + DR) * (1 / X)

and

    New C2H% = AR*2 / (AR*2 + DR) * (1 / X)

Using the percent formula (Eq P1.) where A & B are our original and new C2H%s (respectively),

    PercentIncrease = {(NewC2H% / OrginalC2H%) - 1} / 100
    = {AR*2 / (AR*2 + DR) * (1 / X)} / {AR / (AR + DR) * (1 / X)}

It looks complicated, but it's not too bad. 1/X cancels in both numerator and denominator.

    = ({AR*2 / (AR*2 + DR)} / {AR / (AR + DR)} - 1) * 100

And using the trick that when dividing by a fraction, it's the same as multiplying by the inverse, so we're left with:

    = ({AR*2 / (AR*2 + DR) * (AR + DR) / AR} - 1) * 100

Distributing, collecting common terms, yada yada yada, we're left with:

    = {(AR + DR) / (AR + DR/2) - 1} * 100

If our C2H% really did double, we would expect to see the above in a form similar to P = 2 * Formula. Instead we have decreasing returns as we raise our AR.

Let's work out the percent increase we will get in our C2H% when we change our AR for the general case:

**Proof:**

Same as above, but substituting N for 2 above:

    {Equation 7.} PercentC2H%Increase = {(AR + DR) / (AR + DR/N) - 1} * 100

  * If N = 2, then we double our AR.
  * If N = 0.5, then we half our AR.

Example:

**Q.** What's the C2H% and % Increase for our Frenzy Barb (Level 71) when we double his AR (from 1433 to 2866) ?

**Answer:**

We actually have a few ways to calculate this, so I'll present them all:

Using our newly derived Formula 7 (would be a pity not to use it, don't ya know :-)

    PercentIncreaseC2H% = {(1433 + 780) / (1433 + 780/2) - 1} * 100
    = 21.3933% (Result A.)

Notice that this isn't an absolute delta, but a relative one:
The new C2H% is 21.3933% more then the current C2H%.
(Later, we'll calculate how much our AR needs to change, in order to double our C2H%.)

Now it's always a good idea to verify our formulas, so lets double check the above answer, using the standard C2H% formula (Eq. 6)

    AR = 1433, C2H% = (1433 / (1433 + 780)) * 1/X = 57.1119%
    AR = 2866, C2H% = (2866 / (2866 + 780)) * 1/X = 69.3301% (Result B.)

And making use of the percent formula, Eq. P1:

    PercentIncreaseForC2H% = {(New%C2H% / Orginal%C2H%) - 1} * 100
    = {(69.3301 / 57.1119) - 1} * 100
    = 21.3933%

Good! That matches Result A. (Actually I'm just happy all my Math worked out, as that means I didn't mess up

Using the other percent formula, Eq. P2:

    NewC2H = Current C2H + %Change
    = 57.1119 * 1.2139
    = 69.3301

(Again, the answer matches Result B.)

Double AR for a mere +12 in C2H% ??!!

**Conclusion:** Doubling our AR, doesn't double our C2H%.

* iii) **Effect of CLev on C2H%**

How will my C2H% change the closer I get to level 99, if I leave AR (Dex) the same?

Example:
My Mauler at level 80 had a C2H% of ~72%. This went up to 79% at level 99 without raising AR or Dex. That's a +7 increase! (Later on, we'll calculate how much AR (Dex) I would of needed to have had a 79% C2H% at level 80. That's the real question (& answer) we're after.)

Why did my C2H% go up by so much when I didn't directly add AR or Dex ?

If we take a look at Eq. 1
C2H% = 100 * AR / (AR + DR) * 2 * Clev / (Clev + MLev)
we see from it that the game factors in the difference between the attackers and defenders level (which I've highlighted above.) That is, it gets easier for us to hit a monster *just* by leveling up *without* changing our AR. (Hey, that saves us from putting stats into Dex!) This fact is a partial reason why a Mauler doesn't have to bother with Dex.

Immediate Conclusion: We may be able to have an good C2H% just by leveling up.

* iv) **Why can one char be effective with low Dex, and not another?**

Why do 2 chars, both at CLev 99 and with low Dex, have a such a drastic difference in C2H%? Specifically, why does my Mauler have a 79% C2H% while my MF Frenzy (were he at level 99) would have a 67% C2H% ?

If we ignore AR skills temporarily, we notice the Mauler has a lot of +AR from gear (specifically IK & charms.) But what's the big deal with +AR gear?

Using the corrected Eq. 2 (AR formula), we see that a +72 AR charm is effectively worth 20 points in Dex !

Proof:

    {Equation 2} AR = (Dex * 4) - 8
    72 = (Dex * 4) - 8
    Dex = 20

This is where I realized the concept of "Virtual Dex". If you have +AR items, you "effectively" have a higher Dex.

**Immediate Conclusion:** +AR Charms, in essence add, "Virtual Dex", due to AR being derived from Dex. (Eq.2)

--- 

# A2. Optimal way to increase C2H%

Here's a diagram showing how the order that Diablo 2 calculates our C2H%:

    [Figure 1]
    Dex -> DexAR -> + AR Items -> * AR% Skills -> * Level Difference Modifier -> C2H%

We can raise any stat along the way to increase our final C2H%. If we sacrifice our Dex, we still can have the same C2H% if we make it up by doing one (or more) of the following:

* a) Invest in skills that give +AR%, or
* b) Acquire +AR Gear (Weapons, Armor, Charms)
* c) Increase our CLev to a sufficiently high level

That's the real reason a Mauler Barb (or any other character) is viable with zero points invested in Dex and yet still have a good C2H% -- they are making it up in other ways.

Now, unfortunately, my MF Frenzy Barb doesn't have that luxury to use gear (since he's full of Magic Find charms), so he has to make up AR via other means -- namely Dex and Skills.

Let's see if we can come up with a rough guideline, based on the examples above, on what to do with Dex:

* Before adding/investing stats into Dex, calculate your C2H% at level 99 (based on your AR.)

* If it's > 85% then probably better off investing points you want to place into Dex into another stat (since Dex will be a bad ROI for you.)

* If it's < 80%, Boost your AR (in order from Easiest to Hardest) via:

  1) Gear (i.e. Helm that gives +AR%/level, charms, etc.), or
  2) With +AR% skills, or
  3) Leveling up.

* Then recalculate how much Dex you need to add, taking into consideration your bonuses from skills and gear.

At first glance, this might seem to be a chicken-and-egg problem:

* We don't know exactly how much AR we'll have at CLev 99, to determine our C2H%, which depends on our AR. Argh, recursive problem.

However, we do know that ultimately we're after having a good C2H%, so we can "break the cycle" and just decide what we want our C2H% to be! Then we work "backwards" -- calculating all the stats we need to support our desired C2H%.

Let's get busy and calculate the exact formulas we need to figure out the optimal Dex for our character(s).

---

# A3. Determining how much AR (Dex) you need, given C2H%

The previous section laid out our goals:

* First, we pick what we want our C2H% to be (at level 99.)
* Secondly, we calculate our AR,
* And lastly we calculate our Dex.

Pretty straight-forward.

Oh yeah, I guess the formulas would help.

Now since the answer will (ultimately) depend on your stats, and (final) skills, I'll give another example.

e.g. The Frenzy Barb wants around 80% C2H% at Level 99 against Meph.

To calculate the AR we need, use Equations. 3, 4, and 5:

    {Equation 3.} X = (CLev + MLev) / (100 * 2 * Clev)
    {Equation 4.} Y = X * C2H%
    {Equation 5.} AR = (Y * DR) / (1 - Y)

Solving for X:

    = ( 99 + 90 ) / (200 * 99) = 189 / 19800 = 0.009545

Solving for Y:

    Y = X * 80 = 0.7636

And solving for AR:

    AR = 2520

That's part of the answer.

    {Equation 2.} DexAR = (Dex * 4) - 8
    2520 = (Dex * 4) - 8
    Dex = 632

ACK! What did we do wrong? As that number is WAY too high.

Actually, our calculations are perfectly fine, however, we forgot one little detail: we ignored our +AR% skills!

OOPS!

Lets assume we have maxed our +AR% skills:

* Sword Master at SLev 20 = +180% AR
* Frenzy at SLev 20 = +233% AR
* AR %Skills = 180% + 233% = +413%

So our Frenzy Barb has an effective AR of AR * 5.13. That is:

    CurrentAR = (DexAR + ItemsAR) * AR%Skills
    2520 = (DexAR + 0) * 5.13
    DexAR = 491

    {Equation 2.} AR = (Dex * 4) - 8
    491 = (Dex * 4) - 8
    Dex = 125 (rounding up)

Whew! That's much more reasonable. (Notice how the answer is in the same ballpark as the Mauler with his 150 Dex.)

So that's why we have +AR% skills! To bring the Dex requirements for having a good C2H% out of the stratosphere down to a reasonable level.

And last but not least, since we already have 66 Dex, we only need to invest:

    = (124 - 66)
    = +57 Dex

To hit our target C2H% (pardon the pun.) ;-)

---

# A4. Changing AR effects C2H% how ?

Lets revisit the "double AR doesn't double C2H%" briefly.

To really see how painful doubling our AR is, let's calculate how much Dex we would need:

    {Equation 2.} AR = (Dex * 4) - 8

Our Frenzier with +AR% Skills & Items

    CurrentAR = (DexAR + ItemsAR) * AR%Skills
    2866 = (DexAR + 0) * 5.13
    DexAR = 559

And the total Dex we need:

    DexAR = (Dex * 4) - 8,
    559 = (Dex * 4) - 8
    Dex = 141

And finally the Dex we need to add:

    DexDelta = DexNew - DexOld
    = 141 - 66
    = +75

That's a WHOLE lot of Dex to double our AR, just to raise our C2H% up by +12 !

Double-checking:

    DexAR = (66+58)*4 - 8
    DexAr = 488
    CurrentAR = (DexAR + ItemsAR) * AR%Skills
    = (488) * 5.13
    AR = 2872

(If you're wondering why the resultant AR isn't exactly double our AR, it's because we need a fractional Dex increase, but since stats are only integers I choose to round up.)
i.e.

* +57 Dex would be a little shy of double AR.
* +58 Dex is just a tad over double AR.

For completeness, let's see how much our AR needs to change by, if we want to double out C2H%

Again, two alternate means of solving:

i) **Using Eq. 7:**

    {Equation 7.} PercentC2H%Increase = {(AR + DR) / (AR + DR/N) - 1} * 100

    100% = {(AR + DR) / (AR + DR/N) - 1} * 100
    2 = (AR + DR) / (AR + DR/N)
    N = (2 * DR) / (DR - AR)

ii) **Using Eq. 6:**

    {Equation 6.} C2H% = AR / (AR + DR) * (1 / X)

    2 * C2H% = (AR * N) / {(AR * N) + DR} * (1/X)
    2 * AR / (AR+DR) * (1/X) = (AR * N) / ((AR * N) + DR) * (1/X)

Canceling same terms on both sides (1/X and AR)

    2 / (AR + DR) = N / ((AR*N) + DR)
    (2 * N * AR) + (2 * DR) = N*AR + N*DR
    N = -2*DR / (AR - DR) which is actually the same as above.

(Multiply both numerator and denominator by -1)

This result is peculiar:

The denominator `(AR-DR)` shows us:

* First, that once we have a higher AR then DR, that we **can never double our C2H%.** We end up needing a negative AR, which is impossible. This might be a little clearer to see in this form, if divide both numerator and denominator by DR:

    N = 2 / (1 - AR/DR)

* Secondarily, as our AR approaches DR, we need an infinite amount of AR to double our C2H%.

**Conclusion:** We have very rapid decreasing retains on increasing our C2H% by raising AR.

To calculate how much AR you need to double your C2H%, use this formula:

    {Equation 8.} AR for Double C2H% = Current AR * 2 / {1 - (AR/DR)}

---

# A6. How do I keep that Block Rate up?

From Arreat Summit:

    Total Blocking = {Blocking * (Dexterity - 15)} / (Character Level * 2)

We have one equation, with 4 variables. We can't exactly "solve" it for Dex, since we would have an infinite number of answers.

The "trick" of picking our final value and working backwards to figure out the rest of the stats worked for us last time, so let's use that again.

The value we pick for Blocking doesn't really matter, just as long as we keep it constant -- let's pick a shield with 75% Blocking, and assume that's the only item with Blocking.

What does our Dex have to be, if we want to maintain the same blocking rate as we increase our level?

Proof:

Again, we have 2 ways of determining this.

i) We just could write down the first few levels and try to spot the pattern:

  * For CLev 1: 75% = 75% * (Dex - 15) / (1 * 2), Dex = 17
  * For CLev 2: 75% = 75% * (Dex - 15) / (2 * 2), Dex = 19
  * For CLev 3: 75% = 75% * (Dex - 15) / (3 * 2), Dex = 21

ii) Just directly work out the formula: We want our Blocking Rate for CLev {N+1} to be the same for CLev {N}. The term that modifies our blocking rate should be equal to one:

    (Dex - 15) / (2 * CLev) = 1
    Dex = (2 * CLev) + 15

 That gives us the total Dex we need per level.

 The Dex change per level up is (using the formula we just derived)

    Delta = New - Old
    = Dex for CLev N+1 - Dex for CLev N
    = {2 * (CLev+1) + 15} - {2 * (CLev+1) + 15}
    = 2*Clev + 2 + 15 - 2*CLev - 15
    = 2

**Conclusion:** We need to invest 2 Dex each time we increase our level to maintain the same blocking rate.
If your Dex is greater then (Clev * 2 - 15), the extra Dex will help you to have a higher blocking rate.

---

# Concluding Remarks:

To increase our Chance To Hit %, we want to increase our "Virtual Dex" via other means then Dex. This "frees" up stats that would of been placed there, to be invested into other skills, such as Str or Vit.

Barbs will want to raise their weapon mastery, and their combat skill (WW, Berserk, or Frenzy). Other character classes will want to invest in those skills that give them give +AR. Paladins: Fanaticism, Bowazons: Penetrate, etc.

If you can't afford the skills, try looking for items that give +AR, since they tend to give more "virtual Dex" then adding a few points of Dex alone.

---

Feel free to leave feedback via a [new issue](https://github.com/Michaelangel007/diablo2_melee_dex_analysis/issues/new) if something in this doc needs to be clarified further, or could be explained better.

Copyleft {C} 2002-2025, Michaelangel007.
May be freely used and distributed verbatim for non-commercial use.
